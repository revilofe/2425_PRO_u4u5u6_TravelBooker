# Actividad: Desarrollo de Proyecto Software en Kotlin

**ID actividad:** 2425_PRO_u4u5u6_taskManager

**Agrupamiento de la actividad**: Individual 

---

### Descripción: **Ejercicio: Gestor de Reservas para una Agencia de Viajes**

En este ejercicio, crearás una plicación en la que aplicarás los conceptos de Programación Orientada a Objetos (POO) en Kotlin, incluyendo herencia, interfaces, clases abstractas, principios SOLID y arquitectura en capas. La aplicación simula un gestor de reservas para una agencia de viajes, permitiendo la creación y consulta de reservas de vuelo y de hotel. 

#### **Contexto y Objetivo**

Desarrolla una aplicación de consola en Kotlin que permita gestionar **reservas** en una agencia de viajes. Estas reservas se dividen en dos tipos: **Reserva de Vuelo** y **Reserva de Hotel**. Ambas derivan de una superclase o interfaz denominada **Reserva**.

La aplicación debe seguir una **arquitectura en capas**, separando claramente:
- **La capa de presentación (UI):** se encarga de la interacción con el usuario a través de la consola.
- **La capa de lógica de aplicación:** gestiona la lógica de negocio (creación, almacenamiento y manejo de reservas).
- **La capa de acceso a datos:** aunque en este ejercicio se puede utilizar un repositorio en memoria, se debe abstraer su acceso mediante interfaces, aplicando el principio de inversión de dependencias.

#### **Requerimientos Funcionales y No Funcionales**

1. **Arquitectura en Capas y Principio de Inversión de Dependencias**
  - La lógica de negocio debe depender de abstracciones (por ejemplo, interfaces de repositorios) y no de implementaciones concretas.
  - La comunicación entre la interfaz de usuario y la lógica de negocio debe estar claramente separada.

2. **Modelo de Dominio: Reserva, Reserva de Vuelo y Reserva de Hotel**
  - **Reserva (Superclase o Interfaz):**
    - Contendrá la lógica común a todas las reservas, aunque no se permitirá la creación de una instancia de la misma.
    - Posee un **id**. Se asigna automáticamente al crear la instancia. No puede ser nula y no se puede modificar.
    - Posee una **fechaCreacion**. Se asigna automáticamente al crear la instancia. No puede ser nula y no se puede modificar.
    - Posee una **descripcion**. No puede ser nula (por ejemplo, descripción del itinerario o servicio).
    - Debe incluir una propiedad `detalle`, cuyo getter utilice la lógica común para concatenar el *id* y la descripción.
  - **Reserva de Vuelo:**
    - Hereda las propiedades de Reserva.
    - Posee atributos propios: **origen**, **destino** y **horaVuelo**.
    - La propiedad **detalle** se genera dinámicamente, por ejemplo:  
      `id + " - " + descripcion + " - " + origen + " -> " + destino [horaVuelo]`.
    - Su constructor es **privado**. Se debe disponer de un método de clase (companion object) llamado `creaInstancia` para generar una nueva instancia.
    - Sobreescribe `toString` para mostrar formateada toda la información de la reserva de vuelo.
  - **Reserva de Hotel:**
    - Hereda las propiedades de Reserva.
    - Posee atributos propios: **ubicacion** y **numeroNoches**.
    - La propiedad **detalle** se genera dinámicamente, por ejemplo:  
      `id + " - " + descripcion + " - " + ubicacion (numeroNoches)`.
    - Al igual que Reserva de Vuelo, su constructor es privado y se debe utilizar el método `creaInstancia` para crear instancias.
    - Sobreescribe `toString` para mostrar formateada toda la información de la reserva de hotel.

3. **Buenas Prácticas y Principios SOLID**
  - Utiliza el principio de **inversión de dependencias**: la lógica de negocio no debe depender de clases concretas para el almacenamiento de las reservas.
  - Documenta y comenta el código de forma clara, explicando las decisiones de diseño, especialmente aquellas que no están explícitamente indicadas en la descripción.
  - Separa los métodos estáticos (en Kotlin se implementan mediante *companion objects*) y asegúrate de que la creación de instancias se haga mediante el método `creaInstancia`.
  - Integra el uso de **clases genéricas** (por ejemplo, en la implementación del repositorio) y **expresiones regulares** para validar ciertos formatos de entrada (por ejemplo, el formato de la hora en la Reserva de Vuelo).

