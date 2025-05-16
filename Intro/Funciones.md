# Funciones

Una función es un bloque de código que realiza una tarea específica. En Go, se definen con la palabra clave func. Se usan para dividir un programa en partes más pequeñas, legibles y reutilizables.

## Tipos de funciones

Go tiene varios tipos de funciones según cómo se usan:

1. Funciones estándar (simples)

    Una función que recibe parámetros y retorna un valor.

    📌 ¿Cuándo se usa?
    Cuando necesitas encapsular una operación básica que transforma uno o más valores.

    🧩 Ejemplo: Recargar el saldo de una tarjeta.

    🎯 Problema que resuelve: Centraliza la lógica de recarga, evitando repetir la misma fórmula en varias partes del código.

    ```go
    package main
    import "fmt"

    func topUpBalance(balance float64, amount float64) float64 {
        return balance + amount
    }

    func main() {
        balance := 1500.0
        balance = topUpBalance(balance, 500.0)
        fmt.Println("New balance:", balance)
    }
    ```

2. Funciones con múltiples valores de retorno

    Go permite retornar más de un valor.

    📌 ¿Cuándo se usa?
    Cuando necesitas más de un resultado, como un valor y un estado.

    🧩 Ejemplo: Procesar un pago: devuelve el nuevo saldo y si fue exitoso.

    🎯 Problema que resuelve: Permite manejar errores o condiciones sin excepciones, usando el segundo valor como control.

    ```go
    package main
    import "fmt"

    func processPayment(balance float64, amount float64) (float64, bool) {
        if amount > balance {
            return balance, false
        }
        return balance - amount, true
    }

    func main() {
        balance := 1000.0
        newBalance, success := processPayment(balance, 200.0)
        fmt.Println("Payment successful:", success)
        fmt.Println("Remaining balance:", newBalance)
    }
    ```

3. Funciones con valores nombrados de retorno

    Nombras las variables de retorno directamente en la firma de la función.

    📌 ¿Cuándo se usa?
    Cuando quieres mejorar la claridad del propósito de cada valor retornado.

    🧩 Ejemplo: Obtener información de un usuario.

    🎯 Problema que resuelve: Documenta mejor qué representa cada valor retornado, lo que ayuda al mantenimiento del código.

    ```go
    package main
    import "fmt"

    func getUser() (name string, active bool) {
        name = "Carlos"
        active = true
        return
    }

    func main() {
        name, active := getUser()
        fmt.Println("User:", name, "Active?", active)
    }
    ```

4. Funciones variádicas

    Aceptan un número variable de argumentos.

    📌 ¿Cuándo se usa?
    - Cuando no sabes cuántos argumentos vas a recibir.
    - Cuando querés ofrecer parámetros opcionales o permitir llamadas más flexibles.
    - Para operaciones sobre listas de valores: sumas, validaciones, formateo, etc.

    🧩 Ejemplo: Sumar varios cargos a una cuenta.

    🎯 Problema que resuelve:
    Aumenta la flexibilidad: 
    - Permite que la función reciba 0, 1 o muchos valores.
    - Evita tener que pasar un slice manualmente.
    - Permite simular parámetros opcionales, ya que los argumentos pueden omitirse o personalizarse.

    ```go
    package main
    import "fmt"

    func sumCharges(charges ...float64) float64 {
        total := 0.0
        for _, charge := range charges {
            total += charge
        }

        return total
    }

    func main() {
        total := sumCharges(100.0, 200.0, 50.5)
        fmt.Println("Total charges:", total)
    }
    ```
    
    Parametros opcionales

    ```go
    package main
    import "fmt"
    func greet(name string, nicknames ...string) {
        if len(nicknames) > 0 {
            fmt.Printf("Hello %s, aka %s!\n", name, nicknames[0])
        } else {
            fmt.Printf("Hello %s!\n", name)
        }
    }

    func main() {
        greet("Carlos")
        greet("Carlos", "Charlie")
    }

    ```

5. Funciones anónimas (funciones literales)

    Se definen sin nombre y pueden ejecutarse en el momento o asignarse a variables.

    📌 ¿Cuándo se usa?
    - Cuando necesitas una función rápida y local que se usa solo una vez.
    - Cuando no tiene sentido crear una función con nombre.
    - Cuando trabajás con concurrencia (go), especialmente para procesos en segundo plano o tareas asíncronas.

    🧩 Ejemplo: Validar si un monto cumple una condición mínima.

    🎯 Problema que resuelve: Evita tener que declarar funciones por separado cuando solo se usan una vez.

    ```go
    package main
    import "fmt"

    func main() {
        validateAmount := func(amount float64) bool {
            return amount >= 100
        }

        fmt.Println("Is valid amount?", validateAmount(150))
    }
    ```

