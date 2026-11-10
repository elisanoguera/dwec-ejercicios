# Sesión 6

# Unidad 3. Formularios y controles

## Ejercicio 1 - Mostrar el contenido de un campo

Crea un formulario con un único campo para introducir un nombre. Cada vez que el usuario modifique el contenido del campo, debe mostrarse debajo del formulario.

A continuación se muestra el código *HTML* inicial:

```html

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Mostrar valor de un campo</title>
</head>
<body>
    <h1>Datos del usuario</h1>
    <form id="formulario">
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" name="nombre">
		<button type="submit">Mostrar contenido</button>
    </form>
    <p>Valor del campo: <span id="resultado"></span></p>

    <script>
    // TODO
    </script>
</body>
</html>

```

<details>

  <summary>Solución:</summary>

```javascript

    // Accedemos al formulario
    const formulario = document.getElementById("formulario");

    // Accedemos al campo del formulario
    const campoNombre = document.getElementById("nombre");

    // Accedemos al elemento donde mostraremos el resultado
    const resultado = document.getElementById("resultado");

    // Detectamos cualquier modificación del campo
    formulario.addEventListener("submit", function (event) {
	   // Evita que la página se recargue
       event.preventDefault();
       // Leemos y mostramos el valor actual. Se podría acceder también con event.target.elements.nombre.value
       // resultado.textContent = event.target.elements.nombre.value;
       resultado.textContent = campoNombre.value;
    });

```

</details>


## Ejercicio 2 - Acceso a campos del formulario

A partir del siguiente código *HTML*, crea el código necesario en *JavaScript* para que cuando se envie el formulario, se impida el envío y muestre en un `alert` el valor de los campos del formulario.

```html

<!DOCTYPE html>
<html>
    <head>
	<meta charset="UTF-8">
	<title>Formularios</title>
    </head>
    <body>
	<div id="contenedor">
	    <form id="formulario">
		<div>
		    <label for="nombre">Nombre</label>
		    <input name="nombre" type="text" id="nombre" required>
		</div>
		<div>
		    <label for="email">Email</label>
		    <input name="email" type="email" id="email" required>
		</div>
		<div>
		    <input name="" type="submit">
		</div>
	    </form>

	</div>
    </body>

    <script>
	// TODO
    </script>
</html>

```

<details>

  <summary>Solución:</summary>

```javascript

     // Formulario
     let formulario = document.getElementById("formulario");

     // Manejador de eventos
     formulario.addEventListener("submit", function(evento) {
	 // Impedimos el envío
	 evento.preventDefault();

	 // Accedemos al contenido de los campos 'nombre' y 'email'
	 // También se puede hacer mediante: formulario.elements.nombre.value y formulario.elements.email.value
	 let nombre = evento.target.elements.nombre.value;
	 let email = evento.target.elements.email.value;

	 // Mostramos los valores de los campos
	alert(`Nombre: ${nombre}, email: ${email}`);

     });

```

</details>


## Ejercicio 3 - Formulario de inscripción

Crea un formulario que permita escribir el nombre de una persona y enviarlo. Al enviar el formulario, se debe desactivar el botón para evitar que se pulse dos veces. Mientras el botón esté desactivado debe mostrar el texto `Procesando...`. Simula un procesamiento de 2 segundos mediante `setTimeout()`, al finalizar el temporizador, vuelve a activar el botón y recupera su texto original. Este sería el código *HTML* inicial:

```html

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Formulario de inscripción</title>
</head>
<body>
    <h1>Formulario de inscripción</h1>

    <form id="formulario">
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" name="nombre" required>
        <button type="submit" id="botonEnviar">Enviar</button>
    </form>

    <p id="resultado"></p>

    <script>
	// TODO
    </script>

</body>
</html>


```

<details>

  <summary>Solución:</summary>

