# Execution context

Un envoltorio que ayuda a administrar el código que está siendo ejecutado. [(A. Alicea Understanding Javascript lectura 7)][0]. En un solo archivo de código, incluso en una sección de él, puede haber muchos *entornos léxicos* que determinan los *scopes* de los identificadores como funciones o variables. Cuál de ellos se está ejecutando en el momento actual es algo que se administra a través de los *contextos de ejecución*. Puede contener elementos más allá de aquellos escritos en el código aportados por el compilador o intérprete por ejemplo. 

## 1° phase: Creation and 'Hoisting'

* [(A. Alicea Understanding Javascript lectura 11][0].

![captura de pantalla][1]

Cuando nuestro código de ejecuta en el browser, el motor de Javascript pasa por 2 fases durante la creación del *execution context*, la creación y el *hoisting*. Considera el siguiente código: 

```javascript
b();              // 'Hello again!'
console.log(a);   // undefined

var a = '¡Hola Mundo!';

function b() {
  console.log('Hello again!');
}
```


En muchos lenguajes de programación este comportamiento simplemente dará un error, debido a que estamos invocando identificadores que aún no han sido creados. Sin embargo en Javascript no se provoca ningún error porque el *contexto de ejecución*  se crea en dos fases, y durante la primera, llamada '<mark>creación</mark>' se crean el *Global object*, además de el objeto *this*, el *Outer environment*, pero además durante esta fase, el parser recorre el código reconociendo dónde se han creado variables y dónde se han creado funciones, y en este punto configura espacio en memoria para estas variables y/o funciones. A este proceso se le suele llamar '*hoisting*'.  

No se trata realmente de que el código está siendo 'levantado' al tope de su *scope*, o entorno léxico, sino simplemente que incluso antes de ser ejecutado, el motor de Javascript ya ha reconocido las variables y funciones en el código y les ha asignado un espacio en memoria. Es por eso que la segunda línea del ejemplo de código anterior devuelve un `undefined`. En el momento de asignarle un espacio en memoria, todas las variables tienen asignado un *placeholder* que es siempre el valor primitivo `undefined`. En el caso de las funciones, estas son alocadas con todo su cuerpo.  

Por todo lo anterior, cuando la ejecución del código comienza, las variables y funciones ya existen en memoria, por lo que invocarlas no provoca error, aunque en el caso de las variables, estas aún no han pasado por la ejecución del operador de asignación, lo que resulta en que obtenemos el valor `undefined`. 

## 2° phase: Execution phase

* [(A. Alicea Understanding Javascript lectura 13][0].

![captura de pantalla][2]

Entonces, ya se ha configurado el contexto de ejecución y se han asignado espacios de memoria para todos los identificadores como variables y funciones. Por lo tanto, ahora se ejecuta el código, línea por línea. 



[2]:../assets/img/execution-context-execution-phase.png
[1]:../assets/img/execution-context-creation-phase.png
[0]:https://www.udemy.com/course/understand-javascript/

