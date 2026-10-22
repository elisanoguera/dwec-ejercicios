# Sesión 3 - Unidad 2. JavaScript

## Ejercicio 1 - Trabajo con arrays  de objetos

Dado el siguiente array de objetos, realiza las siguientes operaciones mediante programación funcional:


```javascript

    let coches = [
        {id: 1, marca:"Seat", modelo:"Ibiza", precio:16000},
        {id: 2, marca:"Seat", modelo:"Ateca", precio:28000},
        {id: 3, marca:"Volkswagen", modelo:"Golf", precio:31000},
        {id: 4, marca:"Kia", modelo:"Niro", precio:35000}
    ]

```

1. Obtén los coches de la marca *Seat*.

<details>

  <summary>Solución:</summary>

   ```javascript

      let cochesSeat = coches.filter(coche => coche.marca == "Seat");

   ```

</details>

2. Obtén los coches cuyo precio sea menor que *25000*.

<details>

  <summary>Solución:</summary>

   ```javascript

      let cochesMenor25000 = coches.filter(coche => coche.precio < 25000);

   ```

</details>

3. Encuentra el primer coche cuyo precio sea mayor que 20000

<details>

  <summary>Solución:</summary>

   ```javascript

      let primeroMayor20000 = coches.find(coche => coche.precio > 20000);

   ```

</details>

4. Transforma el array en otro con los mismos campos más uno adicional, denominado *premium*. Si el precio es mayor de *20000*, `premium=true`; en caso contrario, `premium=false`.

<details>

  <summary>Solución:</summary>

   ```javascript

    let cochesConCampoPremium = coches.map(coche => {
      let nuevo = {};
      Object.assign(nuevo, coche);
      nuevo.premium = (nuevo.precio > 20000) ? true : false;
      return nuevo;
    });

   ```

</details>


5. Calcula el precio medio de los coches de la marca *Seat*.

<details>

  <summary>Solución:</summary>

   ```javascript

    // Utilizando 'reduce' con un acumulador que almacena la cuenta y la suma parcial
    let totalYCuentaSeat = coches.reduce((acc, coche) => {
        if (coche.marca == "Seat") {
          // Sumamos el precio
          acc.total += coche.precio;
          // Incrementamos el número de vehículos Seat
          acc.cuenta++;
        }
        return acc;
    }, {total: 0, cuenta: 0}) ;

    // Calculamos la media
    let precioMedioSeat = totalYCuentaSeat.total / totalYCuentaSeat.cuenta;

   ```
</details>

## Ejercicio 2 - Cálculo de medias (variante funcional)

Vamos a resolver el ejercicio estudiado en el apartado de *Funciones* utilizando código funcional en lugar de bucles. El objetivo es el mismo: crear una función que calcule la media aritmética de un conjunto variable de valores pasados como parámetros.

**Claves de resolución**

La función tiene que procesar un conjunto variable de parámetros, por lo que se deberán utilizar de nuevo los parámetros `rest`.

En cuanto a la elección de la función que se deberá utilizar, hay que tener en cuenta que queremos operar sobre un listado (array) y generar como resultado un único valor. ¿Cuál de las funciones estudiadas en este apartado está especializada en esa tarea?

<details>

  <summary>Solución:</summary>

  La función que habrá que utilizar es, por supuesto, `reduce`. A continuación, se muestra un ejemplo de solución.


   ```javascript
        // Dado que la función debe admitir un número variable de parámetros, utilizamos los parámetros rest
        function media(...numeros) {

          if (numeros.length == 0)
            return 0;
  
          // Calculamos la suma total con ‘reduce’ en lugar de un bucle
          let resultado = numeros.reduce((acc, numero) => {
            return acc + numero;
          }, 0);
          
          return resultado / numeros.length;
        }

   ```

</details>


## Ejercicio 3 - Comprobación del modo estricto

Ejecuta el siguiente programa en una etiqueta `<script>` dentro de una página *HTML* de las siguientes tres maneras:

1. De manera convencional

2. Activando el modo estricto

3. Sin modo estricto, pero activando el atributo `type="module"` en la etiqueta `<script>`.

Ejecuta el siguiente programa, con y sin modo estricto. ¿Sabrías explicar por qué no funciona en modo estricto?