```javascript

        const formulario = document.getElementById("formulario");
        const campoNombre = document.getElementById("nombre");
        const botonEnviar = document.getElementById("botonEnviar");
        const resultado = document.getElementById("resultado");

        formulario.addEventListener("submit", function (evento) {
            // Evita que la página se recargue
            evento.preventDefault();

            // Evita procesar el formulario dos veces
            if (botonEnviar.disabled) {
                return;
            }

            // Lee el contenido del campo
            const nombre = campoNombre.value.trim();

            // Bloquea el botón durante el procesamiento
            botonEnviar.disabled = true;
            botonEnviar.textContent = "Procesando...";

            resultado.textContent = "";

            // Simula un envío que tarda 2 segundos
            setTimeout(function () {
                
                resultado.textContent = "Formulario enviado para: " + nombre;

                // Vuelve a habilitar el botón
                botonEnviar.disabled = false;
                botonEnviar.textContent = "Enviar";

                // Limpia el formulario
                formulario.reset();
            }, 2000);
        });

```

</details>

## Ejercicio 4 - Objetos y formularios

Disponemos de un formulario con los campos: `Nombre`, `Apellidos`, `Correo electrónico`, `Ciclo formativo` y `Modalidad`. Cuando se cargue la página, los campos del formulario deben mostrar automáticamente los datos almacenados en el objeto `alumno`. Al pulsar el botón `Guardar`, debe aparecer un mensaje indicando que los datos se han guardado correctamente.

El código *HTML* inicial sería el siguiente

```html

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Datos del alumno</title>
</head>
<body>

    <h1>Datos del alumno</h1>

    <form id="formularioAlumno">

        <p>
            <label for="nombre">Nombre:</label>
            <input type="text" id="nombre" name="nombre" required>
        </p>

        <p>
            <label for="apellidos">Apellidos:</label>
            <input type="text" id="apellidos" name="apellidos" required>
        </p>

        <p>
            <label for="correo">Correo electrónico:</label>
            <input type="email" id="correo" name="correo" required>
        </p>

        <p>
            <label for="ciclo">Ciclo formativo:</label>
            <select id="ciclo" name="ciclo">
                <option value="DAM">DAM</option>
                <option value="DAW">DAW</option>
                <option value="ASIR">ASIR</option>
            </select>
        </p>

        <p>
            <label for="modalidad">Modalidad:</label>
            <select id="modalidad" name="modalidad">
                <option value="presencial">Presencial</option>
                <option value="semipresencial">Semipresencial</option>
            </select>
        </p>

        <button type="submit">Guardar cambios</button>

    </form>

    <p id="resultado"></p>

    <h2>Contenido actual del objeto</h2>
    <pre id="datosObjeto"></pre>

    <script>
        // Objeto con los datos iniciales
        const alumno = {
            nombre: "Elena",
            apellidos: "López García",
            correo: "elena.lopez@gmail.com",
            ciclo: "DAW",
            modalidad: "semipresencial"
        };

    // TODO 

    </script>

</body>
</html>

```

<details>

  <summary>Solución:</summary>

```javascript

    // Seleccionamos los elementos necesarios
        const formulario = document.getElementById("formularioAlumno");
        const resultado = document.getElementById("resultado");
        const datosObjeto = document.getElementById("datosObjeto");

        // Función para mostrar el objeto en la página
        function mostrarObjeto() {
            // JSON.stringify (value, replacer, space)
            // value: objeto
            // replacer: propiedades a mostrar, si es null se muestran todas
            // space: si es Number es el número de espacios que se intertarán
            datosObjeto.textContent = JSON.stringify(alumno, null, 4);
        }

        // Cargamos los datos iniciales del objeto en el formulario
        document.getElementById("nombre").value = alumno.nombre;
        document.getElementById("apellidos").value = alumno.apellidos;
        document.getElementById("correo").value = alumno.correo;
        document.getElementById("ciclo").value = alumno.ciclo;
        document.getElementById("modalidad").value = alumno.modalidad;

        // Mostramos inicialmente el contenido del objeto
        mostrarObjeto();

        // Asignamos la función manejadora de eventos al envío del formulario
        formulario.addEventListener("submit", function (evento) {
            // Evitamos que la página se recargue
            evento.preventDefault();

            // Guardamos los valores del formulario en el objeto
            alumno.nombre = document.getElementById("nombre").value;

            alumno.apellidos = document.getElementById("apellidos").value;

            alumno.correo = document.getElementById("correo").value;

            alumno.ciclo = document.getElementById("ciclo").value;

            alumno.modalidad = document.getElementById("modalidad").value;

            // Mostramos un mensaje
            resultado.textContent = "Los datos se han guardado correctamente.";

            // Mostramos el objeto actualizado
            mostrarObjeto();

            // También podemos comprobarlo en la consola
            // console.log(alumno);
        });

```