4. **Interfaz de Usuario (Consola)**
  - La aplicación debe interactuar con el usuario a través de la consola, mostrando un menú que permita:
    - Crear una nueva reserva (seleccionando entre Reserva de Vuelo o Reserva de Hotel).
    - Listar todas las reservas registradas, mostrando el detalle de cada reserva mediante polimorfismo.
  - La capa de presentación debe comunicarse con la lógica de negocio a través de interfaces o abstracciones.

5. **Lógica de Aplicación**
  - Implementa un servicio (por ejemplo, `ReservaService`) que gestione la creación, almacenamiento (en memoria) y consulta de reservas.
  - Este servicio debe depender de una interfaz de repositorio (por ejemplo, `IReservaRepository`), permitiendo cambiar la implementación del almacenamiento sin afectar la lógica de negocio. Es decir, debéis aplicar el ppio DIP e inyectar en esta clase `ReservaService` un repositorio a través de la abstracción `IReservaRepository`.

#### **Objetivos del Ejercicio**

- Demostrar la comprensión de los fundamentos de la Programación Orientada a Objetos mediante la instanciación y uso de objetos.
- Aplicar conceptos avanzados de POO como herencia, clases abstractas e interfaces.
- Crear y utilizar clases que hagan uso de genéricos.
- Aplicar principios SOLID, especialmente la inversión de dependencias.
- Emplear expresiones regulares para la validación de entradas.
- Integrar y utilizar librerías externas para extender la funcionalidad del proyecto.
- Documentar y presentar el código de manera clara y comprensible.

#### **Trabajo a Realizar**

1. **Definición de Clases y Estructura del Proyecto**
  - Organiza el proyecto en paquetes (o módulos) que representen cada capa:
    - `presentacion` para la interfaz de usuario.
    - `servicios` (o `aplicacion`) para la lógica de negocio.
    - `datos` para la implementación del repositorio (en memoria).
    - `dominio` para definir las clases **Reserva**, **Reserva de Vuelo** y **Reserva de Hotel**.

2. **Implementación del Modelo de Dominio**
  - Define la superclase o interfaz `Reserva` que incluya:
    - Las propiedades comunes (`id`, `fechaCreacion`, `descripcion` y `detalle`).
    - La lógica compartida que consideres necesaria.
  - Implementa las clases `Reserva de Vuelo` y `Reserva de Hotel` siguiendo las especificaciones:
    - Campos inmutables (por ejemplo, `id` y `fechaCreacion` generados automáticamente).
    - Las propiedades específicas de cada una (`origen`, `destino`, `horaVuelo`) y (`ubicacion`, `numeroNoches`)
    - Constructores privados con el método `creaInstancia` en el *companion object*.
    - Propiedad `detalle` que concatene la información de forma dinámica.

3. **Desarrollo de la Lógica de Aplicación**
  - Implementa un servicio (`ReservaService`) que:
    - Utilice una interfaz de repositorio (`IReservaRepository`) para almacenar y recuperar reservas (`agregar` y `obtenerTodas`).
    - Permita la creación de nuevas reservas mediante métodos que invoquen `creaInstancia` de cada clase.
  - Aplica el principio de inversión de dependencias, de modo que el servicio dependa de la abstracción, no de una implementación concreta.

4. **Interfaz de Usuario (Consola)**
  - Desarrolla una interfaz de usuario en consola que muestre un menú con las siguientes opciones:
    - **Opción 1:** Crear nueva reserva (se debe preguntar al usuario si desea crear una Reserva de Vuelo o de Hotel, y solicitar los datos requeridos).
    - **Opción 2:** Listar todas las reservas registradas, mostrando el detalle (id y descripción) de cada reserva.
  - La capa de presentación debe comunicarse con el servicio para realizar las operaciones solicitadas.

5. **Documentación y Pruebas**
  - Comenta el código de forma clara, explicando las decisiones de diseño y la aplicación de los principios SOLID.
  - Realiza pruebas y depura la aplicación para asegurar su correcto funcionamiento.
