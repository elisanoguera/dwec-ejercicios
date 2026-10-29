# Sesión 4

# Unidad 3. El DOM y las API de navegador 

## Ejercicio 1 - Acceder al DOM

```html

<html>
<body>
  <div>Users:</div>
  <ul>
    <li>John</li>
    <li>Peter</li>
  </ul>
</body>
</html>

```

Responde a las siguientes preguntas:

1. ¿Cómo accederías al nodo `<div>`?
2. ¿Cómo accederías al nodo `<ul>`?
3. ¿Cómo accederías al segundo `<li>`?



<details>

  <summary>Solución:</summary>

Hay diferentes maneras, por ejemplo:

1. Para acceder al nodo `<div>`:

    ```javascript

        document.body.firstElementChild
        // o
        document.body.children[0]
      
    ```

2. Para acceder al nodo `<ul>`:

    ```javascript

        document.body.lastElementChild
        // o
        document.body.children[1]

    ```

3. Para acceder al segundo `<li>`:

    ```javascript

        // obtener <ul>, y luego obtener su último elemento hijo
        document.body.lastElementChild.lastElementChild

    ```

</details>


## Ejercicio 2 - Buscar elementos en el DOM

```html

<html>
  <body>
    <form id="search">
      Buscar a los visitantes:
      <table id="age-table">
        <tr>
          <td>Edad:</td>
          <td id="age-list">
            <label><input type="radio" name="age" value="young">menor de 18</label>
            <label><input type="radio" name="age" value="mature">18-50</label>
            <label><input type="radio" name="age" value="senior">mayor de 50</label>
           </td>
        </tr>
      </table>    
      <input type="submit" value="Search">
    </form>
  </body>
</html>

```

¿Cómo encontrarías los siguientes elementos en el código `HTML` anterior?

1. La tabla con `id="age-table"`
2. Todos los elementos `label` dentro de la tabla 
3. El primer `td` de la tabla 
4. El formulario con `id="search"`
5. El primer `input` en el formulario
6. El último `input` en el formulario

<details>

  <summary>Solución:</summary>

```javascript

        // 1. La tabla con id="age-table".
        let table = document.getElementById('age-table')

        // 2. Todos los elementos label dentro de la tabla
        table.getElementsByTagName('label')
        // or
        document.querySelectorAll('#age-table label')

        // 3. El primer td de la tabla
        table.getElementsByTagName('td')[0]
        // or
        table.querySelector('td')

        // 4. El formulario con id="search"
        let form = document.getElementsById('search')
        //o, utilizando el form específicamente
        document.querySelector('form[id="search"]')

        // 5. El primer input en el formulario
        form.getElementsByTagName('input')[0]
        // o
        form.querySelector('input')

        // 6. El último input en el formulario
        let inputs = form.querySelectorAll('input') // encontrar todos los inputs
        inputs[inputs.length-1] // obtener el último
    
```

</details>


## Ejercicio 3 - Creación de HTML desde JavaScript

Utiliza las funciones del **DOM** para crear desde *JavaScript* el siguiente código **HTML**.

A continuación, dispones del **HTML** resultante.


```html

<div class="tarjeta">
    <div class="tarjeta-titulo">
	<h2>
	    Datos de contacto
	</h2>
    </div>
    <div class="tarjeta-cuerpo">
	<p class="tarjeta-nombre">
	    <span class="negrita">Nombre:</span> Laura Pérez
	</p>
	<p class="tarjeta-email">
	    <span class="negrita">Email:</span> laura@noexiste.com
	</p>
	<p class="tarjeta-telefono">
	    <span class="negrita">Teléfono:</span> 612123123
	</p>
    </div>
</div>

```



<details>

  <summary>Solución:</summary>
  
  No existe una solución única, ya que se pueden utilizar diferentes funciones del DOM. 
  
  A continuación, dispones del código de la solución.

   ```javascript

        // Crear elementos
        let tarjeta = document.createElement("div");
        tarjeta.classList.add("tarjeta");

        let tarjetaTitulo = document.createElement("div");
        tarjetaTitulo.classList.add("tarjeta-titulo");

        let encabezado = document.createElement("h2");
        encabezado.textContent = "Datos de contacto";

        let tarjetaCuerpo = document.createElement("div");
        tarjetaCuerpo.classList.add("tarjeta-cuerpo");

        let tarjetaNombre = document.createElement("p");
        tarjetaNombre.classList.add("tarjeta-nombre");

        let tarjetaEmail= document.createElement("p");
        tarjetaEmail.classList.add("tarjeta-email");

        let tarjetaTelefono = document.createElement("p");
        tarjetaTelefono.classList.add("tarjeta-telefono");

        let spanNombre = document.createElement("span");
        spanNombre.classList.add("negrita");

        let spanEmail = spanNombre.cloneNode();
        let spanTelefono = spanNombre.cloneNode();

        spanNombre.textContent = "Nombre:";
        spanEmail.textContent = "Email:";
        spanTelefono.textContent = "Teléfono:";

        // Añadir elementos
        tarjetaTitulo.append(encabezado);

        tarjetaNombre.append(spanNombre);
        tarjetaNombre.append(" Laura Pérez");

        tarjetaTelefono.append(spanTelefono);
        tarjetaTelefono.append(" 612123123");

        tarjetaEmail.append(spanEmail);
        tarjetaEmail.append(" laura@noexiste.com");

        tarjetaCuerpo.append(tarjetaNombre);
        tarjetaCuerpo.append(tarjetaEmail);
        tarjetaCuerpo.append(tarjetaTelefono);

        tarjeta.append(tarjetaTitulo);
        tarjeta.append(tarjetaCuerpo);

        // Añadir estructura al cuerpo de la página
        document.body.append(tarjeta);

   ```

</details>


## Ejercicio 4 - Leer atributos del `Dataset`

Escribe el código para obtener el atributo `data-menu-opciones` del documento y leer su valor.

```html

<!DOCTYPE html>
<html>
<body>
  <div data-menu-opciones="menu">Selecciona una opción:</div>
  <script>
    /* Tu código */
  </script>
</body>
</html>

```

<details>

  <summary>Solución:</summary>

```html

<!DOCTYPE html>
<html>
<body>
  <div data-menu-opciones="menu">Selecciona una opción:</div>
  <script>
    // obteniéndolo
    let elem = document.querySelector('div');

    // leyendo el valor
    alert(elem.dataset.menuOpciones);
    // o
    alert(elem.getAttribute('data-menu-opciones'));
  </script>
</body>
</html>
```

</details>

## Ejercicio 5 - Trabajo con colecciones del DOM

Diseña una función *JavaScript* que se encargue de conmutar la presencia de la clase `activado` en todos los elementos `<div>` con clase `item`:

- Los elementos `<div class=”item activado”>` se deben convertir en `<div class=”item”>`.
- Los elementos `<div class=”item”>` se deben convertir en `<div class=”item activado”>`

**Claves de resolución**

1. En primer lugar, debes seleccionar el conjunto de elementos sobre el que quieres actuar.
2. Recuerda que lo que obtendrás será una colección, no un elemento individual.
3. En lugar de comprobar mediante un condicional si un elemento tiene la clase `activado`, ¿hay algún método que te permita realizar la conmutación directamente?

<details>

  <summary>Solución:</summary>

 
   ```javascript

      function conmutar() {
        let items = document.querySelectorAll(“div.item”);
        for (let item of items) {
          item.classList.toggle(“activado”);
        }
      }

   ```

</details>