</details>


## Ejercicio 5 - Acceso a valores del formulario

Dado el formulario siguiente, crea una función *JavaScript* que muestre mediante un `alert` el contenido de sus campos cuando se produzca el evento de envío. El formulario no debe enviarse.

```html

<!DOCTYPE html>
<html>
    <head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
	<title> Acceso a valores del formulario</title>
    </head>
    <body>
	<h1>Formulario de contacto</h1>
	<form name="form1">
	    <div>
		<label for="nombre">Nombre</label>
		<input id="nombre" name="nombre" type="text">
	    </div>
	    <div>
		<label for="apellidos">Apellidos</label>
		<input id="apellidos" name="apellidos" type="text">
	    </div>
	    <div>
		<label for="email">Email</label>
		<input id="email" name="email" type="text">
	    </div>
	    <div>
		<label for="telefono">Teléfono</label>
		<input id="telefono" name="telefono" type="text">
	    </div>
	    <div>
		Edad:
		<label for="menor30">Menos de 30</label>
		<input id="menor30" name="edad" type="radio" value="menor30">
		<label for="entre3050">Entre 30 y 50</label>
		<input id="entre3050" name="edad" type="radio" value="entre3050">
		<label for="mayor50">Más de 50</label>
		<input id="mayor50" name="edad" type="radio" value="mayor50">
	    </div>
	    <div>
		<button type="submit">Enviar</button>
	    </div>
	</form>
	<script>
	 // TODO
	</script>
    </body>
</html>

```

*Claves de resolución*

1. El formulario no debe enviarse: recuerda que el evento de envío lleva asociada la acción de envío por defecto, así que deberás impedir que se ejecute. 
2. Puedes acceder a `form.elements` para iterar la colección, pero ten en cuenta que si lo haces accederás a todos los controles, tengan o no el mismo atributo `name`: en este ejemplo en concreto, accederás a los tres elementos radio y al botón de envío también. Por ello, es más recomendable acceder a los elementos a través de su `name`.

<details>

  <summary>Solución:</summary>

```javascript

	 // Accedemos al formulario
	let form = document.forms.form1;
	// Manejador de eventos
	form.addEventListener("submit", function(evento) {
		// Impedimos el envío por defecto
		evento.preventDefault();
		// Mensaje que se mostrará
		let mensaje = `Nombre: ${form.elements.nombre.value}
		Apellidos: ${form.elements.apellidos.value}
		Email: ${form.elements.email.value}
		Teléfono: ${form.elements.telefono.value}
		Edad: ${form.elements.edad.value}`;
		// Mostramos el mensaje
		alert(mensaje);
	});

```

</details>



## Ejercicio 6 - Envío y validación de formularios

Crea un formulario con tres campos, para *nombre*, *apellidos* y *NIF/NIE*, y sus correspondientes etiquetas.

Los tres campos deben ser obligatorios. Puedes utilizar validación *HTML5* para ello. Además, debes añadir la lógica de validación necesaria para comprobar, antes del envío, si el *NIF* o *NIE* introducido es correcto de acuerdo con el algoritmo oficial. Si el número no es correcto, se mostrará un mensaje mediante `alert`; si es correcto, se procederá al envío del formulario.

Dispones del código de una función de comprobación de *NIF/NIE* que puedes utilizar para realizar la comprobación:

