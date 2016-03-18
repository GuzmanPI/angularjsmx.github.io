---
layout: post
permalink: /blog/intro-angular2/
title: "Intro a Angular 2"
date:   2016-03-18 10:00:00
categories: [angular2, post]
author: israelgp4
description: Angular 2 es más simple que Angular 1. Pero, que sea simple no significa que es menos poderoso, sino todo lo contrario
---

[Angular 2](https://angular.io/features.html) es 80% más rápido que la v1, ya que calcula los cambios en los datos y no en el DOM. Tambien soporta varios lenguajes como JavaScript 5 y 6, [TypeScript](http://www.typescriptlang.org/) y [Dart](https://www.dartlang.org/). **ng-repeat** los valores que existen en un conjunto de objetos, está vez nos referiremos a la habilidad que tiene Angular de renderear una variable en el DOM en el formato que necesitamos.

El paradigma vista/controlador de la v1 ya no existe y ahora todo en Angular 2 está encapsulado dentro de **componentes**. Es importante mencionar que hay un **componente raíz**, que es el componente principal de nuestra aplicación. 

A continuación muestro la definición de un componente simple en Angular 2 con Typescript: d

{% highlight javascript %}
import {Component} from 'angular2/core';

@Component({
  selector: 'saludo',
  template: '<p>Hola, {{nombre}}</p>'
})
export class Saludo {
  nombre: string;

  constructor() {
    this.nombre = 'Israel';
  }
}
{% endhighlight %}

La primer linea **import {Component} from 'angular2/core';** importa la funcionalidad del decorador [*Component*](https://angular.io/docs/ts/latest/api/core/Component-decorator.html) del paquete principal de Angular 2 *(angular2/core)*. En Angular 2 todo lo que inicia con **@** es un decorador.

El *decorador* **@Component** define nuestro componente. El *selector* define el tag que con el que podremos utilizar nuestro componente dentro de un HTML, en este caso **<saludo></saludo>**. El **template** define el HTML de nuestro componente.

La *clase* **Saludo** es una clase de JavaScript, que define la lógica de nuestro componente. En esta clase estamos declarando una variable de tipo *string* que se llama **nombre**  y la inicializamos dentro del **constructor** de nuestra clase. 

A continuación haremos el componente **componente raíz** de nuestra aplicación: d

{% highlight javascript %}
import {bootstrap} from 'angular2/platform/browser';
import {Saludo} from './saludo';

bootstrap(Saludo);
{% endhighlight %}

La primer linea **import {bootstrap} from 'angular2/platform/browser';** importa la funcionalidad de inicialización (*bootstrap*) de Angular.

La segunda linea **import {Saludo} from './saludo';** importa el componente **Saludo** que creamos anteriormente.

La funcion **bootstrap** le indica a Angular que nuestro **componente raíz** (*componente de aplicación*) será el componente **Saludo** 

Para utilizar nuestro componente de aplicación (**root**) en el index.html solo debemos usar el tag del selector que definimos en nuestro componente, como se muestra a continuación:

{% highlight html %}
 <html>
   <head>
     <title>Intro a Angular 2</title>
     ...
   </head>
   <body>
     <saludo>Carcgando aplicación...</saludo>
   </body>
 </html>
{% endhighlight %}

Angular 2 tiene un componente raiz (**root component**) el cual es el único tag que usaremos en nuestro archivo index.html. 

En Angular 2, cualquier componente puede importar y utilizar otro componente. 

Los componentes de Angular 2 encapsulan un template en HTML y su lógica en una clase de JavaScript.

En el próximo post explicareé como crear instalar y crear un proyecto de Angular 2.
