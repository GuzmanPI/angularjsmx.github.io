---
layout: post
permalink: /blog/angular2-components-inputs/
title: "Angular 2 Components: Input"
date:   2016-03-20 00:00:00
categories: [angular2, component, post]
author: eusoj
description: Accediendo a los atributos de un Componente a través de @Input
---

Un Componente en Angular 2 nos permite definir un elemento HTML a través un **selector** si comparamos 
la sintáxis con la de Angular 1 resulta bastante familiar.

{% highlight javascript %}

/*Component Angular 1.5.0*/
.component('hello', {
    template : '<p>Hello</p>'
});

{% endhighlight %}

{% highlight javascript %}

/*Component Angular 2 (beta)*/
@Component({
  selector: 'hello',
  template: '<p>Hello</p>'
})
{% endhighlight %}

Si bien Angular 1 por medio de **bindings** nos permite pasar un valor al atributo de una directiva, **@Input** nos permitirá 
 hacer lo mismo pero en Angular 2. <small> \(si es la primera vez que escribes una aplicación en Angular 2 con TypeScript te recomiendo que leas
 el artículo de [introducción](http://angularmexico.com/blog/intro-angular2/) \)</small>.
 
Para utilizar @Input dentro de nuestros componentes, lo primero que tenemos que hacer es importarlo en nuestro archivo:
   
{% highlight javascript %}
import {Component,Input} from 'angular2/core';
{% endhighlight %}

Una vez realizado esto, dentro de la clase asociada a nuestro componente podremos indicar el nombre y tipo de 
dato que obtendremos a partir de los atributos del elemento, si necesitamos un par llamados **name** y **age** podemos hacer lo siguiente
 para obtenerlos:

{% highlight javascript %}
@Input() name: string;
@Input('age') n : number;
{% endhighlight %}

Si notamos el segundo caso, el de @Input **age**, la sintaxis es un poco diferente, al pasar como parámetro de @Input
el nombre del atributo, podemos definir un nombre diferente a la variable la cual será utilizada dentro 
del template, nuestro archivo del componente quedaría de la siguiente manera

{% highlight javascript %}
/*Archivo: hello.ts*/
  
import {Component,Input} from 'angular2/core';

@Component({
    selector : 'hello',
    template : '<div>Hello { { name } }, { { n } }</div>'
})
  
export class Hello{
    @Input() name: string;
    @Input('age') n : number;
}
{% endhighlight %}

Podemos llamara este componente dentro del que hará bootstrap por medio del tag del *elemento* 
que definimos como selector y agregandolo como "Directiva" para que sea válido dentro del componente. 

{% highlight javascript %}
/*Archivo: component.ts*/
  
import {Component} from 'angular2/core';
 /*Estamos haciendo referencia a la clase Hello del archivo hello.ts*/
import {Hello} from './hello';

@Component({
    selector : 'app',
    template : '
        <hello name="Batman" age="4"></hello>
        <hello *ngFor="#user of users" name="{ {user.name} }" age="{ {user.age} }"></hello>
        ',
    directives :[Hello] /*Importamos como directiva*/
})

export class AppComponent{
   public users = [
       {name: 'Superman', age:4},
       {name: 'Spiderman', age:5},
       {name: 'Robin', age:10}
   ];
}
{% endhighlight %}

El código de este ejemplo se encuentra en el siguiente [repositorio](https://github.com/blacknash/angular2-component-input),