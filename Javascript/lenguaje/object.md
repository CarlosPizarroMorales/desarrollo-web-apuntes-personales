# OBJECT 

Y...¿qué sería un objeto? Una definición concisa y fácil de retener que es además precisa respecto a Javascript sería: una colección de pares nombre/valor. Ok. Y...¿qué sería un par nombre/valor? Pues cualquier estructura en la que un nombre, una *palabra* es asignada con un valor. Lo importante de esto es que esta palabra puede ser definida muchas veces a través de distintos *entornos léxicos* pero solo puede existir con un único valor en el *contexto de ejecución* actual. [(A. Alicea *Understanding Javascript* lectura 8)][0]. Ejemplos generales de pares nombre valor pueden ser: 

```javascript
matricula = '123gwt'
nombre: 'Juanito Pedrito Gomez Argomedo'
```

Algo interesante de los valores de los objetos en Javascript, es que pueden contener a su vez otros pares nombre/valor. Por ejemplo, en el siguiente ejemplo, todo el bloque entre las líneas 1 y 7 forman el "valor" del primer nombre, pero a su vez son un objeto compuesto de pares nombre/valor, donde incluso el nombre "departamento" tiene como *valor* otro grupo de pares nombre/valor: 

```javascript
direccion: {

  calle: 'Principal',
  numero: 100,
  
  departamento: {

    piso: 3,
    numero: 301
  }

}
```


<hr>
<hr>

Lo que sigue abajo no se si debería ir en este lugar...

<hr>

## HOW TO...

### Iterate objects

- `for in` : **(before ES6)** Un detalle de este método es que <mark>itera a través de las propiedades del `prototype` del objeto</mark> y eso puede ser un efecto no deseado.

```javascript
for (const key in objectSample) {
  console.log(`${key}: ${user[key]}`);
}

// name: John Wooot
// email: blabla@bla.com
// ...
```

<hr>

- `Objects.keys()` : **(ES6)** devuelve un `array` de las claves del objeto que se le pasa en argumento.

```javascript
const keys = Object.keys(objectSample); // ['name', 'email', ...]

keys.forEach((key, index) => {
  console.log(`${key}: ${objectSample[key]}`);
})

// name: John Wooot
// email: blabla@bla.com
// ...
```

<hr>

- `Object.values()` : **(ES8)** retorna un `array` de todas los valores del objeto pasado en argumento.

```javascript
Object.values(objectSample).forEach(val => console.log(val)); 

// 'John Wooot'
// 'blabla@bla.com'
// ...
```

<hr>

- `Object.entries()` : **(ES8)** retorna un `array` de arrays. Cada subarray es un par `[key, value]` del objeto pasado en argumento.

```javascript
console.log(Object.entries(objectSample));

// ['name': 'John Wooot'],
// ['email': 'blabla@bla.com' ],
// [...],

// PARA ITERARLO, con for of, o forEach:

for (const [key, value] of Object.entries(objectSample)) {
  console.log(`${key}: ${value}`);
}

Object.entries(objectSample).forEach(([key, value]) => {
  console.log(`${key}: ${value}`); 
})
```



[0]:https://www.udemy.com/course/understand-javascript