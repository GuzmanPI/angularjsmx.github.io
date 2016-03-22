---
layout: post
permalink: /blog/primer-proyecto-angular2/
title: "Como Crear Tu Primer Proyecto de Angular 2"
date:   2016-03-22 09:00:00
categories: [angular2, post]
author: israelgp4
description: Veremos como crear paso a paso un proyecto de Angular 2
---

**Requisito:** Instalar [node y npm](https://nodejs.org/en/download/) en caso de no tenerlos ya instalados.

Lo primero que debemos hacer para crear nuestra primera aplicación, es crear una carpeta on el nombre de nuestro proyecto. Yo la llamareé **Angular2**.

Dentro de la carpeta **Angular2** crearemos los siguientes archivos *json*:

* **tsconfig.json** que sirve de guía para el compilador de Typescript
* **typings.json** que identifica archivos de definición de TypeScript faltantes
* **package.json** que define los paquetes y scripts que necesitamos

Dentro del archivo **tsconfig.json** copia y pega lo siguiente:

{% highlight javascript %}
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
  ]
}
{% endhighlight %}

El archivo **tsconfig.json** guía al compilador de TypeScript.

Dentro del archivo **typings.json** copia/pega lo siguiente:

{% highlight javascript %}
{
  "ambientDependencies": {
    "es6-shim": "github:DefinitelyTyped/DefinitelyTyped/es6-shim/es6-shim.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd",
    "jasmine": "github:DefinitelyTyped/DefinitelyTyped/jasmine/jasmine.d.ts#7de6c3dd94feaeb21f20054b9f30d5dabc5efabd"
  }
}
{% endhighlight %}

Existen librerías que amplían la funcionalidad y sintaxis de JavaScript que el compilador de TypeScript no reconoce nativamente. Le podemos enseñar a Typescript estas funcionalidades por medio de archivos de definición, en nuestro caso en el archivo **typings.json**.

Dentro del archivo **package.json** copia/pega lo siguiente:

{% highlight javascript %}
{
  "name": "angular2-quickstart",
  "version": "1.0.0",
  "scripts": {
    "start": "concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "lite": "lite-server",
    "typings": "typings",
    "postinstall": "typings install"
  },
  "license": "ISC",
  "dependencies": {
    "angular2": "2.0.0-beta.11",
    "systemjs": "0.19.24",
    "es6-promise": "^3.0.2",
    "es6-shim": "^0.35.0",
    "reflect-metadata": "0.1.2",
    "rxjs": "5.0.0-beta.2",
    "zone.js": "0.6.4"
  },
  "devDependencies": {
    "concurrently": "^2.0.0",
    "lite-server": "^2.1.0",
    "typescript": "^1.8.9",
    "typings":"^0.7.9"
  }
}
{% endhighlight %}

Las librerías que requiere nuestra aplicación dependen del administrador de paquetes [npm](https://docs.npmjs.com/) para poder instalarlas. El equipo de de Angular recomienda este set inicial de paquetes especificados en las secciones *dependencies* y *devDependencies* del archivo **package.json**. Ahora, debemos instalar estos paquetes con el comando: **npm install**. Ahora ejecutamos el comando **npm run typings** para correr la herramienta de *typings*.

**Estamos listos.** Ya podemos crear los dos componentes que explicamos en el blog anterior **[Intro a Angular 2](http://angularmexico.com/blog/intro-angular2/)**.

Lo primero que debemos hacer es crear una carpeta que se llame **app** dentro de la carpeta **Angular2**. Dentro de la carpeta **app** creamos los siguentes archivos:

* **main.ts**
* **saludo.component.ts**

Dentro del archivo **main.ts** copia/pega lo siguiente:

{% highlight javascript %}
import {bootstrap} from 'angular2/platform/browser';
import {Saludo} from './saludo.component';

bootstrap(Saludo);
{% endhighlight %}

Dentro del archivo **saludo.component.ts** copia/pega lo siguiente:

{% highlight javascript %}
import {Component} from 'angular2/core';

@Component({
    selector: 'saludo',
    template: '<p>Hola { { nombre } }!</p>'
})
export class Saludo {
    nombre: string;

    constructor() {
        this.nombre = 'Israel';
    }
}
{% endhighlight %}

Ahora creamos nuestro archivo **index.html** a la altura de la carpeta **app**.

Así es como queda la estructura de carpetas/archivos de nuestra aplicación:

```
app/                    --> Código fuente de nuestra aplicación
  main.ts                 --> Arranque de nuestra aplicación (bootstrap)
  saludo.component.ts     --> Componente de Angular 2
node_modules/           --> Paquetes que necesitamos para utilizar Angular 2
  ...
index.html              --> Archivo HTML principal de nuestra aplicación
package.json            --> Archivo de configuración de paquetes
tsconfig.json           --> Archivo de configuración de Typescript
typings.json            --> Archivo de definición de faltantes en Typescript
```

Ahora, dentro del archivo **index.html** copia/pega lo siguiente:

{% highlight html %}
<html>
<head>
  <title>Angular 2</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="styles.css">

  <!-- 1. Cargamos nuestras librerías -->
  <!-- IE requiere polyfills, en este exacto orden -->
  <script src="node_modules/es6-shim/es6-shim.min.js"></script>
  <script src="node_modules/systemjs/dist/system-polyfills.js"></script>
  <script src="node_modules/angular2/es6/dev/src/testing/shims_for_IE.js"></script>
  <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
  <script src="node_modules/systemjs/dist/system.src.js"></script>
  <script src="node_modules/rxjs/bundles/Rx.js"></script>
  <script src="node_modules/angular2/bundles/angular2.dev.js"></script>

  <!-- 2. Configuramos SystemJS -->
  <script>
    System.config({
      packages: {
        app: {
          format: 'register',
          defaultExtension: 'js'
        }
      }
    });
    System.import('app/main')
        .then(null, console.error.bind(console));
  </script>
</head>

<body>

<!-- 3. Desplegamos la aplicación -->
<saludo>Cargando aplicación...</saludo>
</body>
</html>
{% endhighlight %}

El *scrypt* de configuración de SystemJS importa nuestro componente principal de aplicación "**Saludo**".

Para correr la aplicación:

1. Iniciamos el compilador de Typescript con el comando **npm run tsc:w**. La bandera **w** (*watch*) le indica al compilador que escuche a cambios en nuestros archivos *.ts* para recompilar los cambios de manera automática.

2. Iniciamos nuestra aplicacion con el comando **npm start**

En el próximo post veremos funcionalidad del del core de Angular 2.







