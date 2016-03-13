---
layout: post
permalink: /blog/component-angular-1-5/
title: "Método .component() en Angular 1.5"
date:   2016-03-13 02:18:00
categories: [angular, component, post]
author: eusoj
description: Un vistazo rápio al .component de Angular desde la versión 1.5
---

Desde el último release estable de Angular(1.5.0), se introdujo el método de **.component()**, el cuál nos permite simplificar la manera en que creamos directivas y que en cierta manera nos permite escribir código pensando en la versión de Angular 2.

A diferencia de la directiva, la cual era generada a partir de una función, un componente permite definir su comportamiento a partir de un objeto.

{% highlight javascript %}
/*Directiva*/
.directive('hello', function(){
  return {
    scope : {},
    bindToController:{
      name : '='
    },
    controller: function(){}
    controllerAs: 'helloCtrl',
    template: '<h1>Hello {{helloCtrl.name}}</h1>'
  }
});

/*Component*/
.component('hello', {
  bindings: {
    name : '='
  },
  template : '<h1>Hello {{$ctrl.name}}</h1>'
})

{% endhighlight %}

Entre las primeras diferencias que notamos se encuentra la manera en que obtenemos los atributos de nuestros elementos, nuestra directiva utiliza **bindigToController** el cual fu simplificado a **bindings**, de está manera nuestro componente obtiene los valores directamente.

{% highlight javascript %}
/*Directiva*/
  bindToController:{
    name : '='
  },

/*Component*/
  bindings: {
    name : '='
  },

{% endhighlight %}

El siguiente cambio que notamos, es que no tenemos la necesidad de incluir **controller** y **controllerAs** de primera instancia en la definición de nuestro componente, esto se debe a que dentro de nuestro componente ahora existen valores de default para cada uno de estros atríbutos de nuestro objeto:
{% highlight javascript %}
/*Directiva*/
    controller: function(){}
    controllerAs: 'helloCtrl',
    template: '<h1>Hello {{helloCtrl.name}}</h1>'
 
/*Component*/
  template : '<h1>Hello {{$ctrl.name}}</h1>'
{% endhighlight %}


|              | directive      | component             |
|--------------|----------------|-----------------------|
| controller   | default:None   | default: function(){} |
| controllerAs | default: false | default: $ctrl        |

Sin lugar a duda todos estos cambios hacen más entendible la manera de escribir componentes para nuestras aplicaciones, algo que debemos de tener en cuenta es que todos nuestros componentes tendrán el valor de restrict de **E** en tods las ocasiones por lo que siempre será necesario llamarlos como elementos dentro de nuestro HTML, si necesitamos utilizar alguna otra variante como clase o atributo es necesario utilizar una directiva.

En post posteriores, veremos como crear componentes definiendo acciones en su controlador y veremos el manejo de Component Router.
