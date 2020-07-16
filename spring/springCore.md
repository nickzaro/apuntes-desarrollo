# Anotaciones de Spring Core

## @Required

Esta anotación se aplica a los métodos de “setters” de beans. Si se considera un escenario en el se que necesita hacer cumplir una propiedad requerida. La anotación `@Required` indica que el bean afectado debe llenarse en el momento de la configuración con la propiedad requerida. De lo contrario, se genera una excepción de tipo `BeanInitializationException`.

## @Autowired

Esta anotación se aplica a campos, métodos de “setters” y constructores. La anotación @Autowired inyecta la dependencia del objeto implícitamente.

Cuando se usa @Autowired en los campos y se pasen los valores de los campos con el nombre de la propiedad, Spring asignará automáticamente los campos con los valores que se pasan.

Incluso se puede usar `@Autowired` en propiedades privadas, como se muestra a continuación.

```java
packge main

public class Customer {
    @Autowired
    private Person person;
    private int type;
}
```

Cuando usa `@Autowired` en métodos “setter”, Spring intenta realizarlo mediante Type autowiring en el método. Le está indicando a Spring que debe iniciar esta propiedad utilizando un método de “setter” donde se puede agregar su código personalizado, como inicializar cualquier otra propiedad con esta propiedad.

```java
public class Customer {
    private Person person;
    @Autowired
    public void setPerson (Person person) {
       this.person=person;
    }
}
```

Si se considera un escenario en el que necesita una instancia de clase A, pero no almacena A en el campo de la clase, este simplemente usa A para obtener una instancia de B, y está almacenando B en este campo. En este caso, `@Autowired` automáticamente del método setter se adaptará mejor. No tendrá campos no utilizados a nivel de clase.

Cuando se usa @Autowired en un constructor, la inyección del constructor ocurre en el momento de la creación del objeto. Le dice al constructor que se conecte automáticamente cuando se usa como un bean. Una cosa a tener en cuenta aquí es que solo un constructor de cualquier clase de bean puede llevar la anotación `@Autowired`.

```java
@Component
public class Customer {
private Person person;
@Autowired
public Customer (Person person) {
this.person=person;
}
}
```

Nota: A partir de Spring 4.3, @Autowired se convirtió en opcional en las clases con un solo constructor. En el ejemplo anterior, Spring aún inyectaría una instancia de la clase Person si omitiera la anotación @Autowired.

## @Qualifier  

Esta anotación se usa junto con la anotación @Autowired. Cuando necesita más control del proceso de inyección de dependencia, se puede utilizar @Qualifier. @Qualifier se puede especificar en argumentos de constructor individuales o parámetros de método. Esta anotación se utiliza para evitar la confusión que ocurre cuando crea más de un bean del mismo tipo y se desea conectar solo uno de ellos con una propiedad.

Considere un ejemplo donde una interfaz BeanInterface es implementada por dos beans, BeanB1 y BeanB2.

```java
@Component
public class BeanB1 implements BeanInterface {
    //
}
@Component
public class BeanB2 implements BeanInterface {
    //
}
```

Ahora, si BeanA automatiza esta interfaz, Spring no sabrá cuál de las dos implementaciones inyectar.  
Una solución a este problema es el uso de la anotación @Qualifier.

```java
@Component
public class BeanA {
    @Autowired
    @Qualifier("beanB2")
    private IBean dependency;
    ...
}
```

Con la anotación @Qualifier agregada, Spring ahora sabrá qué bean conectar automáticamente, donde beanB2 es el nombre de BeanB2.

## @Configuration

Esta anotación se usa en clases que definen beans. @Configuration es un análogo para un archivo de configuración XML: se configura mediante clases Java. Una clase Java anotada con @Configuration es una configuración en sí misma y tendrá métodos para crear instancias y configurar las dependencias.

Aquí hay un ejemplo:

```java
@Configuartion
public class DataConfig {
    @Bean
    public DataSource source() {
        DataSource source = new OracleDataSource();
        source.setURL();
        source.setUser();
        return source;
    }
    @Bean
    public PlatformTransactionManager manager() {
        PlatformTransactionManager manager = new BasicDataSourceTransactionManager();
        manager.setDataSource(source());
        return manager;
    }
}
```

## @ComponentScan

Esta anotación se usa con la anotación `@Configuration` para permitir que Spring conozca los paquetes para buscar componentes anotados. `@ComponentScan` también se utiliza para especificar paquetes base usando basePackageClasses o basePackage son atributos para escanear. Si no se definen paquetes específicos, el escaneo se realizará desde el paquete de la clase que declara esta anotación.

## @Bean

Esta anotación se utiliza a nivel de método. La anotación @Bean funciona con @Configuration para crear beans Spring. Como se mencionó anteriormente, @Configuration tendrá métodos para crear instancias y configurar dependencias. Dichos métodos serán anotados con @Bean. El método anotado con esta anotación funciona como la ID del bean, y crea y devuelve el bean real.

Aquí hay un ejemplo:

```java
@Configuration
public class AppConfig {
    @Bean
    public Person person() {
        return new Person(address());
    }
    @Bean
    public Address address() {
        return new Address();
    }
}
```

## @Lazy

Esta anotación se usa en clases de componentes. De forma predeterminada, todas las dependencias con conexión automática se crean y configuran al inicio. Pero si desea inicializar un bean “como una carga diferida”, se puede usar la anotación @Lazy sobre la clase. Esto significa que el bean se creará e inicializará solo cuando se solicite por primera vez. También puede usar esta anotación en las clases de @Configuration. Esto indica que todos los métodos de @Bean dentro de esa @Configuración deben inicializarse “como una carga diferida”.

## @Value

Esta anotación se utiliza en los niveles de campo, parámetro de constructor y parámetro de método. La anotación @Value indica una expresión de valor predeterminado para el campo o parámetro para inicializar la propiedad. Como la anotación @Autowired le dice a Spring que inyecte un objeto en otro cuando carga el contexto de su aplicación, también puede usar la anotación @Value para inyectar valores de un archivo de propiedades en el atributo de un bean. Admite marcadores de posición # {…} y $ {…}.


https://mvitinnovaciontecnologica.wordpress.com/2020/02/06/guia-de-anotaciones-de-spring-framework/