# Anotaciones de Spring MVC y REST

## @Controller

Esta anotación se utiliza en clases Java que desempeñan el papel de controlador en su aplicación. La anotación @Controller permite la autodetección de clases de componentes en el classpath y las definiciones de bean de registro automático para ellas. Para habilitar la detección automática de dichos controladores anotados, puede agregar el escaneo de componentes a su configuración. La clase Java anotada con @Controller es capaz de manejar múltiples asignaciones de solicitudes.

Esta anotación se puede usar con Spring MVC y Spring WebFlux.

## @RequestMapping

Esta anotación se usa tanto a nivel de clase como de método. La anotación @RequestMapping se utiliza para asignar solicitudes web a clases de manejador y métodos de manejador específicos. Cuando @RequestMapping se usa en el nivel de clase, crea un URI base para el que se usará el controlador. Cuando esta anotación se utiliza en los métodos, le dará el URI en el que se ejecutarán los métodos del controlador. A partir de esto, puede inferir que la asignación de solicitud a nivel de clase seguirá siendo la misma, mientras que cada método de controlador tendrá su propia asignación de solicitud.

A veces es posible que desee realizar diferentes operaciones en función del método HTTP utilizado, aunque el URI de la solicitud puede permanecer igual. En tales situaciones, puede usar el atributo de método de @RequestMapping con un valor de método HTTP para limitar los métodos HTTP para invocar los métodos de su clase.

Aquí hay un ejemplo básico de cómo funciona un controlador junto con las asignaciones de solicitudes:

```java
@Controller
@RequestMapping("/welcome")
public class WelcomeController {
    @RequestMapping(method = RequestMethod.GET)
    public String welcomeAll() {
        return "welcome all";
    }
}
```

En este ejemplo, solo el método welcomeAll () maneja las solicitudes GET a / welcome.

Esta anotación también se puede usar con Spring MVC y Spring WebFlux.

## @CookieValue

Esta anotación se utiliza a nivel de parámetro de método. @CookieValue se usa como argumento de un método de mapeo de solicitud. La cookie HTTP está vinculada al parámetro @CookieValue para un nombre de cookie determinado. Esta anotación se utiliza en el método anotado con @RequestMapping.

Si se  que el siguiente valor de cookie se recibe con una solicitud HTTP:

`JSESSIONID=418AB76CD83EF94U85YD34W`

Para obtener el valor de la cookie, use @CookieValue de esta manera:

```java
@ReuestMapping("/cookieValue")
    public void getCookieValue(@CookieValue "JSESSIONID" String cookie){
}
```

## @CrossOrigin

Esta anotación se usa tanto a nivel de clase como de método para habilitar solicitudes de origen cruzado. En muchos casos, el host que sirve JavaScript será diferente del host que sirve los datos. En tal caso, Cross-Origin Resource Sharing (CORS) permite la comunicación entre dominios. Para habilitar esta comunicación, solo necesita agregar la anotación @CrossOrigin.

De forma predeterminada, la anotación @CrossOrigin permite todo el origen, todos los encabezados, los métodos HTTP especificados en la anotación @RequestMapping y una duración máxima de 30 min. Puede personalizar el comportamiento especificando los valores de atributo correspondientes.

A continuación se muestra un ejemplo del uso de @CrossOrigin en los niveles de método controlador y controlador:

```java
@CrossOrigin(maxAge = 3600)
@RestController
@RequestMapping("/account")
public class AccountController {
    @CrossOrigin(origins = "http://ejemplo.com")
    @RequestMapping("/message")
    public Message getMessage() {
        // ...
    }
    @RequestMapping("/note")
    public Note getNote() {
        // ...
    }
}
```

En este ejemplo, los métodos getExample () y getNote () tendrán una edad máxima de 3600 segundos. Además, getExample () solo permitirá solicitudes de origen cruzado de `http://ejemplo.com`, mientras que getNote () permitirá solicitudes de origen cruzado de todos los hosts.

## @RequestMapping (variantes)

