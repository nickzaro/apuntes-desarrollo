#Errores en GO
En go no existe excepciones como en otros lenguajes como c++, java, C#, ... etc. 
 El manejo de errores en go se realiza sin sobrecargar el valor del retorno.


```go
// implementar esta interfaz
type error interface {
    Error() string
}

```

#### ¿Como manejar el error?
* verificar si devuelve un error o no *if err!=nil {...}*
Un ejemplo de como usar:

```go
.....
func main(){
    f,err := os.Create("nombres.txt")
    if err != nil { // chequeo el error y retorno de darse este
        fmt.Println(err)
        return 
    }
    defer f.Close() // al final de la ejecución tiene que cerrarse el archivo
    ....
}
```

#### Printing y Logging
Opciones para imprimir o hacer logging de un error:
* ` fmt.Println() // imprime el mensaje del error`
* ` log.Println() // se guarda en un log el error`
* ` log.Fatalln() // muere la goroutine en la cual se provoco ese error se llama a os.Exit()`
* ` log.Panicln() // se pueden usar funciones diferidad y "recover" `
* ` panic() // `

##### Uso de:  ` fmt.Println()` y ` log.Println()`
```go
func main(){
    _,err := os.Open("archivo.txt")
    if err != nil{
        log.Println("un error ocurrio", err) // imprime el error por pantalla igual que con Println()
                                            // porque no fue especificado el archivo a donde escribir
    }
}
```
###### Definiendo el archivo de salida para el log
```go
func main(){
    f,err := os.Create("log.txt")
    if err != nil {
        fmt.Println(err)
    }
    defer f.close()
    log.SetOutPut(f) //uso el puntero para asignar el archivo en el cual escribira log

    f2,err := os.Open("archivo.txt")
    if err != nil{
        log.Println("un error ocurrio", err) // imprime el error por pantalla igual que con Println()
                                            // porque no fue especificado el archivo a donde escribir
    }

    defer f2.Close()
}
```

##### Uso de: ` log.Fatalln()`

```go
func main(){
    defer foo()
    _,err := os.Open("archivo.txt")
    if err != nil{
        log.Fatalln("un error ocurrio", err) // imprime el error y llama a os.Exit()
                                            // terminando la goroutine con codigo de retorno 1
                                            // la funcion diferida foo() no se ejecuta                                      
    }
}
```
##### Uso: `log.Panicln()` y `panic()`

```go
func main(){
    defer foo()
    _,err := os.Open("archivo.txt")
    if err != nil{
        log.Panicln("un error ocurrio", err) // parecido a fatal solo que en este caso se ejecutan
                                            // antes las funciones diferidas como foo(), luego
                                            // finaliza la goroutine con codigo de retorno 2
                                            // peude usar "recover" para evitar la finalización
                                            // panic() es similar
    }
}
```

#### Defer, Panic y Recover
##### Reglas del Defer
1. **Defer** es evaluado cuando en el momento que es leido la linea donde se declaró.

```go
func a(){
    i:= 0
    defer fmt.Prinln(i) //esto imprimirá 0 al final de la ejecución de la función
    i++
    return
}
```
2. **Defer** funciona como una pila, el ultimo que entra es el primero que sale.

```go
func b(){
    for i := 0; i < 4; i++ {
        defer fmt.Print(i) 
    }
    // por consola saldrá:3210
}
```
3. **Defer**  se ejecuta luego del return de la funcion.

```go

func main() {
    var x int
    x++
    fmt.Println(x)
    v := c()
    fmt.Println(v)
}
func c(i int){ // se pasa i = 1
    defer func(){i++}() // como defer se ejecuta luego del return 1
                        // func() retorna 2 y eso es lo que devuelve c(1)
    return 1 
}
// se imprimirá:
// 1
// 2

```

#### Recover
Toma el control de una goroutine en panic, se ejecuta y vuelve a la ejecución normal.
```go
func main() {
    f()
    fmt.Println("Retorna de manera normal desde f")
}

func f() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recuperando en f", r)
        }
    }()
    fmt.Println("Llamando g")
    g(0)
    fmt.Println("retorno normalmente desde g")
}

func g() {
    if i > 2 {
        fmt.Printl("Lanzando panic")
        panic(fmt.Sprintf("%v", i))
    }
    defer fmt.Println("defer en g",i)
    fmt.Println("Imprimiendo g", i)
    g(i + 1)
}
// Llamado g
// Imprimendo g 0
// Imprimendo g 1
// Imprimendo g 2
// Lanzando panic
// defer en g 2
// defer en g 1
// defer en g 0
// Recuperando en f 3
// Retorna de manera normal desde f

```
#### Info, personalizando los errores

Agregamos información a nuestros errores con: **errors.New()**

* %v -> valor
* %T -> tipo
.....

##### Personalizando el error

```go
func main() {
    _, err := sqrt(-123)
    if err != nil {
        log.Fatalln(err)
    }
}

func sqrt(f float64) (float64, error) {
    if f < 0 { // personalizo el error y retorno
        ErrorMat := fmt.Errorf("No hay raíz cuadrada de numeros negativos: %v", f)
        return 0, ErrorMat
    }
    return 42, nil
}

```

##### Implementando la interfaz Error

```go
type ubicacionError struct {
    lat string
    long string
    err error
}

func (n ubicacionError) Error() string { // implemento la interfaz error 
    return fmt.Sprintf("un error de concepto en: %v %v %v", n.lat, n.long, n.err)
} 

func main() {
    _, err := sqrt(-123)
    if err != nil {
        log.Println(err)
    }
}

func sqrt(f float64) ( float64, error) {
    if f < 0 {
        nme := fmt.Errorf("Raíz cuadrada de un numero negativo %v", f)
        return 0, ubicacionError{"55.2", "30.4", nme} // creando el objeto que implenta la interfaz
    }
    return 42, nil
}

```
