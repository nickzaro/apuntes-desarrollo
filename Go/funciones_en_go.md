## Funciones en Go

### Interfaces y Polimorfismo

* En Go los valores pueden ser de mas de un tipo y depende de las interfaces que implemente.
* La interfaz en un tipo de dato, y es una colección de metodos que definimos.
* El tipo que implementa los metodos definidos en la interfaz, implicitamente implementa la interfaz.
* Las Interfaces nos permiten definir comportamiento.

```go
type persona struct {
    nombre    string
    aperllido string
}

type agenteSecreto struct {
    persona
    lpm bool
}

type humano interface {
    presentarse()
}

// presentarse, agenteSecreto al implementar el metodo presentar de la interfaz humano sera tambien de tipo humano
func (a agenteSecreto) presentarse() { 
    fmt.Println("Hola, soy", a.nombre, a.apellido, "un agente secreto")
}

// presentarse, persona al implementar el metodo presentar de la interfaz humano sera tambien de tipo humano
func (p persona) presentarse() { 
    fmt.Println("Hola, soy", p.nombre, p.apellido, "una persona")
}
// sePresenta, puede recibir al tipo agenteSecreto o persona los cuales implementan la interfaz humano
func sePresenta(h humano) {
    h.presentarse()
}

func main() {
    p := persona{
        nombre: "Juan",
        apellido: "Perez",
    }

    as := agenteSecreto {
        persona: persona {
            nombre: "Pepe",
            apellido: "Rodriguez"
        },
        lpm: true,
    }

    sePresenta(p)// se ejecutara la funcion presentarse() de la persona
    sePresenta(as)// se ejecutara la funcion presentarse() del agenteSecreto
}

```
#### Conversion de Tipos y Afirmación

##### Conversion:
```go
type myEntero int

func main {
    var x myEntero = 20
    fmt.Println(x) // 20
    fmt.Printf("%T", x) // main.myEntero
    var y int
    y = int(x) // se realiza la conversion si asigno directamente y = x da error
    fmt.Println(y) // 20
    fmt.Printf("%T", y) // main.int
}
```
##### Afirmación:

```go
...
// Todo igual al primer caso con excepcion de sePresenta
func sePresenta(h humano) {
    switch h.(type) {
        case persona:
            fmt.Println("Pasado por la función sePresenta", h.(persona).nombre) 
            // afirmo al compilador que es del tipo persona y por tanto tiene un atributo nombre
        case agenteSecreto:
            fmt.Println("Pasado por la función sePresenta", h.(agenteSecreto).nombre) 
            // afirmo al compilador que es del tipo agenteSecreto y por tanto tiene un atributo nombre
    }
}
...

```


