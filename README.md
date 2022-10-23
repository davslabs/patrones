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
