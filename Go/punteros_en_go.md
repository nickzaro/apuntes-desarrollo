# Punteros en Go

Es un valor almacenado en memoria, cada ubicacion de memoria tiene una dicerrcion.
* &int
* *int

```go
func main() {
    a := 42
    fmt.Println(a) // imprime el valor, 42
    fmt.Println(&a) // imprime la direccion donde se guarda el valor, 0x10242332

    fmt.Printf("%T\n", a)  // int
    fmt.Printf("%T\n", &a) // *int

var b *int =&a
fmt.Println(b) //  la dirección de memoria de a, 0x10242332
fmt.Println(*b) // desreferenciado imprime el valor, 42
}

```

## Como usar los punteros

En Go todo los parametros que se pasan son por valor, es decir que no se modifica su contenido, por esa razón se usan los punteros, para poder pasar un referencia a la variable que se quiere pasar y poder modificar su contenido.

```go
package main

import (
	"fmt"
)

func main() {
    x := 0
    porValor(x) // no modifica el valor de la variable
    fmt.Println(x) //  0
    porReferencia(&x) // modifica el valor de la variable
    fmt.Println(x) // 10
}

func porValor(n int) {
    n = n + 10
    fmt.Println(n) // 10
}

func porReferencia(n *int) {
    *n = *n + 10
    fmt.Println(*n) // 10
}
```

## Method Sets

| Receptores    | Valores   |
|---------------|-----------|
|    (t T)      |  T y *T   |
|    (t *T)     |   *T      |


* Si el receptor es de tipo `(t T)` entonces se puede pasar valores `T y *T`.
* Si el receptor es de tipo `(t *T)` entonces solo se puede pasar valores de tipo `*T`.


