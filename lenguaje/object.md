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