Spring Framework 4.3 introdujo las siguientes variantes de nivel de método de la anotación @RequestMapping para expresar mejor la semántica de los métodos anotados. El uso de estas anotaciones se ha convertido en el método estándar para definir los puntos finales. Actúan como envoltorios para @RequestMapping.

Estas anotaciones se pueden usar con Spring MVC y Spring WebFlux.

### @GetMapping

Esta anotación se utiliza para asignar solicitudes HTTP GET a métodos de controlador específicos. @GetMapping es una anotación compuesta que actúa como un acceso directo para @RequestMapping (method = RequestMethod.GET).

### @PostMapping

Esta anotación se utiliza para asignar solicitudes HTTP POST a métodos de controlador específicos. @PostMapping es una anotación compuesta que actúa como un acceso directo para @RequestMapping (method = RequestMethod.POST).

### @PutMapping

Esta anotación se utiliza para mapear solicitudes HTTP PUT en métodos de manejador específicos. @PutMapping es una anotación compuesta que actúa como un acceso directo para @RequestMapping (method = RequestMethod.PUT).

### @PatchMapping

Esta anotación se usa para mapear solicitudes HTTP PATCH en métodos de manejador específicos. @PatchMapping es una anotación compuesta que actúa como un acceso directo para @RequestMapping (method = RequestMethod.PATCH).

### @DeleteMapping

Esta anotación se usa para asignar solicitudes HTTP DELETE a métodos de controlador específicos. @DeleteMapping es una anotación compuesta que actúa como un acceso directo para @RequestMapping (method = RequestMethod.DELETE).

### @ExceptionHandler

Esta anotación se usa a nivel de método para manejar excepciones a nivel de controlador. La anotación @ExceptionHandler se usa para definir la clase de excepción que atrapará. Puede usar esta anotación en los métodos que deben invocarse para manejar una excepción. Los valores de @ExceptionHandler se pueden establecer en una matriz de tipos de excepción. Si se produce una excepción que coincide con uno de los tipos de la lista, se invocará el método anotado con el @ExceptionHandler correspondiente.

### @InitBinder

Esta anotación es una anotación de nivel de método que desempeña el papel de identificar los métodos que inicializan WebDataBinder, un DataBinder que vincula el parámetro de solicitud a los objetos JavaBean. Para personalizar el enlace de datos de parámetros de solicitud, puede usar métodos anotados @InitBinder dentro del controlador. Los métodos anotados con @InitBinder incluyen todos los tipos de argumentos que admiten los métodos de controlador.

Se llamarán los métodos anotados de @InitBinder para cada solicitud HTTP si no especifica el elemento de valor de esta anotación. El elemento de valor puede ser un nombre de formulario único o múltiple o parámetros de solicitud a los que se aplica el método de enlace de inicio.

### @Mappings and @Mapping

Esta anotación se usa en campos. La anotación @Mapping es una metaanotación que indica una anotación de mapeo web. Al asignar diferentes nombres de campo, debe configurar el campo de origen en su campo de destino, y para hacerlo, debe agregar la anotación @Mappings. Esta anotación acepta una matriz de @Mapping que tiene los campos fuente y destino.

### @MatrixVariable

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes para que Spring pueda inyectar los bits relevantes de un URI de matriz. Las variables de matriz pueden aparecer en cualquier segmento, cada una separada por un punto y coma. Si una URL contiene variables de matriz, el patrón de mapeo de solicitud debe representarlas con una plantilla de URI. La anotación @MatrixVariable garantiza que la solicitud coincida con las variables de matriz correctas del URI.

### @PathVariable

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes.

La anotación @RequestMapping se puede usar para manejar cambios dinámicos en el URI donde un cierto valor de URI actúa como parámetro. Puede especificar este parámetro usando una expresión regular. La anotación @PathVariable se puede usar para declarar este parámetro.

### @RequestAttribute

Esta anotación se utiliza para vincular el atributo de solicitud a un parámetro de método de controlador. Spring recupera el valor del atributo nombrado para completar el parámetro anotado con @RequestAttribute. Mientras que la @RequestParamannotation se usa para vincular los valores de los parámetros de una cadena de consulta, @RequestAttribute se usa para acceder a los objetos que se han poblado en el lado del servidor.

