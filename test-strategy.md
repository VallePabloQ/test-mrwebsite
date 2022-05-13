# Errores encontrados y corregidos:

1.  El botón de adivinar no funcionaba debido a la línea `guessSubmit.addeventListener('click', checkGuess);` // Aqui solo teníamos un erros de sintaxis ya que solo debíamos cambiar `addeventListener` a `addEventListener`

2.  El programa no mostraba si el número era mayor o menor debido a la linea `const lowOrHi = document.querySelector('lowOrHi');` // esta contante estaba regresando un valor nulo porque no se estaba referenciando bien la clase del parrafo que mostraría el resultado. En este caso solo se debió agregar el '.' antes de la palabra "lowOrHi".

3.  El botón de reiniciar el juego no funcionaba debido a la línea `resetButton.addeventListener('click', resetGame);` // Aquí nuevamente teníamos un error de sintaxis, solo se cambio `addeventListener` por `addEventListener`

4.  La lógica del juego fallaba al momento de generar el número a adivinar, ya que después de 2 intentos el número a adivinar siempre era 1. Esto sucedía porque la función `Math.random()` nos regresa un número en decimales. Por lo que necesitamos redondearlo con `Math.floor()` y luego multiplicarlo por 100 para que devuelva un número entre 0 y 99. Pero lo que se está buscando es que devuelva un número entre 1 y 100 entonces solo le vamos a sumar 1 a nuestra función y ya nos quedaría de la siguiente manera: `Math.floor(Math.random()*100) + 1;`

5.  Después de 5 intentos el programa siempre muestra que ganamos. Esto se debía a que el programa estaba limitado a 5 intentos. También el programa decía que cuando se llegara al límite de intentos mostrara que habíamos ganado. Esto se arreglo aumentando el límite de intentos a 10.

6.  El programa aún mostraba que ganabamos cuando llegabamos al límite de intentos. Por lo que intercambié las condiciones `if(guessCount === ATTEMPS)` con `else if(userGuess === randomNumber)` para que la lógica de adivinar y calcular los intentos ahora si funcionara correctamente.

7.  El programa no reconocía cuando adivinabamos el número. La solución a esto fue meter `guessField.value` dentro de `Number()` para poder trabajar con números y no con texto que era lo que nos estaba mandando esa fución. Nos quedó de la siguiente  manera: `let userGuess = Number(guessField.value);`

8.  Los colores de cuando se ganaba o se perdía estaban al revés. Solo pase el color verde a cuando se adivinaba el número
`lastResult.textContent = 'Felicitaciones! adivinaste el número!';`
`lastResult.style.backgroundColor = 'green';`
El color rojo a cuando te pasas de intentos permitidos 
`lastResult.textContent = '!!!Pérdistes!!!';`
`lastResult.style.backgroundColor = 'red';` 
y el color negro a cuando aún no has adivinado el número.
`lastResult.textContent = 'Incorrecto! ';`
`lastResult.style.backgroundColor = 'black';`

9.  No estaba implementada la función de no permitir números decimales. Implementé esta función con un pequeño if y usando Math.floor() analicé el valor que traía la variable userGuess. Luego de eso ya no permitió el ingreso de decimales, pero aunque no las ingresara los decimales, los seguía contando como intentos. Lo unico que tuve que hacer es que dentro del if al detectar que un número era decimal, restara un intento, ya así la cantidad de intentos se mantenía igual. Quedó de la siguiente manera:
``if(guessCount === 1) {
      guesses.textContent = 'Número aleatorio anterior: ';
    }
    if (userGuess - Math.floor(userGuess) == 0) {
      guesses.textContent += userGuess + ' ';
    }else {
     alert ("No se aceptan decimales. Por favor ingresa un número entero!");
      guessCount--;
    }``
