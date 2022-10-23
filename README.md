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

<b>Ventajas y desventajas</b>

- Ventajas
  - La herencia puede ayudar a factorizar las partes comunes de las familias de algoritmos.
  - Proporciona una alternativa a la extension de contextos, ya que puede realizarse un cambio dinamico de estrategia.
- Desventajas
  - El cliente debe conocer las diferentes estrategias, y debe comprender las posibilidades que ofrecen.
  - Aumenta el numero de objetos creados

<b>Relación con otros patrones</b>

- El patron `Decorator` permite cambiarle la "piel" al objeto, mientras que el patron `Strategy` permite cambiarle las "tripas.