### @RequestBody

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes. La anotación @RequestBody indica que un parámetro de método debe estar vinculado al valor del cuerpo de la solicitud HTTP. El HttpMessageConveter es responsable de convertir del mensaje de solicitud HTTP a objeto.

### @RequestHeader

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes.

La anotación @RequestHeader se usa para asignar el parámetro del controlador para solicitar el valor del encabezado. Cuando Spring asigna la solicitud, @RequestHeader verifica el encabezado con el nombre especificado dentro de la anotación y vincula su valor al parámetro del método del controlador. Esta anotación le ayuda a obtener los detalles del encabezado dentro de la clase de controlador.

### @RequestParam

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes.

A veces obtienes los parámetros en la URL de la solicitud, principalmente en las solicitudes GET. En ese caso, junto con la anotación @RequestMapping, puede usar la anotación @RequestParam para recuperar el parámetro URL y asignarlo al argumento del método. La anotación @RequestParam se usa para vincular parámetros de solicitud a un parámetro de método en su controlador.

### @RequestPart

Esta anotación se utiliza para anotar argumentos del método del controlador de solicitudes.

La anotación @RequestPart se puede usar en lugar de @RequestParam para obtener el contenido de una multiparte específica y vincularlo al argumento del método anotado con @RequestPart. Esta anotación tiene en cuenta el encabezado “Content-Type” en la multiparte (parte de solicitud).

### @ResponseBody

Esta anotación se utiliza para anotar métodos de manejo de solicitudes. La anotación @ResponseBody es similar a la anotación @RequestBody. La anotación @ResponseBody indica que el tipo de resultado debe escribirse directamente en el cuerpo de la respuesta en cualquier formato que especifique, como JSON o XML. Spring convierte el objeto devuelto en un cuerpo de respuesta mediante el HttpMessageConveter.

### @ResponseStatus

Esta anotación se utiliza en métodos y clases de excepción. @ResponseStatus marca un método o clase de excepción con un código de estado y un motivo que debe devolverse. Cuando se invoca el método del controlador, el código de estado se establece en la respuesta HTTP que anula la información de estado proporcionada por cualquier otro medio. Una clase de controlador también se puede anotar con @ResponseStatus, que luego se hereda con todos los métodos @RequestMapping.

### @ControllerAdvice

Esta anotación se aplica a nivel de clase. Como se explicó anteriormente, para cada controlador, puede usar @ExceptionHandler en un método que se llamará cuando ocurra una excepción dada. Pero esto maneja solo aquellas excepciones que ocurren dentro del controlador en el que está definido. Para superar este problema, ahora puede usar la anotación @ControllerAdvice. Esta anotación se utiliza para definir los métodos @ExceptionHandler, @InitBinder y @ModelAttribute que se aplican a todos los métodos @RequestMapping. Por lo tanto, si define la anotación @ExceptionHandler en un método en una clase @ControllerAdvice, se aplicará a todos los controladores.

### @SessionAttribute

Esta anotación se utiliza a nivel de parámetro de método. La anotación @SessionAttribute se usa para vincular el parámetro del método a un atributo de sesión. Esta anotación proporciona un acceso conveniente a los atributos de sesión existentes o permanentes.

### @SessionAttributes

Esta anotacion se aplica a nivel de tipo para un controlador especifico. La anotacion @SessionAtributes se usa cuando se desea agregar un objeto JavaBean en una sesión. Esto se utiliza cuando dea mantener el onjeti en la sesion por un periodo breve.
@SessionAttributes se usa junto con @ModelAttribute.

En el ejemplo se puede apreciar el uso:
```java
@ModelAttribute("person")
public Person getPerson() {}
// within the same controller as above snippet
@Controller
@SeesionAttributes(value = "person", types = {
    Person.class
})
public class PersonController {}

```
El nombre de @ModelAtttribute se asigna a @SessionAttributes como un valor. @SessionAttributes tiene dos elementos. El elemento de valor es el nombre de la session en el modelo y el elemento de tipos es el tipo de atributos de session en el modelo.
