# API de productos con Typescript

<img src="./images/typescript-logo.png" alt="typescript-logo" />

## Descripción

API con CRUD de productos desarollada con Typescript. Por lo tanto, este proyecto nos servirá como introducción al manejo de Typescript y más concretamente a su integración en el lado del backend.

## Introducción a typescript:

### Qué es

Typescript es un superset de Javascript. Decimos que una tecnología es un superset de otra, cuando puede ejecutar todas las funcionalidades de esta a pesar de que, como en este caso, sea un lenguaje de programación diferente. Esto significa que nuestro código de Javascript funcionará, por lo general, sin problemas dentro de Typescript.
Esto se debe a que Typescript está construído por encima de Javascript.

### Qué aporta

Javascript es un lenguaje de tipado dinámico. Esto quiere decir que las variables pueden cambiar el tipo de dato que albergan. El tipado dinámico nos permite trabajar de manera flexible pero, por contra, el código generado puede dar lugar a malos entendidos ya que no estamos seguros del tipo de dato que vamos a tener en cada variable.

Typescript aparece para solucionar este problema, permitiéndonos aportar tipado dinámico a Javascript. Esto permite que nuestro código tengo una mayor rigidez.

### Cómo empezar a utilizarlo

Typescript es un lenguaje compilado. Esto quiere decir que para poder utilizarlo vamos a necesitar que un compilador lo traduzca a código Javascript para que, o bien el navegador, o bien NodeJS, lo puedan interpretar correctamente.

Podemos encontrar la información necesaria para la instalación de Typescript y mucho más en la documentación oficial que se encuentra en el siguiente enlace: https://www.typescriptlang.org/download

En el caso de las distribuciones Linux, tendremos que utilizar npm ejecutando el comando:

```sh
npm install -g typescript
```

Una vez tengamos instalado el compilador, podremos ejecutarlo mediante el comando tsc seguido del nombre del archivo .ts que queramos compilar a javascript. Esto nos generará de manera automática un script de js resultado de dicha compilación.

### tsconfig

A pesar podemos compilar un archivo de Typescript de la manera que hemos explicado en el apartado anterior, la forma correcta de hacerlo es crear, dentro de nuestro proyecto, un archivo de configuración. Para ello, nos ubicaremos en la raíz del proyecto y ejecuremos el comando:

```sh
tsc --init
```

Este comando nos generará un archivo tsconfig.json en el que nos aparecerán multitud de opciones relativas al proceso de compilación de Typescript que podremos comentar, descomentar y editar.

A continuación, vamos a ver algunas de las opciones principales que nos ofrece el archivo tsconfig.json:

- target: Determina a qué versión de Javascript queremos compilar nuestro código de Typescript.

- rootDir: Indica en que directorio raíz se encuentran los archivos de Typescript.

- outDir: Marca en qué carpeta va a ser ubicado el código resultante del proceso de compilación.

### El tipo any

A los tipos nativos que ya existen en Javascript, Typescript añade algunos más. Uno de ellos es el tipo any. Este tipo permite asignar cualquier tipo de dato. No se recomienda su utilización salvo en casos muy justificados ya que anula el propósito fundamental de Typescript.
Si declaramos una variable como vamos a hacer en el ejemplo, podremos asignar y reasignar su valor con el tipo de dato que queramos.

```ts
let element: any;
```

### La inferencia de tipos

Cuando nosotros declaramos una variable en Typescript y no le asignamos un tipo de dato, se la asigna el del valor que le hayamos dado inicialmente debiendo respetarlo igual que en cualquier otro caso.

### Trabajar con objetos

A la hora de trabajar con objetos, mantendremos los mismos principios. Esto quiere decir que deberemos tipar las propiedades que el objeto contenga.
Si queremos definir un tipo de objeto que podamos reutilizar recurriremos al "type". Vamos a ver un ejemplo.
Supongamos que esperamos recibir un objeto de una base de datos con dos propiedades, una será "id" (el cual nos llegará como tipo number) y la otra "nombre" (la cual recibiremos como un tipo string). Este tipo lo vamos a defitir como "Usuario". La manera de definirlo sería la siguiente:

```ts
type Usuario = {
  id: number;
  name: string;
};
```

Una vez creado, ya podemos asignárselo a una variable en la que guardemos el resultado de una llamada a nuestra base de datos aunque también podríamos asignarlo introduciendo nosotros mismos los valores.

```ts
const primerUsuario: Usuario = {
  id: 1,
  name: "Manolo",
};
```

## Desarrollo de una api REST sencilla con NodeJS, Express y Typescript

Vamos a crear un código sencillo para ver cómo podríamos trabajar una api Rest con Typescript.

- Inicializar el repositorio: Para ello ejecutaremos el comando:

```sh
npm init -y
```

- Instalar Typescript en nuestro proyecto: Haremos la instalación de Typescript como dependencia de desarrollo con el comando:

```sh
npm i typescript -D
```

- Incluir la ejecución de Typescript en nuestro package.json: Lo incluiremos dentro de nuestros scripts.

```json
"scripts": {
  "tsc": "tsc"
},
```

- Creamos el tsconfig: Emplearemos el comando:

```sh
tcs --init
```

- Dentro del tsconfig.json le asignamos a la propiedad outDir el directorio en el que queremos que se deposite el código compilado:

```json
"outDir": "./dist"
```

- Instalamos Express: Para levantar nuestro servidor usaremos el framework ExpressJS y lo instalaremos con:

```sh
npm i express
```

- Creamos un archivo app.js y levantamos dentro nuestro servidor de Express.

```ts
import express from "express";

const app = express();

const port: number = 3000;

app.listen(port, () => {
  console.log(`Server listening on port: ${port}`);
});
```

Si la importación de Express nos da problemas de tipado debermos instalar el tipo correspondiente con el comando:

```sh
npm i @types/express
```

- Compilar el código: ejecutaremos el comando tsc.

```sh
tsc
```

- Arrancar el servidor: para arrancar nuestro servidor debemos de tener en cuenta que hay que ejecutar el archivo app.js (nuestro archivo de Javascript ya compilado). En este caso, le hemos indicado a Typescript que lo ubique en el directorio dist/, de modo que ejecutarmos el comando:

```sh
node dist/app.js
```

- Podemos incluir el comando de arranque el el package.json de la siguiente manera:

```json
"dev": "node dist/app.js"
```
