# Condicionales

Estructuras que permiten tomar decisiones en el flujo de ejecución de un programa.

1. If, Else, Else If

Los condicionales "if-else if" son una forma de tomar decisiones en programación. Funcionan de la siguiente manera:

- Se inicia con un "if" que evalúa una condición. Si la condición es verdadera, se ejecuta un bloque de código asociado a ese "if".
- Si la condición del primer "if" es falsa, se pasa al siguiente "else if" (si lo hay). Se evalúa la condición del "else if", y si es verdadera, se ejecuta el bloque de código asociado a ese "else if".
- Este proceso se repite para cada "else if" en secuencia hasta que se encuentra una condición verdadera o hasta que no hay más "else if". Si se encuentra una condición verdadera, se ejecuta el bloque de código correspondiente y se sale de la estructura condicional.
- Si ninguna de las condiciones "if" o "else if" es verdadera, se ejecuta el bloque de código del "else" (si está presente), que es el último recurso.

Ejemplo de if:
```go
if edad < 18 {
    fmt.Println("No puedes pasar")
}
```

Ejemplo de if-else
```go
edad := 65

if edad < 18 {
    fmt.Println("No puedes pasar")
} else {
    fmt.Println("Puedes pasar")
}
```

Ejemplo de if-else if
```go
edad := 18

if edad < 18 {
    fmt.Println("No puedes pasar")
} else if edad > 50 {
    fmt.Println("No puedes pasar")
} else  {
    fmt.Println("Tienes que ser mayor de 18 años y menor de 50 años para poder pasar"
}
```

> Buenas practicas:
> 1. Siempre usar early returns
> 2. Evitar anidaciones profundas
> 3. Else solo cuando es necesario

Mal:
![nested if](nested_if.png)

Mal:
```go
var accesoPermitido bool
if edad < 18 {
    accesoPermitido = false
}else{
    accesoPermitido = true
}

fmt.Println(accesoPermitido)
```

Mejor:
```go
accesoPermitido := false
if edad > 18 {
    accesoPermitido = true
}

fmt.Println(accesoPermitido)
```

2. Switch

La estructura switch es una forma de control de flujo en programación que permite simplificar múltiples comparaciones de una variable contra diferentes valores. Funciona de la siguiente manera:

**Inicio de switch:** La estructura comienza con la palabra clave switch, seguida de la variable o expresión que quieres comparar.

**Casos (case):** Dentro del bloque de switch, defines diferentes casos usando la palabra clave case, seguida de un valor específico que quieres comparar con la variable o expresión del switch. Si la variable o expresión coincide con el valor del case, se ejecuta el bloque de código asociado a ese case.

**Ejecución de un Caso:** Cuando se encuentra una coincidencia entre la variable y un case, se ejecuta el código asociado a ese case y luego se sale de la estructura switch. Esto significa que solo se ejecuta el código de un case coincidente.

**Break:** Aunque en algunos lenguajes es necesario usar la palabra clave break al final de cada bloque case para evitar que el control fluya hacia el siguiente case, en algunos lenguajes modernos como Go, el break es implícito y no es necesario escribirlo.

**default:** Puedes incluir un default al final del switch, que se ejecutará si ninguno de los case coincide. Es similar a un else en una estructura if-else.

```go
var monthNumber int = 3
var station string

switch {
    case monthNumber >= 1 && monthNumber < 3:
        station = "Winter"
    case monthNumber >= 3 && monthNumber < 6:
        station = "Spring"
    case monthNumber >= 6 && monthNumber < 9:
        station = "Summer"
    case monthNumber >= 9 && monthNumber < 12:
        station = "Autumn"
    default:
        station = "Ninguna Estación del Año!"
}
fmt.Println(station)
```

**Fallthrough:** Se usa cuando se desea que el flujo siga
```go
switch num := 2; num {
case 1:
    fmt.Println("Uno")
case 2:
    fmt.Println("Dos")
    fallthrough
case 3:
    fmt.Println("Tres")
}
```

**Finally:** No existe en go, pero podemos usar defer en su lugar (se hablara en proximos capitulos de esto)

3. Goto

Una opcion para saltar un bloque de codigo, y no se detiene el flujo normal del programa. Se usa cuando se desea que el flujo siga

```go
num  := 10

if num > 15 {
    goto fin
}
fmt.Println("Saliendo del if")

fin: 
    fmt.Println("Fin del programa")
```

Aunque se puede usar, no se recomienda, ya que puede generar dificultad de lectura y mantenimiento.
