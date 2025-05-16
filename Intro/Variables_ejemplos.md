# Variables y tipos de datos (Ejemplos)

## Cuando usar map y cuando usar struct

En Go podemos representar estructuras de datos complejas tanto con struct como con map[string]any. Ambos tienen sus usos, pero la elección depende del objetivo del código.


| Situación | Struct o Map? | Por qué? |
|---|---|---|
| Modelo de datos conocido y validable	| ```struct``` |  Seguridad, validación, claridad. |
| Comunicación con APIs bien definidas | ```struct``` |  Facilita encoding/decoding (json.Marshal, etc). |
| Payloads dinámicos (logs, plantillas, JSON libre)	| ```map[string]any``` |  Flexibilidad para estructuras que no son fijas o varían mucho. |
| Prototipado rápido | ```map[string]any``` | Más rápido para pruebas sin definir tipos.
 |

### 1. Usando Struct

Cuando el modelo es conocido y estable

```go
type CustomerRequest struct {
	FirstName      string         `json:"first_name" validate:"required"`
	LastName       string         `json:"last_name" validate:"required"`
	Identification Identification `json:"identification" validate:"required"`
}

type Identification struct {
	Type   string `json:"type"`
	Number string `json:"number"`
}

func createUser() CustomerRequest{
    return CustomerRequest{
		FirstName:      "Joan",
		LastName:       "Nieto",
		Identification: Identification{
			Type: "CC",
			Number: "123",
		},
	}
}
```

✅ Ventajas de usar struct:

- Tipos fuertes y seguros: ayuda al compilador a detectar errores.
- Validaciones fáciles: gracias a etiquetas como validate:"required".
- Auto-completado y navegación: excelente para desarrollo en IDEs.
- Mejor mantenibilidad: el esquema queda claro para cualquier persona que lea el código.
- Documentación automática: más fácil de generar con go doc o herramientas similares.

❌ Desventajas:

- Requiere definir todos los campos con anticipación.
- Menos flexible si el JSON puede cambiar mucho (campos opcionales, estructuras dinámicas).

### 2. Usando map

Cuando la estructura es flexible o desconocida en tiempo de compilación

```go
func createUserMap() map[string]any {
	return map[string]any{
		"first_name": "Joan",
		"last_name":  "Nieto",
		"identification": map[string]any{
			"type":   "CC",
			"number": "123",
		},
	}
}
```

✅ Ventajas de usar map:

- Mayor flexibilidad: útil cuando no se conoce la estructura de antemano.
- Ideal para armar respuestas dinámicas o datos parcialmente definidos.
- Permite agregar o quitar claves fácilmente en tiempo de ejecución.
- Útil en prototipos o pruebas rápidas, sin necesidad de definir nuevos tipos.

❌ Desventajas:

- Menor seguridad de tipos: los errores pueden aparecer solo en tiempo de ejecución.
- No permite validación automática con tags (validate:"required").
- Menor soporte de autocompletado y refactorización en IDEs.
- Posible pérdida de claridad o estructura del código.