```javascript

// Función para calcular la letra del NIF/NIE
function comprobarNifNie(nif) {
    var letras = ['T', 'R', 'W', 'A', 'G', 'M', 'Y', 'F', 'P', 'D', 'X', 'B', 'N', 'J', 'Z', 'S', 'Q', 'V', 'H', 'L', 'C', 'K', 'E', 'T'];

    // Convertimos a mayúsculas
    let nifMay = nif.toUpperCase();

    // Para tratar el NIE
    let primeraLetra = nifMay.substr(0,1);

    // Última letra, para comprobación
    let letraNIF = nifMay.substring(8, 9);

    // Para almacenar el número
    let numNIF;

    // Si el primer carácter no es un número (NIE),
    // sustituimos por su número equivalente de acuerdo al algoritmo del NIE
    if (isNaN(primeraLetra)) {
	switch (primeraLetra) {
	    case "X":
		numNIF = "0";
		break;
	    case "Y":
		numNIF = "1";
		break;
	    case "Z":
		numNIF = "2";
		break;
	    default:
	}
	numNIF += nifMay.substring(1,8);
    } else {
	numNIF = nifMay.substring(0,8);
    }

    // Convertimos a número
    numNIF = parseInt(numNIF);

    // Calculamos la letra que corresponde a partir del número
    // Cogemos el resto de dividir el número del NIF entre 23
    // El resultado nos da la posición del array 'letras' donde
    // se encuentra la letra asociada a dicho número
    let letraCalculada = letras[numNIF % 23];

    // Comprobamos si coincide con la letra indicada en el formulario
    if (letraCalculada === letraNIF) {
	return true;
    } else {
	return false;
    }
}

```

<details>

  <summary>Solución:</summary>

```html

<!DOCTYPE html>
<html>
    <head>
	<meta charset="UTF-8">
	<title>Envío y validación de formularios</title>
    </head>
    <body>
	<div id="contenedor">
	    <form id="formulario">
		<div>
		    <label for="nombre">Nombre</label>
		    <input name="nombre" type="text" id="nombre" required>
		</div>
		<div>
		    <label for="apellidos">Apellidos</label>
		    <input name="apellidos" type="text" id="apellidos" required>
		</div>
		<div>
		    <label for="nif">NIF/NIE</label>
		    <input name="nif" type="text" id="nif" required>
		</div>
		<div>
		    <input name="" type="submit">
		</div>
	    </form>

	</div>
    </body>

    <script>

     // Función para calcular la letra del NIF/NIE
     function comprobarNifNie(nif) {
	 var letras = ['T', 'R', 'W', 'A', 'G', 'M', 'Y', 'F', 'P', 'D', 'X', 'B', 'N', 'J', 'Z', 'S', 'Q', 'V', 'H', 'L', 'C', 'K', 'E', 'T'];

	 // Convertimos a mayúsculas
	 let nifMay = nif.toUpperCase();

	 // Para tratar el NIE
	 let primeraLetra = nifMay.substr(0,1);

	 // Última letra, para comprobación
	 let letraNIF = nifMay.substring(8, 9);

	 // Para almacenar el número
	 let numNIF;

	 // Si el primer carácter no es un número (NIE),
	 // sustituimos por su número equivalente de acuerdo al algoritmo del NIE
	 if (isNaN(primeraLetra)) {
	     switch (primeraLetra) {
		 case "X":
		     numNIF = "0";
		     break;
		 case "Y":
		     numNIF = "1";
		     break;
		 case "Z":
		     numNIF = "2";
		     break;
		 default:
	     }
	     numNIF += nifMay.substring(1,8);
	 } else {
	     numNIF = nifMay.substring(0,8);
	 }

	 // Convertimos a número
	 numNIF = parseInt(numNIF);

	 // Calculamos la letra que corresponde a partir del número
	 // Cogemos el resto de dividir el número del NIF entre 23
	 // El resultado nos da la posición del array 'letras' donde
	 // se encuentra la letra asociada a dicho número
	 let letraCalculada = letras[numNIF % 23];

	 // Comprobamos si coincide con la letra indicada en el formulario
	 if (letraCalculada === letraNIF) {
	     return true;
	 } else {
	     return false;
	 }
     }

     // Formulario
     let formulario = document.getElementById("formulario");

     // Manejador de eventos
     formulario.addEventListener("submit", function(evento) {
	 // Impedimos el envío
	 evento.preventDefault();

	 // Accedemos al contenido del campo 'nif'
	 // También se puede hacer mediante:
	 // formulario.elements.nif.value
	 let nif = evento.target.elements.nif.value;

	 // Comprobamos si es correcto
	 if (comprobarNifNie(nif)) {
	     evento.target.submit();
	 } else {
	     alert("El NIF/NIE es incorrecto");
	 }
     });
    </script>
</html>

```

</details>





