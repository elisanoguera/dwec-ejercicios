# Sesión 5

# Unidad 3. Gestión de eventos 

## Ejercicio 1 - Objetos manejadores de eventos

Crea un programa en *JavaScript* que muestre para cada chiste un elemento `<div>` que contenga el enunciado y un botón con el texto `Ver respuesta`. Al pulsar en el botón se debe mostrar, mediante un `alert`, la respuesta correspondiente. Aquí con un array de objetos `chiste`.

```javascript

let chistes = [
    {
	enunciado: "¿Qué le dice un bit a otro?",
	respuesta: "Nos vemos en el bus."
    },
    {
	enunciado: "¿Qué es un terapeuta?",
	respuesta: "1024 GigaPeutas."
    },
    {
	enunciado: "¿Cuántos programadores hacen falta para cambiar una bombilla?",
	respuesta: "Ninguno, porque es un problema de hardware."
    }
]

```

<details>

  <summary>Solución:</summary>

La manera más sencilla de realizar la tarea es utilizar objetos manejadores de eventos con la función `addEventListener`. Aquí tienes el código de la solución.

`aplicacion.html`

```html

<!DOCTYPE html>
<html>
    <head>
    <meta charset="UTF-8">
	<title>Objetos manejadores de eventos</title>
    </head>
    <body>
	   <div id="contenedor"></div>
    </body>
    <script src="./aplicacion.js"></script>
</html>

```

`aplicacion.js`

```javascript


let chistes = [
    {
	enunciado: "¿Qué le dice un bit a otro?",
	respuesta: "Nos vemos en el bus."
    },
    {
	enunciado: "¿Qué es un terapeuta?",
	respuesta: "1024 GigaPeutas."
    },
    {
	enunciado: "¿Cuántos programadores hacen falta para cambiar una bombilla?",
	respuesta: "Ninguno, porque es un problema de hardware."
    }
]

// Elemento <div> en el que se mostrará el listado
// Debe estar creado en el documento HTML que ejecute el script

let contenedor = document.getElementById("contenedor");

// Función constructora para crear los manejadores de eventos de los botones
function Manejador() {
    // Método 'handleEvent'
    this.handleEvent = function(evento) {
	// la propiedad objetoChiste del objeto hará referencia al objeto chiste
	alert(this.objetoChiste.respuesta);
    }
}

// Recorremos el array de chistes
for (let chiste of chistes) {
    // Creamos un <div> para cada chiste
    let divChiste = document.createElement("div");

    // Creamos un botón para cada chiste
    let boton = document.createElement("button");
    boton.textContent = "Ver respuesta";

    // Creamos un objeto manejador de eventos a partir del prototipo
    let manejadorBoton = new Manejador();

    // Creamos la propiedad 'objetoChiste' en el manejador
    // para que apunte al objeto 'chiste'
    manejadorBoton.objetoChiste = chiste;

    // Añadimos el objeto manejador de eventos al botón
    boton.addEventListener("click", manejadorBoton);

    // Añadimos el enunciado al <div>
    divChiste.append(chiste.enunciado);

    // Añadimos el botón al <div>
    divChiste.append(boton);

    // Añadimos el <div> al contenedor
    contenedor.append(divChiste);
}        

```

</details>


## Ejercicio 2 - Delegación de eventos

Se dispone de una rejilla formada por celdas que se quieren activar o desactivar pulsando sobre ellas. La activación o desactivación de una celda se traducirá en la presencia o ausencia de la clase activa. Crea el código JavaScript necesario para implementar la funcionalidad indicada de la manera más eficiente posible.


```html

<!DOCTYPE html>
<html>
    <head>
	<meta charset="UTF-8">
	<title>Delegación de eventos</title>
	<style>
	 #rejilla {
	     width: 50vw;
	     height: 50vh;
	     margin: auto;
	     display: grid;
	     grid-template-columns: 1fr 1fr 1fr 1fr;
	     gap: 1em;
	     justify-content: stretch;
	 }

	 .celda {
	     cursor: pointer;
	     padding: 1em;
	     background-color: #c2d9ed;
	     display: flex;
	     align-items: center;
	     justify-content: center;
	 }

	 .activa {
	     background-color: #6ea8db;
	 }
	</style>
    </head>
    <body>
	<div id="rejilla">
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda activa">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	    <div class="celda">celda</div>
	</div>
    </body>

    <script>

     // TODO: Crea aquí el código pedido

    </script>
</html>

```

*Claves de resolución*

1. Debes utilizar la característica de delegación de eventos del DOM: dado que todas las celdas están dentro de una capa contenedora, debes agregar el manejador a dicha capa y no a cada celda.
2. Puesto que el manejador va a estar definido en la capa contenedora, también detectará el evento si se pulsa sobre ella. Tienes que impedir que si se pulsa directamente sobre dicha capa (pulsando en los bordes de las celdas, por ejemplo) se añada la clase activa al contenedor.

<details>

  <summary>Solución:</summary>

```javascript

    // Capa contenedora
	let rejilla = document.getElementById("rejilla");

	// Manejador de eventos
	rejilla.addEventListener("click", function(evento) {

	// Comprobamos que el elemento sobre el que hemos pulsado es una celda
	// ‘matches’ comprueba si el elemento cumple con la condición CSS dada
	// En este caso, se comprueba si el elemento tiene la clase ‘celda’
	// Si no ponemos esta condición, al pulsar en los bordes entre las celdas
	// la capa contenedora cambiará de color también
	    if (evento.target.matches(".celda"))
		    evento.target.classList.toggle("activa");
	});

```

</details>


