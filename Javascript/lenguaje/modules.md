# Modules

1. [Introducción](#módulos-en-el-entorno-web-ejemplo-práctico) 
2. [Exportar módulos: `export`](#exportar-módulos) 
3. [Importar módulos: `import / from`](#importar-módulos) 
4. [Renombrar importados/exportados: `as`](#renombrar-identificadores) 
5. [Renombrar 'sin renombrar': uso de `*`](#renombrar-sin-renombrar) 

<hr>

## Módulos en el entorno web. (Ejemplo práctico)

Los módulos en Javascript, son archivos de código Javascript que pueden ser exportados e importados por otros archivos de Javascript. Esto permite crear código modular además de permitir al desarrollador ser más organizado y claro con la estructura de un proyecto.

Algunas tecnologías para realizar módulos antes de que se estandarizaran en ECMAScript son: 

1. [Asynchronous Module Definition (AMD)][1]
2. [CommonJS Modules][2]
3. [Universal Module Definition][3]

Luego en ES6 Javascript incorporó el concepto de módulos de forma nativa. [(Leer)][4]
  

> IMPORTANTE: 
> - por defecto, los módulos solo aceptan código bajo el modo estricto, sin importar si está presente la cláusula 'use strict' o no.
> - la palabra `export` solo funciona al principio del archivo (excepto cuando es una expresión al final), por lo que no se puede usar dentro de otros scopes que el global.
> - El motor de Javascript realiza hoisting de las sentencias incluidas en `export` por lo que se pueden definir en cualquier parte del código.

## EXPORTAR MÓDULOS

- Para utilizar módulos de Javascript en el desarrollo web, es necesario incluir el atributo `type="module"` en el elemento `script` que carga el archivo de Javascript, y una ventaja que es su carga es asincrónica por lo que no impactan en el rendimiento en la carga de la vista. No es necesario utilizar el atributo `defer` para obtener este comportamiento asíncrono. Un ejemplo en código:

```html
  <body>

    <!-- bla blá, bla blá -->
    <script type="module" src="module_1.js"></script>
  </body>
```

- Si se intenta ejecutar este archivo html mediante doble clic, al abrir la consola de las herramientas de desarrollo, se podrá observar el siguiente mensaje de error: 

![mensaje de error cors file protocol][5]

- Este mensaje indica en su cuerpo que los archivos con módulos de Javascript solo pueden ser ejecutados por el navegador si es bajo los protocolos indicados, entre ellos, http y https. Por lo tanto, siempre se debe utilizar un servidor local o remoto para su desarrollo. Otra manera de evitar el error es utilizar un *module bundler* para Javascript.

- Ahora que está todo listo, para un ejemplo práctico agregaré 1 módulo Javascript al `index.html`: 

```html
<script type="module" src="module_2.js"></script>
```

- Entonces comenzaremos con el código en los archivos Javascript. Para poder importar/exportar código en los módulos, existen palabras clave. Primero, la exportación se puede realizar a través de la palabra clave `export` ya sea al principio de todo el código, o bien con una sentencia `export` al final. 


- CASO 1 con la palabra reservada `export` al principio del módulo *¿o sección que se desea exportar?*: 

```javascript
export

const hiAgain = 'Hello World, earthling!';
const wot = (x) => `U pass me ${x} but I don't know WTF to do with it.`;
const arrFome = [1, 2, 3, {a:4, b:5, c:6}];
```

> AL PARECER, el CASO 1 solo exporta la primera sentencia.

<hr>

- CASO 2 con una sentencia `export` al final: 

```javascript
const hiAgain = 'Hello World, earthling!';
const wot = (x) => `U pass me ${x} but I don't know WTF to do with it.`;
const arrFome = [1, 2, 3, {a:4, b:5, c:6}];


export { hiAgain, wot, arrFome }; 
```

<hr>

## IMPORTAR MÓDULOS

> IMPORTANTE:
> - La palabra reservada `import` al igual que `export` solo puede ser utilizada en módulos. Dentro de un script general o de un elemento `<script></script>` por ejemplo, generará un error.
> - Los nombres importados no se levantan al entorno global. Solo quedan disponibles en el módulo que los levanta. (VENTAJA DE SEGURIDAD)
> - El motor de Javascript hará 'hoist' de los expresiones `import` por lo que se pueden escribir en cualquier punto de un programa.
> - Todo módulo, con `export/import` funciona solo bajo modo estricto. NO OLVIDAR.
> - Es obligatorio usar { } para envolver los identificadores importados.
> - Un módulo que 'importa' de otros módulos se considera un *'top-level module'* mientras que aquél que suministra código es llamado *'sub-module'*
> - Solo pueden ser importados, nombres que antes fueron exportados en otros módulos. El resto del scope queda fuera del alcance de `import`.
> - Los nombres importados en un módulo lo son solo en modo 'lectura' por lo que no es posible modificar su código.
> - Algunos entornos como Node y Webpack permiten omitir la extensión y `./` en la ruta del archivo pero por ejemplo en los módulos nativos esta práctica generará un error:

![error lazy path in modules][6]


## RENOMBRAR identificadores

- se pueden renombrar los nombres exportados tanto durante la exportación como la importación.
- La utilidad más inmediata es evitar colisiones de nombres.
- La palabra clave para lograrlo es `as`.
- Ejemplos:
  - `export { hiAgain as hiNoMore }` ahora el elemento definido en el módulo como `const hiAgain` debe ser importado en el destino como `hiNoMore`. 
  - `import { hiAgain as hiNoMore}` ahora el módulo destinatario del código debe invocar a `hiAgain` como `hiNoMore`.

## RENOMBRAR 'sin renombrar'

- Supongamos este código: 

```javascript
// bla bla bla...
// bla bla, mucho código
// ...

export { myConst, myVar, myFunc, myObj } 

// Lo anterior, se puede importar de esta manera 
// para renombrarlo, "sin renombrarlo": 

import * as objetoImportado from './module.js';

// esto crea el objeto 'objetoImportado', conteniendo 
// todos los valores exportados que pueden ser 
// invocados como propiedades y métodos del objeto:

objetoImportado.myFunc(args...);
const nuevaVar = objetoImportado.myConst;

console.log(objetoImportado.myVar);
```



[6]:../assets/img/module-error-lazy-relative-path.png
[5]:../assets/img/module-file-protocol-cors-error.png
[4]:https://tc39.es/ecma262/#sec-modules  
[3]:https://github.com/umdjs/umd
[2]:https://en.wikipedia.org/wiki/CommonJS
[1]:https://github.com/amdjs/amdjs-api/blob/master/AMD.md
[0]:https://www.freecodecamp.org/news/javascript-es-modules-and-module-bundlers/