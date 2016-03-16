---
layout: post
permalink: /blog/custom-filters-angular/
title: "Custom Filters en Angular"
date:   2016-03-15 19:18:00
categories: [angular, filter, post, tip]
author: eusoj
description: Custom filters, un gran ayudante para el manejo del DOM dentro de Angular
---

Si bien al escuchar el término "filter" en Angular nos recuerda de manera inmediata a la hábilidad de filtrar dentro de un **ng-repeat** los valores que existen en un conjunto de objetos, está vez nos referiremos a la habilidad que tiene Angular de renderear una variable en el DOM en el formato que necesitamos.

La mayoría de los **filtros** de [Angular](https://docs.angularjs.org/api/ng/filter/) que utilizamos dentro de nuestras aplicaciones son para dar formato a fechas, monedas, números, etc., cada uno de elos bien cubiertos y con bastante documentación de como ser utilizados dentro del sitio, basta con poner un **pipe** ( &#124;
 ) e inmediatamente el filtro a utilizar.

{% highlight html %}
<!-- Resultado: 2.59 -->
<p>{{ 2.5879879812 | number: 2}}</p>

<!-- Resultado: $2.49 -->
<p>{{ 2.49 | currency : "$"}}</p>

<!-- Restulado: Oct 28, 2010 10:40:23 PM -->
<p>{{1288323623006 | date:'medium'}}</p>
{% endhighlight %}

Dentro de nuestras aplicaciones podemos tener filtros personzalizados utilizando el método *.filter* bajo la siguiente estructura:

{% highlight javascript %}
angular
  .filter('filtername' , filter_function)

function filter_function(){
  return function(input) { 
    return input;
  }; 
}
{% endhighlight %}

*.filter* recibe dos parámetros, el primero es el nombre de nuestro filtro , y en seguida debemos de darle una función, si deseamos construir un filtro que se de la bienvenida a un usario, la primera parte de nuestro código quedaría de la siguiente manera:

{% highlight javascript %}
angular
  .filter('bienvenida' , filter_function)
{% endhighlight %}

Teniendo el filtro definido, la función para generar el mensaje quedaría como sigue:

{% highlight javascript %}
function filter_function(){

  return function(input) { 
    return "Bienvenido" + input;
  }; 

}
{% endhighlight %}

El parámetro de la función **input** es el valor u objeto que se encuentra la izquierda de nuestro pipe y cuyo valor dará la salida en el DOM, está función es invocada cada vez que se genera un **$digest** en Angular.

Para invocarlo en HTML tenemos que hacer lo siguiente:

{% highlight html %}
<!-- Resultado: Bienvenido Josue -->
<p>{{ 'Josue' | bienvenida}}</p>
{% endhighlight %}

Dentro de estos filtros incluso podemos definir operaciones matemáticas que afecten el resultado, como el siguiente caso en el cual escribimos un filtro que obtenga el triple del número que indicamos.


{% highlight javascript %}
angular
  .filter('triple' , triplefunction)

function triplefunction(){
  return function(input) { 
    return input*3;
  }; 
}
{% endhighlight %}

{% highlight html %}
<!-- Resultado: 9 -->
<p>{{  3 | triple }}</p>

<!-- Resultado: 12 -->
<p>{{  4 | triple }}</p>

<!-- Resultado: $15.00-->
<!-- Podemos utilizar muchos filtros al mismo tiempo -->
<p>{{  5 | triple | currency: "$"}}</p>
{% endhighlight %}

Si bien en muchos casos, el performance se ve afectado cuando abusamos del uso de estos filtros, resultand de gran ayuda en casos de que necesitemos formatos muy especificos dentro de nuestras aplicaciones, hay que usarlos sabiamente y considerar el costo que tendrán en el *$digest* de Angular.

