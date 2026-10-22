# Sesión 2 - Unidad 2. JavaScript

## Ejercicio 1 - Construcción objeto mediante un literal

¿Cuáles serían los valores de las variables `a`, `b`, `c` y `d` después de ejecutar el siguiente código?

```javascript
let a = 1, b = 1;

let c = ++a; // ?
let d = b++; // ?
```

<details>

  <summary>Solución:</summary>

  La respuesta es:

        a = 2
        b = 2
        c = 2
        d = 1
  
   ```javascript
  let a = 1, b = 1;

    alert( ++a ); // 2, la forma de prefijo devuelve el nuevo valor
    alert( b++ ); // 1, la forma de sufijo devuelve el antiguo valor

    alert( a ); // 2, incrementado una vez
    alert( b ); // 2, incrementado una vez
   ```

</details>


## Ejercicio 2 - Funciones constructoras

Reescribir esta condición `if` usando el operador ternario `?`:

```javascript
let result;

if (a + b < 4) {
  result = 'Menor';
} else {
  result = 'Mayor';
}
```

<details>

  <summary>Solución:</summary>

   ```javascript
        let result = (a + b < 4) ? 'Menor' : 'Mayor';
   ```

</details>


## Ejercicio 3 - Object.Create()

Reemplazar las funciones anónimas con funciones de flecha en el siguiente código:

```javascript

    function ask(question, yes, no) {
        if (confirm(question)) yes();
        else no();
    }

    ask(
    "Do you agree?",
    function() { alert("You agreed."); },
    function() { alert("You canceled the execution."); }
    );
```

<details>

  <summary>Solución:</summary>

   ```javascript
        function ask(question, yes, no) {
            if (confirm(question)) yes();
            else no();
        }

        ask(
        "Do you agree?",
        () => alert("You agreed."),
        () => alert("You canceled the execution.")
        );
   ```

</details>


## Ejercicio 4 - Class

Realizar una función llamada `sumAll` que devuelva la suma de todos los parámetros. El número de parámetros será variable. Utilizar un bucle de tipo `for of` para recorrer el `array`.

<details>

  <summary>Solución:</summary>

   ```javascript
        function sumAll(...args) { // args es el nombre del array

            let sum = 0;

            for (let arg of args) sum += arg;

            return sum;
        }

        sumAll(1); // 1
        sumAll(1, 2); // 3
        sumAll(1, 2, 3); // 6
   ```

</details>
