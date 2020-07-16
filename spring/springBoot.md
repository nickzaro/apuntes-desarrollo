# Anotaciones de Spring Boot

## @EnableAutoConfiguration

Esta anotación generalmente se coloca en la clase de aplicación principal. La anotación @EnableAutoConfiguration define implícitamente un “paquete de búsqueda” base. Esta anotación le dice a Spring Boot que comience a agregar beans según la configuración de classpath, otros beans y varias configuraciones de propiedades.

## @SpringBootApplication

Esta anotación se utiliza en la clase de aplicación al configurar un proyecto Spring Boot. La clase anotada con @SpringBootApplication debe mantenerse en el paquete base. Lo único que hace @SpringBootApplication es un escaneo de componentes. Pero escaneará solo sus subpaquetes. Como ejemplo, si coloca la clase anotada con @SpringBootApplication en el ejemplo com, entonces @SpringBootApplication escaneará todos sus subpaquetes, como com.mvit.a, com.apps.b y com.apps.a.x.

@SpringBootApplication es una anotación conveniente que agrega todo lo siguiente:

     @Configuración

     @EnableAutoConfiguration

     @ComponentScan
