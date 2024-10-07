
# Sistema Bancario - Proyecto de Microservicios 

Este repositorio contiene la documentación y los diagramas UML del proyecto del sistema bancario basado en microservicios. El proyecto se compone de cuatro servicios:


1. **TransaccionMS**: Microservicio para la gestión de Transacciones Bancarias .
1. **CustomerMS**: Microservicio para la gestión de clientes.
2. **AccountMS**: Microservicio para la gestión de cuentas bancarias.
3. **Eureka Server**: Servicio de registro para la gestión y descubrimiento de microservicios.

## Diagramas UML
El repositorio incluye los siguientes diagramas:

- **Diagrama de Caso de Uso**
- **Diagrama de Secuencia**
- **Diagrama de Componentes**

## Estructura del Proyecto
### Microservicios y Servicios
El sistema está compuesto por cuatro servicios independientes:

1. **TransactionMS** - [Repositorio de AccountMS](https://github.com/Bailon18/transaction-ms)
2. **CustomerMS** - [Repositorio de CustomerMS](https://github.com/Bailon18/customer-ms)
3. **AccountMS** - [Repositorio de AccountMS](https://github.com/Bailon18/account-ms)
4. **Eureka Server** - [Repositorio de Eureka Server](https://github.com/Bailon18/eureka-server)

### Base de Datos
Cada microservicio se conecta a su propia base de datos MySQL alojada en Railway. Las configuraciones ya están predefinidas y no es necesario realizar ajustes adicionales para la conexión a la base de datos.

## Implementación en la Nube
Los microservicios están desplegados en Railway con la documentación de cada servicio disponible a través de Swagger, por lo que pueden ser testeados directamente en la nube utilizando los siguientes enlaces:

- **TransactionMS en la nube**: [TransactionMS Deployment](https://transaction-ms-production.up.railway.app/swagger-ui/index.html)
- **CustomerMS en la nube**: [CustomerMS Deployment](https://account-ms-production.up.railway.app/swagger-ui/index.html)
- **AccountMS en la nube**: [AccountMS Deployment](https://account-ms-production.up.railway.app/swagger-ui/index.html)
- **Eureka Server en la nube**: [Eureka Server Deployment](https://euraka-server-production.up.railway.app/)


## Ejecución Local
Si deseas ejecutar los microservicios localmente, sigue estos pasos:

### Requisitos Previos
- Java 11 o superior
- Maven
- MySQL instalado localmente
- Postman para probar los endpoints

### Instrucciones
1. Clona los repositorios correspondientes:

  ```yaml
   git clone https://github.com/Bailon18/transaction-ms
   git clone https://github.com/Bailon18/customer-ms
   git clone https://github.com/Bailon18/account-ms
   git clone https://github.com/Bailon18/eureka-server
   
   ```

2. Configura las bases de datos locales en `application.yml` para `TransactionMS`, `CustomerMS` y `AccountMS` . No es necesario cambiar la configuración de bases de datos se utilizas las bases de datos en Railway.

3. Descomenta las siguientes configuraciones para habilitar la ejecución local:

    #### TransactionMS
   - `client/AccountFeign.java` -> Elimina el parámetro `url` en la anotación `@FeignClient` para que apunte a la instancia local.
   - `resources/openapi.yaml` -> Verifica las rutas locales para los servicios.
   - `application.yml` -> Descomenta las siguientes líneas:
     ```yaml
     #defaultZone: http://localhost:8761/eureka/ 
     #hostname: localhost
     ```

   #### AccountMS
   - `client/ClienteFeign.java` -> Elimina el parámetro `url` en la anotación `@FeignClient` para que apunte a la instancia local.
   - `resources/static/openapi.yaml` -> Verifica las rutas locales para los servicios.
   - `application.yml` -> Descomenta las siguientes líneas:
     ```yaml
     #defaultZone: http://localhost:8761/eureka/ 
     #hostname: localhost
     ```

   #### CustomerMS
   - `client/AccountFeign.java` -> Elimina el parámetro `url` en la anotación `@FeignClient` para que apunte a la instancia local.
   - `resources/static/openapi.yaml` -> Verifica las rutas locales para los servicios.
   - `application.yml` -> Descomenta las siguientes líneas:
     ```yaml
     #defaultZone: http://localhost:8761/eureka/ 
     #hostname: localhost
     ```

   #### EurekaServer
   - `application.yml` -> Descomenta las siguientes líneas:
     ```yaml
     #server:
     #  port: 8761
     ```

4. Una vez que los tres servicios estén en ejecución, accede a:


   - **TransactionMS API**: [http://localhost:8084/cuentas](http://localhost:8084/cuentas)
   - **CustomerMS API**: [http://localhost:8082/clientes](http://localhost:8082/clientes)
   - **AccountMS API**: [http://localhost:8081/cuentas](http://localhost:8081/cuentas)
   - **Eureka Dashboard**: [http://localhost:8761/](http://localhost:8761/)

### Probar con Postman
Puedes utilizar Postman para realizar pruebas de los endpoints de cada microservicio. La documentación detallada de cada endpoint está disponible en los repositorios individuales.

## Descripción del Proyecto
Este sistema está planteado en el contexto de un banco ficticio llamado **Banco XYZ**. El propósito es gestionar clientes y cuentas bancarias utilizando una arquitectura de microservicios. Los servicios se comunican entre sí utilizando `FeignClient` y están registrados en el `Eureka Server`.