```javascript

function Enemigo (s, f) {
  salud = s;
  fuerza = f;
}

Enemigo.prototype.atacar = function () {
    console.log(`Atacando con fuerza ${fuerza}`);
}

let enemigo1 = new Enemigo(50,20);
let enemigo2 = new Enemigo(40,15);

enemigo1.atacar();
enemigo2.atacar();

```

En cada uno de los tres casos, responde a las siguientes preguntas:

1. ¿El programa se ejecuta sin fallos?

2. En caso afirmativo, ¿funciona correctamente de acuerdo con lo que se espera?

3. ¿Puedes identificar los errores y explicar por qué se producen?

<details>

  <summary>Solución:</summary>
  

El programa se ejecuta sin fallos en una etiqueta `<script>` convencional, pero produce fallos por variable no declarada en el caso de funcionar como módulo o utilizar el modo estricto.

Como puedes comprobar, el programa no funciona correctamente: en modo normal muestra en ambos casos `Atacando con fuerza 15`, cuando en el caso de `enemigo1` debería indicar `fuerza 20`.

```javascript

enemigo1.atacar(); // Atacando con fuerza 15 --> Debería indicar fuerza 20
enemigo2.atacar(); // Atacando con fuerza 15

```

El problema está en la función `Enemigo` y en la función `atacar`: en ambos casos, se ha omitido el uso de `this` para hacer referencia a las propiedades del objeto.

En modo no estricto, JavaScript no encuentra ningún problema de ejecución: la primera llamada a la función `Enemigo` realiza dos asignaciones a variables sin declarar, salud y fuerza, por lo que pasa a buscarlas en el ámbito exterior a la función, que es el `objeto global`. Como allí tampoco están definidas, las define. `salud` y `fuerza` pasan, por tanto, a ser dos variables definidas en el objeto global con valores `50` y `20`, respectivamente.

Al llamar a `Enemigo` la segunda vez, se vuelve a ejecutar el código incorrecto, pero con una diferencia: esta vez JavaScript sí que encuentra las variables definidas en el objeto global, por lo que las sobrescribe. `salud` y `fuerza` pasan a almacenar los valores `40` y `15`, respectivamente.

La función `atacar` tiene el mismo fallo: no hace referencia a `this.fuerza`, sino a `fuerza`. Por ello, en lugar de buscar una propiedad en el objeto (`enemigo1` o `enemigo2`), procede a buscar una variable a través del ámbito léxico, llegando al objeto global. Ahí, encuentra efectivamente una variable llamada `fuerza`, que almacena el último valor que se le ha asignado, que es `15`. Por eso, ambas llamadas a atacar producen el mismo resultado: están accediendo a la misma variable global.

El modo estricto nos protege de este tipo de errores silenciosos, ya que prohíbe la declaración automática de variables si previamente no han sido definidas mediante `let`, `var` o `const`. Por ello, cuando el código trata de ejecutar `salud = s` se produce un error de referencia, ya que `salud` no ha sido declarada en el objeto global.

</details>


## Ejercicio 4 - Parámetros de las funciones

La siguiente función espera recibir como parámetro un objeto con una propiedad denominada data. Sin embargo, puedes comprobar que si se llama a la función sin parámetros o con `null` se producirá un error. Modifica el código para que se capture dicho error y se muestre un mensaje en la consola con el que se indique el problema. En el caso de que produzca un error, la función deberá devolver `-1`.

     ```javascript

      function procesar(mensaje) {
        return mensaje.data;
      }

    ```


**Claves de resolución**

El acceso a `mensaje.data` provoca un error de acceso si mensaje es `null` o `undefined`. Por tanto, hay que englobar el código de la función en un bloque de control de errores para capturarlo. El bloque de procesamiento del error deberá realizar dos tareas: escribir el mensaje en la consola y devolver el valor `-1` como resultado de la función.

<details>

  <summary>Solución:</summary>

   ```javascript

      function procesar(mensaje) {

        try {

          return mensaje.data;

        } catch(error) {
      
        console.log(“El parámetro ‘mensaje’ no está definido”);
        
        return -1;
      
      }


   ```

</details>

