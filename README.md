# Patrones de diseño

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

