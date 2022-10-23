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


