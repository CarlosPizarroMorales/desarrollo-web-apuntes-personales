# GLOBAL EXECUTION CONTEXT

*"Not inside a function"*

## REFERENCIAS:

* [Anthony Alicea on Udemy (*Understanding Javascript* lectura 10)][5]

<hr>

El contexto de ejecución global, es el contexto base en el que se ejecuta cualquier código en Javascript. Cuando quiera que se está ejecutando código Javascript, lo que está pasando en realidad es que uno o más [*entornos léxicos*][1] están siendo 'levantados' en la memoria del computador luego de ser analizados por el parser, luego interpretados o compilados, traducidos a lenguaje que el computador puede comprender. Estos *entornos léxicos* al momento de ejecutarse son 'envueltos' en un [*contexto de ejecución*][2] que es un espacio en memoria donde los valores y funciones que hemos programado en nuestro código viven y mueren. Y de nuevo, el *contexto de ejecución* básico sobre el que se ejecutan todos los demás, es el llamado "global".

Se llama "global" porque los identificadores que se crean en este contexto, son visibles y están disponibles desde cualquier otro. Y algo interesante que hace sin que el programador necesite indicarlo, es <mark>crear 2 objetos</mark> (el motor de Javascript es quien los crea en este contexto):

1. El *Objeto Global* (una colección de pares nombre/valor) 
2. El *Objeto this* (una variable especial)

También crea un objeto más, que en el caso *contexto global* está vacío, es el *outer environment* (entorno exterior). Además, en este contexto se ejecutan nuestros *entornos léxicos* por lo que finalmente, podemos ilustrarlo de esta manera:

![captura de entorno global][0]

Ahora podemos hacer un ejercicio simple:
* crear una carpeta con un archivo html completamente mínimo y un archivo con extensión js: 

```bash
myFolder/
 | index.html
 | app.js
```

* Ahora, dentro del archivo html:

```html
<html>
  <head></head>
  <body>
    <script src="app.js"></script>
  </body>
</html>
```

* Y dentro del archivo app.js: NADA. Exactamente nada por ahora.
* Ejecutamos el archivo con LiveServer u otro servidor y vamos a las herramientas de desarrollo, podemos escribir `this` o `window` y pese a que nuestro archivo de Javascript está vacío, vemos que estos objetos existen. Lo que pasó fue que en el momento en que ejecutamos nuestro archivo index.html y este invocó al archivo app.js, el motor de Javascript reconoció el entorno léxico y creo un contexto de ejecución para nuestro código, agregando el objeto global `window` (si estamos en el browser) y el objeto `this`: 

![global][3]

* A primera vista se puede observar que el objeto `this` y el objeto `window` devuelven el mismo objeto, y esto es así porque estamos posicionados en el contexto global, pero no será siempre igual. El objeto `window` por su parte, lo provee el motor de Javascript (V8 en Chromium-related) para establecer un canal de comunicación con todos las características y funciones que tiene la ventana de navegación, así como para contener el documento de cada ventana en un contexto de ejecución separado. 

* Si ahora, dentro del archivo app.js escribimos el siguiente código y volvemos a ejecutar nuestro index.html:

```javascript
var a = '¡Hola Mundo!';

function b() {
  // Por ahora no sirvo para nada
}
```

* Veremos al observar la consola en las herramientas de desarrollo, que nuestros identificadores, variable y función, pueden ser invocados por su nombre: 

![identificadores en global][4]

* Pero además, se observa otra cosa interesante, y es que tanto `a` como `b` han sido agregados como pares nombre/valor al objeto `window`, o sea el objeto *global*. Por lo tanto también pueden ser invocados con la siguiente sintaxis: `window.a` y `window.b`

## Por lo tanto: 

> Cuando una función o variable (un identificador) no está dentro de ninguna función (*scope*) está ubicada en el contexto global. 

[5]:https://www.udemy.com/course/understand-javascript
[4]:../assets/img/identifiers-in-global.png
[3]:../assets/img/global-this.png
[2]:../varios/execution-context.md
[1]:../varios/lexical-environment.md
[0]:../assets/img/global-execution-context.png