# Asincronismo-con-JavaScript

[Introducción al asincronismo](#Introducción-al-asincronismo)

[Presentación del reto](#Presentación-del-reto)

[Definición Estructura Callback](#Definición-Estructura-Callback)

[]()

[]()

[]()

[]()

[]()

[]()

[]()

[]()

[]()

[]()

## Introducción al asincronismo

JavaScript es un lenguaje de programacion asincrono y no bloqueante con un manejador de eventos conocido como **EventLoop** implementado en un unico hilo(thread) para sus interfaces de entrada y salida

**¿Que es asincronismo?**

Es la accion que no ocurre al mismo tiempo. 

**Ejemplo:**

En un aeropuerto hay un hilo o **thread** que es por donde llegan y salen los aviones, existe una torre de control la cual se llamaria **EventLoop**, dos aviones no se pueden recibir al mismo tiempo ni tampoco salir al mismo tiempo, tiene que existir un tiempo de espera para que uno de ellos pueda llegar o salir y despues continuar con el siguiente

![assets/1.png](assets/1.png)

**Terminos a utilizar con Js**

- **Memory heap:** Región de memoria libre, normalmente de gran tamaño, dedicada al alojamiento dinámico de objetos. Es compartida por todo el programa y controlada por un recolector de basura que se encarga de liberar aquello que no se necesita.

- **Cola o Queue:** Cada vez que nuestro programa recibe una notificación del exterior o de otro contexto distinto al de la aplicación, el mensaje se inserta en una cola de mensajes pendientes y se registra su callback correspondiente.

- **Eventloop o Loop de eventos:** Cuando la pila de llamadas (call stack) se vacía, es decir, no hay nada más que ejecutar, se procesan los mensajes de la cola. Con cada ‘tick’ del bucle de eventos, se procesa un nuevo mensaje.

- **Call Stack:** La pila de llamadas, se encarga de albergar las instrucciones que deben ejecutarse. Nos indica en que punto del programa estamos, por donde vamos.

- **CallBack:** Una función de callback es una función que se pasa a otra función como un argumento, que luego se invoca dentro de la función externa para completar algún tipo de rutina o acción.

- **Events:** Comportamientos del usuario que interactúa con una página que pueden detectarse para lanzar una acción, como por ejemplo que el usuario haga click en un elemento (onclick), que elija una opción de un desplegable (onselect), que pase el ratón sobre un objeto (onmouseover), etc.

- **Compilar:** Compilar es generar código ejecutable por una máquina, que puede ser física o abstracta como la máquina virtual de Java.

- **Transpilar:** Transpilar es generar a partir de código en un lenguaje código en otro lenguaje. Es decir, un programa produce otro programa en otro lenguaje cuyo comportamiento es el mismo que el original.

- **Hoisting:** Sugiere que las declaraciones de variables y funciones son físicamente movidas al comienzo del código en tiempo de compilación.

- **DOM:** DOM permite acceder y manipular las páginas XHTML como si fueran documentos XML. De hecho, DOM se diseñó originalmente para manipular de forma sencilla los documentos XML.

- **XML:** Lenguaje de marcado creado para la transferencia de información, legible tanto para seres humanos como para aplicaciones informáticas, y basado en una sencillez extrema y una rígida sintaxis. Así como el HTML estaba basado y era un subconjunto de SGML, la reformulación del primero bajo la sintaxis de XML dio lugar al XHTML; XHTML es, por tanto, un subconjunto de XML.

- **API:** Interfaz de programación de aplicaciones (Application Programming Interface). Es un conjunto de rutinas que provee acceso a funciones de un determinado software.

- **Concurrencia:** Cuando dos o más tareas progresan simultáneamente.

- **Paralelismo:** Cuando dos o más tareas se ejecutan, literalmente, a la vez, en el mismo instante de tiempo.

- **Bloqueante:** Una llamada u operación bloqueante no devuelve el control a nuestra aplicación hasta que se ha completado. Por tanto el thread queda bloqueado en estado de espera.

- **Síncrono:** Es frecuente emplear ‘bloqueante’ y ‘síncrono’ como sinónimos, dando a entender que toda la operación de entrada/salida se ejecuta de forma secuencial y, por tanto, debemos esperar a que se complete para procesar el resultado.

El memory heap es el espacio en memoria compartido para toda la aplicacion, luego esta la pila de ejecucion o **Call Stack** donde estaran las funciones puestas en ejecucion en forma de pila y despues va a estar la cola de tareas.

Las funciones que estan en **Call Stack** hacen un llamado a un **setTimeOut** o a alguna **API**, la cual se desencadena por medio de un **CallBack** y este va a ser puesto en la **Cola de tareas**, mientras tanto otras funciones se estan ejecutando y estan entrado y saliendo.

El **EventLoop** se encarga de preguntar si la pila de ejecucion o **Call Stack** esta vacia para luego resolver la funcion que estaba puesta en **CallBack** y luego pasa a ejecutarla y de esta forma es como continua el funcionamiento del asincronismo en JavaScript.

## Presentación del reto

Utilizar las principales estructuras que utiliza Js para trabajar con el asincronismo **(CallBacks, Promises, Async Await)**.

Consumir la API de Rick And Morty la cual contiene todos los personajes de la serie animada.

![assets/2.png](assets/2.png)

1. Obtener la lista de cuantos personajes tiene la serie.

2. Nombre del primer personaje que regrese.

3. Obtener la dimension a la cual pertenece el personaje en un tercer llamado.

La API se va a utilizar 3 veces en cada uno de los ejercicios utilizando **(CallBacks, Promises, Async Await)**, para esto es necesario entender como funciona la API y en este [enlace](https://rickandmortyapi.com/documentation) se encuentra toda la documentacion, donde se explica como esta constituida la API, cuales son los principales elementos a obtener y cuales son las caracteristicas que tiene (personajes, locacion, episodios), etc.

## Definición Estructura Callback

El **Callback** es una funcion que al crearla se le pasa como parametro una segunda funcion y de esta forma al momento de hacer una peticion o un llamado asincrono esta se ejecuta despues del llamado.

Abrir la terminal y ubicar la carpeta donde se esten realizando los proyectos.

Se inicializa el proyecto con `npm init` que permite establecer que es el proyecto y de que se va a trabajar con el 

![assets/3.png](assets/3.png)

Ahora en la carpeta del curso crear la carpeta **src**, dentro de esta crear una subcarpeta que se llame **callback** y luego dentro de esta crear un nuevo archivo que se llame **index.js**.

Lo primero que se va a hacer es crear una funcion y esta funcion se le va a pasar por parametro una segunda funcion la cual va a ejecutar codigo.

1. Se crea una funcion suma que recibe 2 parametros el cual es el numero 1 y el numero 2. La funcion como resultado regresa la suma de los 2 numeros.

2. Se crea la segunda funcion que recibe los parametros de la funcion 1 y un tercer parametro llamado callback (por convencion se coloca la palabra callback para identificar que es un callback). La funcion retorna al callback con los argumentos de la primer funcion

3. se imprime a traves de un `console.log` los parametros que recibe la funcion `calc` y se hace el llamado de la funcion 1 por parametro junto con sus parametros.

Teniendo en cuenta esto, si existiera una funcion resta, se podria ejecutar en forma de pila, primero la suma, luego la resta, etc.

```
function sum(num1, num2) {
    return num1 + num2;
}

function calc(num1, num2, callback) {
    return callback(num1,num2);
}

console.log(calc(5, 8, sum));
```

Antes de ejecutar este bloque de codigo, una buena practica es generar los scripts que permitiran ejecutar el programa de forma correcta.

abrir el archivo **package.json** y borrar la siguiente linea de codigo `"test": "echo \"Error: no test specified\" && exit 1"` reemplazar por lo siguiente `"callback": "node src/callback/index.js"`

![assets/4.png](assets/4.png)

Ahora abrir la terminal sobre la ubicacion del proyecto y ejecutar 

`npm run callback`

y en la terminal aparecera el resultado del programa

![assets/5.png](assets/5.png)

A continuacion abrir nuevamente el archivo **index.js** para seguir trabajando con ejemplos pero con tiempos y esta vez el ejemplo sera con fechas como se muestra a continuacion 

1. Se crea la function date que recibe como argumento un callback, despues imprime a traves de console.log la fecha actual es decir hoy, despues se establece un setTimeout para que exista una ejecucion del callback de 3 segundos.

2. Se crea la funcion PrintDate que pasa como parametro el nombre del callback y a traves de console.log imprime el callback

3. se llama a la funcion date con el nombre del callback

```
function date(callback) {
    console.log(new Date);
    setTimeout(function () {
        let date = new Date;
        callback(date);
    }, 3000)
}

function printDate(dateNow) {
    console.log(dateNow);
}

date(printDate);
```

Nuevamente en la terminal ejecutar `npm run callback`

![assets/6.png](assets/6.png)

Lo primero que pasa es la operacion que se habia realizado en un principio, en segundo lugar e ejecuta `console.log(new Date);` y por ultimo se ejecuta 3 segundos despues la fecha con la diferencia de 3 segundos