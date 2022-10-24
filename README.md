# Patrones de diseño

## Listado de patrones

- [Patrones de diseño](#patrones-de-diseño)
  - [Listado de patrones](#listado-de-patrones)
  - [Elementos principales](#elementos-principales)
  - [Clasificación](#clasificación)
    - [Proposito](#proposito)
    - [Ambito](#ambito)
- [Patrones](#patrones)
  - [Patrón State](#patrón-state)
  - [Patrón Strategy](#patrón-strategy)
  - [Patrón Singleton](#patrón-singleton)
  - [Patrón Composite](#patrón-composite)
  - [Patrón Adapter](#patrón-adapter)
  - [Patrón Observer](#patrón-observer)
  - [Patrón Factory](#patrón-factory)
  - [Patrón Decorator](#patrón-decorator)
  - [Patrón Memento](#patrón-memento)

## Elementos principales
1. Nombre: Describe en pocas palabras un problema de diseño

2. Problema:
   1. Cuando se aplica
   2. Explica el problema y el contexto
   3. Verifica condiciones de aplicación

3. Solucion:
   1. Diseño, relaciones, responsabilidades y colaboraciones
   2. Es una plantilla que se puede aplicar en situaciones diferentes

4. Consecuencias:
   1. Resultados, ventajas e inconvenientes
   2. Costos y beneficios
   3. Impacto, flexibilidad, extensibilidad y portabilidad

## Clasificación
### Proposito
1. Creacion: Creacion de objetos
2. Estructural: Composicion de clases u objetos
3. Comportamiento: Interaccion, responsabilidad entre clases y objetos

### Ambito
1. Clase: Relaciones entre clases y subclases (Herencia), son relaciones estaticas (fijadas en tiempo de compilacion).
2. Objeto: Relaciones entre objetos, son relaciones dinamicas (pueden cambiar en tiempo de ejecucion).

|        |        |                      | Proposito                                                      |                                          |
|--------|--------|----------------------|----------------------------------------------------------------|------------------------------------------|
|        |        | Creacion             | Estructurales                                                  | Comportamiento                           |
| Ambito | Clase  | Factory              | Adapter (clases)                                               |                                          |
|        | Objeto | Builder<br>Singleton | Adapter (objetos)<br>Composite<br>Decorator<br>Facade<br>Proxy | Memento<br>Observer<br>State<br>Strategy |

# Patrones

## Patrón State
[Volver](#listado-de-patrones)

Modifica el comportamiento cada vez que cambia el estado interno. Crea un objeto por cada estado posible del objeto que lo llama.

<b>Problema</b>
- El comportamiento depende del estado del objeto
- Operaciones con muchas condiciones anidadas que dependen del estado del objeto

<b>Solución</b>

Se implementa una clase para cada estado diferente del objeto, y el desarrollo de cada metodo segun un estado determinado.
El objeto de la clase a la que le pertenece dichos estados resuelve los distintos comportamientos segun su estado, con instancias de dichas clases de estado. Asi, siempre tiene presente en un objeto ele stado actual y se comunica con este para resolver sus responsabilidades.

<b>Implementación</b>
- Las transiciones de cambio de estado pueden hacerlas:
  - La subclase: teniendo una referencia del estado que le precede y cuando.
  - Contexto: tras la solicitud del cliente.
- Definiendo una tabla de transicion de estado. Esto permite cambiar los criterios de transicion mediante modificacion de datos, en lugar de código.
- Creación/Destrucción de objetos estado:
  - Crear el objeto cuando es necesario, utilizarlo y destruirlo. (Nunca se sabe que estado toma el objeto en runtime).
  - Crear todos los objetos estado de antemano, utilizar alguno y nunca destruirlos. (Cambios rapidos de estado).
  
  ![image](https://user-images.githubusercontent.com/5508796/197398184-0e3e9c55-47e0-4776-8035-083f84eb2295.png)

<b>Ventajas y desventajas</b>
- Ventajas:
  - Se localizan facilmente las responsabilidades de los estados especificos
  - Hace los cambios de estado explicitos
  - Los objetos State pueden ser compartidos (si no contienen variables de instancia)
  - Facilita ampliacion de estados
  - Permite a un objeto cambiar de clase en el runtime
- Desventajas:
  - Incrementa el numero de subclases

<b>Relación con otros patrones</b>
  
El patron `State` puede ser considerado una extensión del `Strategy`. Ambos patrones estan basados en composicion: Pueden cambiar el comportamiento del contexto delegando parte del trabajo a subclases. Mientras que el `Strategy` convierte objetos en estructuras completamente independientes del contexto, `State` permite a estos objetos alterar el estado del contexto si lo necesitan.

## Patrón Strategy
[Volver](#listado-de-patrones)

Define una familia de algoritmos, encapsula cada uno de llos y los hace intercambiables.

<b>Problema</b>
- Necesidad de implementar varios algoritmos complejos
- Emplear distintos algoritmos apropiados en distintos momentos
- Dificultad en agregar nuevos algoritmos o modificar existentes

Cualquier programa que ofrezca una funcion o servicio, que puede ser realizado de varias maneras, es candidato a este patron.

<b>Solución</b>

Aplicar el patron a una clase que defina multiples comportamientos mediante instrucciones condicionales, evitando de esta forma emplear estas instrucciones, moviendo el codigo a clases independientes donde se almacenaran cada estrategia.

<b>Implementación</b>

Entre las posibilidades disponibles se encuentran:
- Pasar como parametro la información necesaria para la estrategia (bajo acoplamiento).
- Pasar como parametro el contexto y dejar que la estrategia solicite la informacion que necesita (alto acoplamiento).
- Matener dentro de la estrategia una referencia al contexto (alto acoplamiento).

![image](https://refactoring.guru/images/patterns/diagrams/strategy/solution.png)

<b>Ventajas y desventajas</b>

- Ventajas
  - La herencia puede ayudar a factorizar las partes comunes de las familias de algoritmos.
  - Proporciona una alternativa a la extension de contextos, ya que puede realizarse un cambio dinamico de estrategia.
- Desventajas
  - El cliente debe conocer las diferentes estrategias, y debe comprender las posibilidades que ofrecen.
  - Aumenta el numero de objetos creados

<b>Relación con otros patrones</b>

- El patron `Decorator` permite cambiarle la "piel" al objeto, mientras que el patron `Strategy` permite cambiarle las "tripas.

## Patrón Singleton
[Volver](#listado-de-patrones)

Garantiza que una clase solo tenga una instancia, y proporciona un punto de acceso global a ella.

<b>Problema</b>
- Necesidad de asegurar que solo exista un objeto gestor
- Necesidad de implementar un patron que permita controlar o restringir las situaciones que exigen la creacion y el control de acceso a la instancia privilegiada para la tarea.

<b>Solución</b>

Todas las implementaciones de esta patron recaen en los mismos dos pasos en comun:
- Convertir el constructor por defecto en privado, para prevenir que otros objetos puedan instanciar con `new` a la clase Singleton.
- Crear un metodo estatico que actue como el constructor de la clase. Este metodo estatico verificara si existe creada una instancia del objeto, de ser asi devuelve dicha instancia. De lo contrario, este metodo creara una instancia de la clase Singleton para luego retornarla.

<b>Implementación</b>
- Definir una funcion estatica en la clase Singleton.
- Esta operacion debe contener acceso a la instancia de la clase, y asegurarse de que dicha variable este inicializada antes de devolver su valor.
- Los clientes solo pueden acceder a dicha instancia a traves de esta clase estatica.
- No se crea y se almacena hasta que se accede a la variable por primera vez (lazy-load).
- El constructor debe estar definido como `protected` o `private`.

![image](https://refactoring.guru/images/patterns/diagrams/singleton/structure-en.png)

<b>Ventajas y desventajas</b>
- Ventajas:
  - Acceso unico desde cualquier parte de la aplicacion y control de la instancia creada.
  - Lazy Load (se crea la instancia solo cuando es requerida).
- Desventajas:
  - Su implementación se pierde dentro del sistema. Para mitigar esto se sugiere agregarle la palabra "Singleton" delante de su nombre.
  - Puede traer complicaciones en sistema multi hilo (bloqueos, dead-locks)
  - Puede traer problemas de descendencia, si se hereda de un objeto singleton.
  - Controles adicionales haran mas complejo la implementación.

<b>Relación con otros patrones</b>
- Una clase `Facade` puede ser transformada en un `Singleton` dado a que un solo objeto `Facade` es suficiente en la mayoria de los casos.

## Patrón Composite
[Volver](#listado-de-patrones)

Permite que los clientes traten de manera uniforme a los objetos individuales y a los compuestos.

<b>Problema</b>

Se presentan escenarios en los cuales existen objetos y contenedores de estos objetos en los cuales se puede requerir la invocacion de los mismos metodos o la ejecucion de las mismas responsabilidades.

<b>Solución</b>

Diseñar una estructura que permita ser usada de forma simple o compuesta de la misma manera, usando un mecanismo recursivo para que los clientes no tengan que saber de que estan compuestos.

<b>Implementación</b>
- Definir una interfaz comun para los objetos de la composicion y proveer una interfaz para gestionar los hijos. Dicha interfaz implementa el comportamiento por defecto comun a todas las subclases.
- Definir un objeto simple de la composicion que defina el comportamiento primitivo.
- Definir el objeto complejo, que almacenara a los componentes hijos.

<img width="931" alt="image" src="https://user-images.githubusercontent.com/5508796/197421772-96261315-7b14-4e1f-845b-7c9310d9f937.png">

<b>Ventajas y desventajas</b>
- Ventajas
  - Permite representar una jerarquia de objetos
  - Principio `Open/Closed`. Permite introducir nuevos elementos en la aplicacion sin romper el codigo existente.
- Desventajas
  - Puede resultar dificultoso proveer una interfaz comun para clases cuya funcionalidad difiere demasiado.
  
<b>Relación con otros patrones</b>
- Se puede utilizar el patron `Builder` para crear arboles `Composite` complejos.
- `Composite` y `Decorator` tienen diagramas de estructura similares ya que ambos se basan en la composición recursiva para organizar un número indefinido de objetos.
  - Un Decorator es como un Composite pero sólo tiene un componente hijo. Hay otra diferencia importante: Decorator añade responsabilidades adicionales al objeto envuelto, mientras que Composite se limita a “recapitular” los resultados de sus hijos.
  - No obstante, los patrones también pueden colaborar: puedes utilizar el Decorator para extender el comportamiento de un objeto específico del árbol Composite.

## Patrón Adapter
[Volver](#listado-de-patrones)

Convierte la interfaz de una clase en otra interfaz que espera el cliente. Permite que clases trabajen juntas que de otra manera no podrían por no tener la misma interfaz.

<b>Problema</b>

Se presentan escenarios en los cuales se requiere que dos clases trabajen juntas pero no pueden por no tener la misma interfaz.

<b>Solución</b>

Se logra adaptando la clase necesaria mediante una del dominio, que se encargara de adaptar el funcionamiento.

<b>Implementación</b>
- Definir una interfaz del dominio que usa el Cliente.
- Definir una interfaz existente que necesita adaptarse.
- Crear una clase adaptadora que implemente la interfaz del dominio y contenga una instancia de la interfaz existente.
- El cliente usara la interfaz del dominio para interactuar con la clase adaptadora.

![image](https://refactoring.guru/images/patterns/diagrams/adapter/structure-object-adapter-indexed-2x.png)

<b>Ventajas y desventajas</b>
- Ventajas:
  - Principio de responsabilidad unica: se separa la interfaz del cliente de la interfaz del servicio.
  - Principio abierto/cerrado: se puede agregar nuevos servicios sin modificar el cliente.
- Desventajas:
  - Aumenta la complejidad del sistema. En ocasiones es mas sencillo crear una nueva clase que implemente la interfaz requerida.

<b>Relación con otros patrones</b>
- `Facade` define una nueva interfaz para objetos existentes, mientras que `Adapter` intenta hacer que la interfaz existente sea utilizable. Normalmente `Adapter` sólo envuelve un objeto, mientras que `Facade` trabaja con todo un subsistema de objetos.
- `Adapter` proporciona una interfaz diferente al objeto envuelto, `Proxy` le proporciona la misma interfaz y `Decorator` le proporciona una interfaz mejorada.
- `Adapter` cambia la interfaz de un objeto existente mientras que `Decorator` mejora un objeto sin cambiar su interfaz. Además, `Decorator` soporta la composición recursiva, lo cual no es posible al utilizar `Adapter`.

## Patrón Observer
[Volver](#listado-de-patrones)

Define una dependencia de uno a muchos entre objetos de manera que cuando un objeto cambia de estado, todos sus dependientes son notificados y actualizados automáticamente.

<b>Problema</b>

Se necesita consistencia entre clases relacionadas, pero con un bajo acoplamiento.

<b>Solución</b>

Se define una dependencia uno a muchos entre objetos, de tal forma que cuando un objeto cambia de estado, todos sus dependientes son notificados y actualizados automáticamente. Se utiliza un mecanismo de publicación/inscripción para notificar a los observadores.

<b>Implementación</b>
- Definir una clase `Subject` que mantiene una lista de sus dependientes, llamados `Observers`, y provee un mecanismo para añadir o eliminar dependientes.
- Definir una interfaz `Observer` que declara un método de actualización que es llamado por el `Subject`.
- Definir una clase `ConcreteSubject` que extiende la clase `Subject` y notifica a sus dependientes cuando cambia su estado.
- Definir una clase `ConcreteObserver` que implementa la interfaz `Observer` y mantiene una referencia a un objeto `ConcreteSubject` concreto.

<b>Modelo push:</b> el sujeto envia a los observadores información sobre los cambios. </br>
<b>Modelo pull:</b> los observadores solicitan información al sujeto explicitamente.

![image](https://user-images.githubusercontent.com/5508796/197629669-a3513d78-64f6-4eea-bb22-fc949c8ad9e6.png)

<b>Ventajas y desventajas</b>
- Ventajas:
  - Se pueden establecer relaciones entre objetos en tiempo de ejecución.
  - Principio abierto/cerrado: se puede agregar nuevos servicios sin modificar el cliente.
- Desventajas:
  - Los suscriptores pueden ser notificados en cualquier orden.

## Patrón Factory
[Volver](#listado-de-patrones)

Define una interfaz para crear un objeto, pero deja a las subclases decidir que clase instanciar. Permite que una clase delegue la creación de objetos a sus subclases.

<b>Problema</b>

Cuando un objeto debe crear una instancia y solo conoce una clase abstracta y no sabe definir que subclase instanciar.

<b>Solución</b>

Facilitar la creación de objetos sin especificar la clase concreta que se va a instanciar, delegando esta responsabilidad a las subclases.

<b>Implementación</b>

Existen dos variantes principales de la clase `Creator`:
- `Concreta`: El creador es una clase concreta y proporciona una implementacion predeterminada del metodo de fabricacion. (Es posible tener una clase abstracta, que defina una implementacion predeterminada del metodo de fabricacion, y que las subclases puedan sobreescribirlo si es necesario).
- `Abstracta`: No proporciona implementacion predeterminada del metodo de fabricacion. Debe ser sobreescribido por las subclases.

![image](https://user-images.githubusercontent.com/5508796/197632381-ff3dec30-35fe-4dad-b1e7-b328c6fc1fae.png)

Metodos de fabricacion parametrizados:
- El metodo de fabricacion puede recibir parametros que determinen el tipo de objeto a crear.
- Permite crear objetos de diferentes tipos, pero con una interfaz común.

<b>Ventajas y desventajas</b>
- Ventajas:
  - Evitar el acoplamiento entre el cliente y las clases concretas.
  - Principio de responsabilidad unica: se separa la creacion de objetos de su uso.
  - Principio abierto/cerrado: se puede agregar nuevos productos sin modificar el cliente.
- Desventajas:
  - El codigo puede volverse mas complejo al agregar nuevas subclases.

<b>Relación con otros patrones</b>
- `Factory` es parecido a `Builder` en que ambos encapsulan la creacion de objetos, pero `Factory` se enfoca en la creacion de objetos complejos, mientras que `Builder` se enfoca en la creacion de objetos complejos paso a paso.

## Patrón Decorator
[Volver](#listado-de-patrones)

Asigna responsabilidades adicionales a un objeto dinamicamente. Ofrece una alternativa flexible a la herencia para extender la funcionalidad.

<b>Problema</b>

A veces se quiere añadir responsabilidades a objetos individuales en vez de a toda una clase.

<b>Solución</b>

Se encierra al componente en otro objeto que añade las responsabilidades deseadas. Este objeto se llama `Decorator`. El decorador se ajusta a la interfaz del componente que decora. El decorador reenvia las peticiones al componente y puede realizar acciones adicionales antes o despues del reenvio.

<b>Implementación</b>
- Se define una interfaz para los objetos que se pueden decorar.
- Se define un objeto al que se le pueden añadir responsabilidades.
- Se crea un `Decorator` que mantiene una referencia al objeto que se va a decorar, define una interfaz que se ajusta a la interfaz del componente.
  
<b>Ventajas y desventajas</b>
- Ventajas:
  - Se pueden añadir responsabilidades a objetos individuales en tiempo de ejecución.
  - Se pueden combinar varias responsabilidades.
  - Se puede eliminar responsabilidades en tiempo de ejecución.
  - Principio de responsabilidad unica: se separa la responsabilidad de la creacion de la responsabilidad de la extension.
- Desventajas:
  - El codigo puede volverse mas complejo al añadir nuevas responsabilidades.

<b>Relación con otros patrones</b>
- `Adapter` cambia la interfaz de un objeto, mientras que `Decorator` añade responsabilidades sin cambiar su interfaz.
- `Adapter` proporciona una interfaz diferente a la que tiene el objeto, mientras que `Proxy` proporciona la misma interfaz que el objeto y `Decorator` proporciona una interfaz mejorada.
- `Composite` y `Decorator` tienen estructuras similares, pero tienen diferentes propósitos. `Composite` se usa para representar jerarquias de objetos, mientras que `Decorator` se usa para añadir responsabilidades a objetos individuales.

## Patrón Memento
[Volver](#listado-de-patrones)

Permite guardar y restaurar el estado previo de un objeto sin revelar los detalles de su implementación.

<b>Problema</b>

Muchas veces es necesario almacenar el estado interno de un objeto para poder restaurarlo en un momento posterior.

<b>Solución</b>

`Memento` implementa un objeto llamado memento que almacena una instantanea del estado interno de otro objeto. Solo el creador puede almacenar y restaurar el estado del memento.

<b>Implementación</b>

<b>Ventajas y desventajas</b>
- Ventajas:
  - Se pueden producir instantanead del estado del objeto sin violar el encapsulamiento.
  - Puede simplificar el codigo de la originadora, permitiendo que la cuidadora mantenga el historial de estados.
- Desventajas:
  - Consumo de memoria adicional.
  - Las cuidadoras deben rastrear el ciclo de vida de los mementos.
