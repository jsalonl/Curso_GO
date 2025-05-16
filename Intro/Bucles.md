# Bucles

Go solo tiene una estructura de bucle: for. Pero puede tomar varias formas:

1. Bucle clásico (tipo for de C)

```go
package main
import "fmt"

func main(){
    for i := 0; i < 10; i++ {
        fmt.Println(i)
    }
}
```

2. Bucle tipo while

```go
package main
import "fmt"

func main(){
    i := 0
    for i < 5 {
        fmt.Println(i)
        i++
    }
}
```

3. Bucle infinito

```go
package main
import "fmt"

func main(){
    for {
        fmt.Println("Loop infinito")
        break // O usar return
    }
}
```

4. Recorrer slices

```go
package main
import "fmt"

func main(){
    names := []string{"Alice", "Bob", "Charlie"}
    for i, name := range names {
        fmt.Println(i, name)
    }
}
```

4. Recorrer mapas

```go
package main
import "fmt"

func main(){
    balances := map[string]float64{
        "Alice": 100.0,
        "Bob": 250.5,
    }

    for user, balance := range balances {
        fmt.Println(user, balance)
    }

}
```

5. Saltos break y continue

```go
package main
import "fmt"

func main(){
    for i := 1; i <= 5; i++ {
        if i == 3 {
            continue // Salta el 3
        }
        if i == 5 {
            break // Sale del bucle
        }
        fmt.Println(i)
    }
}
```
