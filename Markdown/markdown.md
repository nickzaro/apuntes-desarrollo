<!--Titulos-->
# Markdown

```
# Titulo h1
## Titulo h2
### Titulo h3
#### Titulo h4
##### Titulo h5
###### Titulo h6
```

# Titulo h1
## Titulo h2
### Titulo h3
#### Titulo h4
##### Titulo h5
###### Titulo h6

## Formato texto

```
*Italica*
**Negrita**
~~Tachado~~
```

*Italica*
**Negrita**
~~Tachado~~


## Listas desordenadas

```
* un item
    * sub item
* otro item
* otro mas
```

* un item
    * sub item
* otro item
* otro mas

## Lista ordenada

```
1. primer item
    1. un sub item
2. segundo item
3. tercer item
```
1. primer item
    1. un sub item
2. segundo item
3. tercer item

## Enlaces

` [Google](http://www.google.com)`

[Google](http://www.google.com)

## Citas

```
> Cita en  markdown
```

> Cita en  markdown

## Una linea divisoria

```
--- 

___

```

--- 

___

## Codigo de una sola linea

```
` console.log("Una linea de codigo")`
```

` console.log("Una linea de codigo")`

## Codigo multilinea

> \```go
packge main
> func main(){
    println("Hola Go")
}
> \```


```go
packge main

func main(){
    println("Hola Go")
}

```

## Tabla

```
|Titutlo1   |Titulo2     |Titulo3    |
|-----------|:-----------|-----------|
|Elemento1  |Elemento2   |Elemento3  |
|*Elemento4*|`Elemento5 `|Elemento6  |
```

|Titutlo1   |Titulo2     |Titulo3    |
|-----------|:-----------|-----------|
|Elemento1  |Elemento2   |Elemento3  |
|*Elemento4*|`Elemento5 `|Elemento6  |

## Imagenes

### Logo de enlace web

` ![Logo de google de enlace web](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
`

![Logo de google de enlace web](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

### Logo de imagen local

` ![Logo de google de imagen local](googlelogo.png) `

![Logo de google de imagen local](googlelogo.png)

## Check en github

```
* [x] Tarea 1
* [x] Tarea 2
* [ ] Tarea 3
* [ ] Tarea 4
```

* [x] Tarea 1
* [x] Tarea 2
* [ ] Tarea 3
* [ ] Tarea 4

## Emojis en github

```
:smile:
:stuck_out_tongue:
```


:smile:
:stuck_out_tongue:

## Video en github

` [![IMAGE ALT TEXT HERE](video.PNG)](https://www.youtube.com/watch?v=D8-YSqAoxD4) `

[![IMAGE ALT TEXT HERE](video.PNG)](https://www.youtube.com/watch?v=D8-YSqAoxD4)


## Diagramas Plantuml

````
class Object{
    equals()
}
class ArrayList {
    Object[] elementData
    sizeHI
    toString()
}
Object<|--ArrayList
````

```plantuml
class Object{
    equals()
}
class ArrayList {
    Object[] elementData
    sizeHI
    toString()
}
Object<|--ArrayList
```

```
start
if (condition A) then (yes)
  :Text 1;
elseif (condition B) then (yes)
  :Text 2;
  stop
elseif (condition C) then (yes)
  :Text 3;
elseif (condition D) then (yes)
  :Text 4;
else (nothing)
  :Text else;
endif
stop
```

```plantuml
start
if (condition A) then (yes)
  :Text 1;
elseif (condition B) then (yes)
  :Text 2;
  stop
elseif (condition C) then (yes)
  :Text 3;
elseif (condition D) then (yes)
  :Text 4;
else (nothing)
  :Text else;
endif
stop
```

## Formulas

` $$\int_{-\infty}^\infty e^{-x^2} = \sqrt{\pi}$$ `

$$\int_{-\infty}^\infty e^{-x^2} = \sqrt{\pi}$$