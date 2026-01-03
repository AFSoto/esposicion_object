# Objetos en JavaScript - Guía Completa para Clase

## Tabla de Contenidos
1. [¿Qué es un objeto?](#qué-es-un-objeto)
2. [Sintaxis y Creación de Objetos](#sintaxis-y-creación-de-objetos)
3. [Acceder y Modificar Propiedades](#acceder-y-modificar-propiedades)
4. [Métodos en Objetos](#métodos-en-objetos)
5. [Objetos Anidados](#objetos-anidados)
6. [Arrays de Objetos](#arrays-de-objetos)
7. [Métodos Importantes de Object](#métodos-importantes-de-object)
8. [Desestructuración](#desestructuración)
9. [Spread Operator](#spread-operator)
10. [Conceptos Avanzados](#conceptos-avanzados)

---

## ¿Qué es un objeto?

Un **objeto** en JavaScript es una colección de propiedades relacionadas que representan una entidad. Es como un contenedor que agrupa información y funcionalidad.

### Sin objetos (problemático):
```javascript
let nombrePersona = "Carlos";
let edadPersona = 28;
let profesionPersona = "Desarrollador";
```

### Con objetos (organizado):
```javascript
let persona = {
  nombre: "Carlos",
  edad: 28,
  profesion: "Desarrollador"
};
```

**Concepto clave**: Un objeto es una colección de pares clave-valor donde cada propiedad tiene un nombre (clave) y un valor asociado.

---

## Sintaxis y Creación de Objetos

### 1. Notación Literal (más común)
```javascript
let producto = {
  nombre: "Laptop",
  precio: 1500,
  disponible: true
};
```

### 2. Constructor Object
```javascript
let producto = new Object();
producto.nombre = "Laptop";
producto.precio = 1500;
producto.disponible = true;
```

### 3. Object.create()
```javascript
let producto = Object.create(null);
producto.nombre = "Laptop";
producto.precio = 1500;
```

---

## Acceder y Modificar Propiedades

### Notación de Punto
```javascript
// Acceder
console.log(persona.nombre); // "Carlos"

// Modificar
persona.edad = 29;

// Agregar nueva propiedad
persona.ciudad = "Bogotá";
```

### Notación de Corchetes
```javascript
// Acceder con variable
let propiedad = "nombre";
console.log(persona[propiedad]); // "Carlos"

// Agregar propiedad
persona["apellido"] = "González";

// Propiedad con espacios
let obj = {
  "nombre completo": "Carlos González"
};
console.log(obj["nombre completo"]);
```

### ¿Cuándo usar corchetes?
- Cuando el nombre de la propiedad está en una variable
- Cuando el nombre tiene espacios o caracteres especiales
- Para construir propiedades dinámicamente en bucles

---

## Métodos en Objetos

Los objetos pueden tener funciones como propiedades, llamadas **métodos**.

### Sintaxis Tradicional
```javascript
let calculadora = {
  numero1: 10,
  numero2: 5,
  
  sumar: function() {
    return this.numero1 + this.numero2;
  },
  
  restar: function() {
    return this.numero1 - this.numero2;
  }
};

console.log(calculadora.sumar()); // 15
```

### Sintaxis Moderna (ES6)
```javascript
let calculadora = {
  numero1: 10,
  numero2: 5,
  
  sumar() {
    return this.numero1 + this.numero2;
  },
  
  restar() {
    return this.numero1 - this.numero2;
  }
};
```

### La palabra clave `this`
`this` se refiere al objeto actual. Es como decir "este objeto en el que estoy".
```javascript
let persona = {
  nombre: "Ana",
  edad: 25,
  
  saludar() {
    return `Hola, soy ${this.nombre} y tengo ${this.edad} años`;
  }
};

console.log(persona.saludar());
// "Hola, soy Ana y tengo 25 años"
```

---

## Objetos Anidados

Los objetos pueden contener otros objetos como propiedades.
```javascript
let estudiante = {
  nombre: "Ana",
  edad: 20,
  direccion: {
    calle: "Cra 7",
    numero: 123,
    ciudad: "Bogotá",
    pais: "Colombia"
  },
  calificaciones: {
    matematicas: 4.5,
    programacion: 5.0,
    ingles: 4.2
  }
};

// Acceder a propiedades anidadas
console.log(estudiante.direccion.ciudad); // "Bogotá"
console.log(estudiante.calificaciones.programacion); // 5.0

// Modificar propiedades anidadas
estudiante.direccion.ciudad = "Medellín";
```

---

## Arrays de Objetos

Una estructura muy común en aplicaciones reales.
```javascript
let estudiantes = [
  { nombre: "Ana", edad: 20, promedio: 4.2 },
  { nombre: "Luis", edad: 22, promedio: 3.8 },
  { nombre: "María", edad: 21, promedio: 4.7 },
  { nombre: "Pedro", edad: 19, promedio: 4.0 }
];

// Acceder a un estudiante específico
console.log(estudiantes[0].nombre); // "Ana"

// Recorrer con forEach
estudiantes.forEach(estudiante => {
  console.log(`${estudiante.nombre}: ${estudiante.promedio}`);
});

// Filtrar estudiantes
let destacados = estudiantes.filter(est => est.promedio > 4.0);

// Mapear para obtener solo nombres
let nombres = estudiantes.map(est => est.nombre);

// Encontrar un estudiante
let ana = estudiantes.find(est => est.nombre === "Ana");
```

---

## Métodos Importantes de Object

### Object.keys()
Retorna un array con las claves (nombres de propiedades).
```javascript
let persona = { nombre: "Carlos", edad: 28, ciudad: "Bogotá" };
let claves = Object.keys(persona);
console.log(claves); // ["nombre", "edad", "ciudad"]
```

### Object.values()
Retorna un array con los valores.
```javascript
let valores = Object.values(persona);
console.log(valores); // ["Carlos", 28, "Bogotá"]
```

### Object.entries()
Retorna un array de arrays con pares [clave, valor].
```javascript
let entradas = Object.entries(persona);
console.log(entradas);
// [["nombre", "Carlos"], ["edad", 28], ["ciudad", "Bogotá"]]

// Útil para iterar
Object.entries(persona).forEach(([clave, valor]) => {
  console.log(`${clave}: ${valor}`);
});
```

### Object.assign()
Copia propiedades de uno o más objetos a un objeto destino.
```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let obj3 = { e: 5 };

let combinado = Object.assign({}, obj1, obj2, obj3);
console.log(combinado); // { a: 1, b: 2, c: 3, d: 4, e: 5 }
```

### Object.freeze()
Congela un objeto, impidiendo modificaciones.
```javascript
let config = { apiUrl: "https://api.example.com" };
Object.freeze(config);

config.apiUrl = "otra-url"; // No tiene efecto
console.log(config.apiUrl); // "https://api.example.com"
```

### Object.seal()
Sella un objeto: puedes modificar propiedades existentes pero no agregar/eliminar.
```javascript
let persona = { nombre: "Carlos", edad: 28 };
Object.seal(persona);

persona.edad = 29; // Funciona
persona.ciudad = "Bogotá"; // No tiene efecto
delete persona.nombre; // No tiene efecto
```

---

## Desestructuración

Extraer propiedades de objetos de manera elegante.

### Desestructuración Básica
```javascript
let persona = { nombre: "Carlos", edad: 28, ciudad: "Bogotá" };

// Forma tradicional
let nombre = persona.nombre;
let edad = persona.edad;

// Con desestructuración
let { nombre, edad } = persona;
console.log(nombre); // "Carlos"
console.log(edad); // 28
```

### Renombrar Variables
```javascript
let { nombre: nombrePersona, edad: edadPersona } = persona;
console.log(nombrePersona); // "Carlos"
```

### Valores por Defecto
```javascript
let { nombre, edad, pais = "Colombia" } = persona;
console.log(pais); // "Colombia" (si no existe en el objeto)
```

### Desestructuración Anidada
```javascript
let estudiante = {
  nombre: "Ana",
  direccion: {
    ciudad: "Bogotá",
    pais: "Colombia"
  }
};

let { nombre, direccion: { ciudad } } = estudiante;
console.log(ciudad); // "Bogotá"
```

### En Parámetros de Función
```javascript
function mostrarPersona({ nombre, edad }) {
  console.log(`${nombre} tiene ${edad} años`);
}

mostrarPersona(persona); // "Carlos tiene 28 años"
```

---

## Spread Operator

El operador spread (...) permite expandir objetos.

### Copiar Objetos
```javascript
let persona = { nombre: "Carlos", edad: 28 };
let copia = { ...persona };

// Modificar la copia no afecta el original
copia.edad = 30;
console.log(persona.edad); // 28
```

### Combinar Objetos
```javascript
let info1 = { nombre: "Carlos", edad: 28 };
let info2 = { ciudad: "Bogotá", profesion: "Developer" };

let completo = { ...info1, ...info2 };
// { nombre: "Carlos", edad: 28, ciudad: "Bogotá", profesion: "Developer" }
```

### Agregar/Sobrescribir Propiedades
```javascript
let persona = { nombre: "Carlos", edad: 28 };
let empleado = { ...persona, puesto: "Developer", edad: 29 };
// { nombre: "Carlos", edad: 29, puesto: "Developer" }
// La edad se sobrescribe
```

---

## Conceptos Avanzados

### Comparación de Objetos
Los objetos se comparan por referencia, no por contenido.
```javascript
let obj1 = { a: 1 };
let obj2 = { a: 1 };
let obj3 = obj1;

console.log(obj1 === obj2); // false (diferentes referencias)
console.log(obj1 === obj3); // true (misma referencia)

// Para comparar contenido, usa JSON.stringify
console.log(JSON.stringify(obj1) === JSON.stringify(obj2)); // true
```

### Eliminar Propiedades
```javascript
let persona = { nombre: "Carlos", edad: 28, ciudad: "Bogotá" };
delete persona.edad;
console.log(persona); // { nombre: "Carlos", ciudad: "Bogotá" }
```

### Verificar si Existe una Propiedad
```javascript
let persona = { nombre: "Carlos", edad: 28 };

// Operador in
console.log("nombre" in persona); // true
console.log("apellido" in persona); // false

// hasOwnProperty
console.log(persona.hasOwnProperty("nombre")); // true
```

### Optional Chaining (?.)
Evita errores al acceder a propiedades que podrían no existir.
```javascript
let persona = {
  nombre: "Carlos",
  direccion: {
    ciudad: "Bogotá"
  }
};

// Sin optional chaining (puede dar error)
// console.log(persona.trabajo.empresa); // Error!

// Con optional chaining
console.log(persona.trabajo?.empresa); // undefined (sin error)
console.log(persona.direccion?.ciudad); // "Bogotá"
```

### Getters y Setters
```javascript
let persona = {
  nombre: "Carlos",
  apellido: "González",
  
  get nombreCompleto() {
    return `${this.nombre} ${this.apellido}`;
  },
  
  set nombreCompleto(valor) {
    [this.nombre, this.apellido] = valor.split(" ");
  }
};

console.log(persona.nombreCompleto); // "Carlos González"
persona.nombreCompleto = "Ana Martínez";
console.log(persona.nombre); // "Ana"
```

---

## Estructura de Clase (1 hora)

### Fase 1: Introducción (10 min)
- ¿Qué son los objetos y por qué son importantes?
- Ejemplos del mundo real
- Sintaxis básica

### Fase 2: Fundamentos (15 min)
- Crear objetos
- Acceder y modificar propiedades
- Notación de punto vs corchetes

### Fase 3: Características Avanzadas (15 min)
- Métodos y `this`
- Objetos anidados
- Arrays de objetos

### Fase 4: Herramientas Modernas (10 min)
- Métodos de Object
- Desestructuración
- Spread operator

### Fase 5: Ejercicios Prácticos (10 min)
- Presentar los 3 ejercicios
- Aclarar dudas

---

## Ejercicios Prácticos

### Ejercicio 1: Sistema de Biblioteca (Básico)

Crea un objeto `libro` con las siguientes propiedades:
- título
- autor
- año de publicación
- número de páginas
- disponible (boolean)

Luego agrega un método `descripcion()` que retorne un string con toda la información del libro en formato legible.

**Ejemplo de salida:**
```
"El libro 'Cien años de soledad' de Gabriel García Márquez, publicado en 1967, 
tiene 417 páginas y está disponible."
```

---

### Ejercicio 2: Carrito de Compras (Intermedio)

Crea un objeto `carritoCompras` que contenga:

**Propiedades:**
- `productos`: array de objetos, donde cada producto tiene nombre, precio y cantidad

**Métodos:**
- `agregarProducto(nombre, precio, cantidad)`: agrega un producto al carrito
- `calcularTotal()`: retorna el precio total (precio × cantidad de todos los productos)
- `aplicarDescuento(porcentaje)`: aplica un descuento al total y retorna el nuevo total
- `mostrarProductos()`: muestra en consola todos los productos del carrito

**Ejemplo de uso:**
```javascript
carritoCompras.agregarProducto("Laptop", 1500, 1);
carritoCompras.agregarProducto("Mouse", 25, 2);
console.log(carritoCompras.calcularTotal()); // 1550
console.log(carritoCompras.aplicarDescuento(10)); // 1395 (10% de descuento)
```

---

### Ejercicio 3: Sistema de Estudiantes (Avanzado)

Crea un array llamado `estudiantes` donde cada estudiante es un objeto con:
- nombre
- edad
- calificaciones (objeto con materias y notas)

**Implementa las siguientes funciones:**

1. `calcularPromedio(estudiante)`: retorna el promedio de calificaciones de un estudiante

2. `obtenerMejorEstudiante(estudiantes)`: retorna el estudiante con el mejor promedio

3. `estudiantesDestacados(estudiantes)`: retorna un array con los estudiantes mayores de edad (≥18) que tengan promedio superior a 4.0

4. `agregarCalificacion(estudiante, materia, nota)`: agrega una nueva calificación al estudiante

**Ejemplo de estructura:**
```javascript
let estudiantes = [
  {
    nombre: "Ana",
    edad: 20,
    calificaciones: {
      matematicas: 4.5,
      programacion: 5.0,
      ingles: 4.2
    }
  },
  // ... más estudiantes
];
```

---

## Preguntas Frecuentes

### ¿Cuál es la diferencia entre objetos y arrays?
- **Arrays**: colecciones ordenadas, se accede por índice numérico
- **Objetos**: colecciones de pares clave-valor, se accede por nombre de propiedad

### ¿Qué pasa si intento acceder a una propiedad que no existe?
Retorna `undefined`, no genera un error.

### ¿Puedo tener funciones dentro de objetos?
Sí, se llaman métodos y son muy comunes.

### ¿Los objetos son mutables?
Sí, puedes modificar sus propiedades incluso si están declarados con `const`. El `const` solo impide reasignar la variable, no modificar el contenido del objeto.

### ¿Cómo copio un objeto sin que se modifique el original?
Usa spread operator o `Object.assign()` para copias superficiales. Para copias profundas, usa `structuredClone()` o JSON parse/stringify.

---

## Recursos Adicionales

- [MDN Web Docs - Objetos](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Working_with_Objects)
- [JavaScript.info - Objetos](https://javascript.info/object)
- Practica en: [Exercism](https://exercism.org/tracks/javascript), [Codewars](https://www.codewars.com/)

---

**¡Éxito en tu clase! 🚀**