6. Funciones como valores (funciones de primera clase)

    Puedes pasar funciones como argumentos o retornarlas.

    📌 ¿Cuándo se usa?
    Cuando quieres aplicar distintas operaciones sin duplicar lógica.

    🧩 Ejemplo: Aplicar un interés o un descuento al saldo.

    🎯 Problema que resuelve: Permite definir comportamientos intercambiables, útil en reglas de negocio.

    ```go
    package main
    import "fmt"

    // Función que aplica una operación a un balance
    func applyOperation(balance float64, operation func(float64) float64) float64 {
        return operation(balance)
    }

    func main() {
        // Interés simple
        simpleInterest := func(b float64) float64 { return b * 1.05 }

        // Interés compuesto
        compoundInterest := func(b float64) float64 { return b * 1.10 }

        balance := 1000.0

        // Aplicar interés simple
        newBalanceSimple := applyOperation(balance, simpleInterest)
        fmt.Println("Balance con interés simple:", newBalanceSimple)

        // Aplicar interés compuesto
        newBalanceCompound := applyOperation(balance, compoundInterest)
        fmt.Println("Balance con interés compuesto:", newBalanceCompound)
    }
    ```

7. Closures (funciones que capturan variables del entorno)

    Funciones que recuerdan las variables de su contexto.

    📌 ¿Cuándo se usa?
    Cuando necesitas que una función recuerde el estado entre llamadas.

    🧩 Ejemplo: Generar IDs de usuario incrementalmente.

    🎯 Problema que resuelve: Permite mantener una variable privada sin exponerla globalmente.

    ```go
    package main
    import "fmt"

    func idGenerator() func() int {
        id := 0
        return func() int {
            id++
            return id
        }
    }

    func main() {
        generateID := idGenerator()
        fmt.Println("User ID:", generateID())
        fmt.Println("User ID:", generateID())
    }
    ```

8. Métodos (funciones asociadas a un tipo)

    Funciones que se asocian a un tipo (struct)

    📌 ¿Cuándo se usa?
    Cuando una función actúa sobre una estructura de datos específica.

    🧩 Ejemplo: Mostrar el saldo de una tarjeta.

    🎯 Problema que resuelve: Agrupa comportamientos con los datos que afectan, similar a métodos en OOP.

    ```go
    package main
    import "fmt"

    type Card struct {
        Number string
        Balance float64
    }

    func (c Card) PrintBalance() {
        fmt.Printf("Card %s has balance: %.2f\n", c.Number, c.Balance)
    }

    func main() {
        card := Card{Number: "1234-5678", Balance: 1200.0}
        card.PrintBalance()
    }
    ```

9. Funciones recursivas

    Funciones que se llaman a sí mismas.

    📌 ¿Cuándo se usa?
    Cuando el problema se puede definir en términos de sí mismo (ej: factorial, árbol, suma acumulada).

    🧩 Ejemplo: Sumar pagos de los últimos N días.

    🎯 Problema que resuelve: Reduce el uso de bucles en operaciones matemáticas o algoritmos recursivos.

    ```go
    package main
    import "fmt"

    func cumulativePayments(n int) int {
        if n == 0 {
            return 0
        }

        return n + cumulativePayments(n-1)
    }

    func main() {
        total := cumulativePayments(5)
        fmt.Println("Total cumulative payments:", total)
    }
    ```

10. Funciones defer (diferidas)

    Se ejecutan al final de la función donde están definidas.

    📌 ¿Cuándo se usa?
    Cuando necesitas asegurar que algo se ejecute al final de una función (liberar recursos, registrar logs, enviar métricas, etc.).

    🧩 Ejemplo: Registrar cierre de sesión de un usuario.

    🎯 Problema que resuelve: Evita olvidar ejecutar tareas críticas al final de una función.

    ```go
    package main
    import "fmt"

    func logoutUser(username string) {
        defer fmt.Println("Logging out:", username)
        fmt.Println("Performing cleanup...")
    }

    func main() {
        logoutUser("Carlos")
    }
    ```