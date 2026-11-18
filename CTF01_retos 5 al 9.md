Integrantes:
Álvaro Murcia González
Raúl Jurado Morales
Alejandro Quiñones


## Ficha 5 · Reto 5: otra huella distinta (SHA-1)

> **Enunciado.** La contraseña es `HashingIsOneWay2026`. Calcula su hash **SHA-1** y envía
> `flag{sha1}`.

**1. Tipo de reto:** X Hash ☐ Codificación ☐ Cifrado ☐ Combinado

```
Por que tenemos una contraseña y debemos obtener su huella mediante unas función HASH. No estamos cifrando ni codificando el texto
```

**2. Concepto.** *¿En qué se diferencia SHA-1 de MD5 en longitud de salida? ¿Se considera seguro
SHA-1 hoy? ¿Por qué?*

```
La diferencia entre ambos radica en que MD5 tiene 128 bits (32 caractéres hexadecimales) y SHA-1 tiene 160 bits (40 caractéres hexadecimales).
No, ni SHA-1 ni MD5 se consideran seguros a día de hoy por que no son resistentes a colisiones. 
```

**3. Procedimiento.** Comando exacto y explicación de cada parte:

| Parte del comando | Qué hace |
|---|---|
| echo | Muestra el texto|
| -n | Evitar añadir un salto de linea |
| \| | Envia el texto como entrada al siguente comando |
| sha1sum | calcula el HASH SHA-1 del texto recibido |

**4. Por qué lo hacemos así.** *¿Por qué el guion y los espacios de la salida no forman parte de
la flag? Calculad también el MD5 de la misma contraseña y comparad las dos salidas.*

| Algoritmo | Hash obtenido | Nº de caracteres | Bits |
|---|---|---|---|
| MD5 |1374cfc99a0de192a72ea8f627304d52 | 32 | 128 |
| SHA-1 | 98666584dca50be8bfc35461f4eabe0e31b887ad | 40 | 160 |

```
Conclusión: Como podemos obsevar el HASH MD5 tiene un total de 32 caractéres hexadecimales (128 bits) mientras que el SHA-1 tiene 40 caractéres hexadecimales (160 bits)
```

**5. Uso de la IA**

| Pregunta que le hicimos | Qué aprendimos | ¿Se equivocó? ¿Cómo lo comprobamos? |
|---|---|---|
| Diferencias entre MD5 y SHA-1 | Que diferencia el MD5 al SHA-1 | No, haciendo la prueba con ambos HASH y comprobando que el resultado fuese diferente |

**6. Flag:** `flag{98666584dca50be8bfc35461f4eabe0e31b887ad}`

**7. Verificación**

```
Comprobación de que la longitud del HASH son exactamente 40 caracteres hexadecimales y que todas las letras se encuentran en minuscula
```

---

## Ficha 6 · Reto 6: el mensaje en otro alfabeto (hexadecimal)

> **Enunciado.** Decodifica la cadena hexadecimal `4b6572636b686f666673` y envía
> `flag{palabra}`.

**1. Tipo de reto:** ☐ Hash X Codificación ☐ Cifrado ☐ Combinado

```
...
```

**2. Concepto.** *¿Qué es el hexadecimal? ¿Qué caracteres puede contener? ¿Cuántos caracteres
hexadecimales hacen falta para representar un byte? ¿Protege la información o solo la
representa?*

```
- Es un sistema de numeración posicional en base 16 utilizado apliamente en informatica para representar datos binarios de una forma más compacta y legible para el ser humano.
- Utiliza 16 símbolos distintos: los dígitos numéricos del 0 al 9 (para representar los valores 0 a 9) y las letras de la A a la F (mayúsculas o minúsculas, para representar los valores del 10 al 15).
- Hacen falta exactamente 2 caracteres hexadecimales para representar un byte (8 bits). Cada carácter hexadecimal equivale a 4 bits (un nibble), por lo que $4 + 4 = 8\text{ bits} = 1\text{ byte}$.
- Solo la representa. El hexadecimal es un sistema de codificación, no de cifrado. No utiliza ninguna clave secreta; cualquiera que conozca el estándar (como la tabla ASCII/UTF-8) puede revertir la representación al instante sin dificultad.
```

**3. Procedimiento.** Comando o herramienta y explicación:

| Parte del comando o paso | Qué hace |
|---|---|
| echo - n | Envia la cadena hexadecimal a la salida estandar sin añadir un salto de linea al final |
| \| | Redirige la salida del comando echo como entrada al comando xxd |
| xxd | Herramienta de volcado hexadecimal que permite convertir datos entre binario/texto y hexadecimal |
| -r | Invierte la operación habitual: convierte desde formato hexadecimal hacia texto/binario plano |
| -p | Indica que la entrada es un flujo hexadecimal continuo y limpio (Sin direcciones de memoria ni columnas de formato)

**4. Por qué lo hacemos así.** *¿Cómo supisteis que estaba en hexadecimal? La cadena tiene 20
caracteres: ¿cuántas letras esperáis obtener y por qué? Relacionadlo con el caso guiado 4.*

```
- Porque la cadena tiene una longitud par (20 caracteres) y está compuesta exclusivamente por dígitos del 0 al 9 y letras comprendidas entre la a y la f (4b, 65, 72...), sin caracteres especiales como = o letras posteriores a la f (que indicarían Base64 u otras codificaciones).
- Se esperan obtener 10 letras (caracteres ASCII). Como cada byte (carácter estándar) se representa mediante 2 dígitos hexadecimales, dividimos la longitud total entre dos ($20 \div 2 = 10$).
- Tal como se vio en el Caso guiado 4 con Base64 (donde la contraseña obtenida era recuerdaquebase64NOescifrar), el hexadecimal demuestra que codificar no es cifrar. Al igual que Base64 transforma bloques binarios en caracteres ASCII legibles para su transporte, el hexadecimal solo cambia la representación de los datos. Ninguno de los dos utiliza una clave secreta, por lo que cualquier persona puede revertir el proceso de forma trivial sin comprometer la seguridad real de la información.
```

**Para investigar.** La palabra que obtenéis es el apellido de una persona que enunció un
principio muy importante en criptografía. *¿Quién era y qué dice ese principio?*

```
La palabra obtenida es "Kerckhoffs", apellido de Auguste Kerckhoffs, un criptográfico neerlandes del siglo XIX. En 1883 formulo el principo de Kerckhoffs que establece que: "Un criptosistema debe ser seguro, incluso si todo sobre el sistema, excepto la clave, es de conocimiento público". En otras palabras, la seguridad de un sistema criptográfico no debe de depender de mantener en secreto el algoritmo o el metodo utilizado, si no unicamente de mantener en secreto la clave 
```

**5. Uso de la IA**

| Pregunta que le hicimos | Qué aprendimos | ¿Se equivocó? ¿Cómo lo comprobamos? |
|---|---|---|
| Como decodificar una cadena hexadecimal limpia desde la terminal y cual es su relación con el principio criptográfico asociado | El uso de los parámetros -r y -p en xxd para leer cadenas hexadecimales sin formato y el significado histórico del principio de Kerckhoffs | No se equivocó; se comprobó verificando par por par en la tabla ASCII y confirmando que el resultado tiene 10 caractéres |

**6. Flag:** `flag{Kerckhoffs}`

**7. Verificación**

```
La cadena de 20 caractéres produce exactamente 10 caractéres, respetando la mayuscula inicial y el resto en minuscula
```

---
## Ficha 7 · Reto 7: Base… ¿cuál? (Base32)

> **Enunciado.** Decodifica la cadena en **Base32** `MRSWMZLOONQV6ZLOL5YHE33GOVXGI2LEMFSA====` y
> envía `flag{texto}`.

**1. Tipo de reto:** ☐ Hash X Codificación ☐ Cifrado ☐ Combinado

```
...
```

**2. Concepto.** *¿En qué se diferencia Base32 de Base64? Comparad el alfabeto y el relleno con
`=`.*

| | Base64 | Base32 |
|---|---|---|
| Caracteres que usa | 64 caractéres: Letras de la A-Z, a-z, números 0-9 y simbolos + /| 32 caractéres: Letras mayúsculas A-Z y números del 2 al 7 (omite 0,1,8 y 9 para evitar confusiones visuales con letras como la O-I y B) |
| Relleno | Como máximo dos signos igaules (= o ==) ya que trabaja en bloques de 4 caractéres (24 bits)| Hasta 6 signos iguales (=, ===, ====, ======) ya que trabaja en bloques de 8 caractéres (40 bits) |
| ¿Usa minúsculas? | Si (Distingue entre mayúsculas y minusculas) | No (El estándar solo emplea mayúsculas) |

**3. Procedimiento.** Comando exacto y explicación de cada parte:

| Parte del comando | Qué hace |
|---|---|
| echo -n | Envia la cadena codificada a la salida estandar sin añadir un salto de linea al final |
| \| | Redirige la salida del comando echo como entrada al siguiente comando |
| base32 | herramienta estándar de GNU Coreutils para codificar o decodificar datos en Base 32 |
| -d | Indica a la herremienta que debe realizar la operación inversa (decodificar de Base 32 a texto plano) |

**4. Por qué lo hacemos así.** *¿Qué os hizo sospechar que no era Base64? ¿Qué pasa si intentáis
decodificarla con `base64 -d`?*

```
- El relleno final: La cadena termina con cuatro signos igual (====). En Base64, el relleno máximo posible es de dos signos (==), por lo que ver cuatro signos juntas es un indicador inmediato de Base32.
- El alfabeto: Toda la cadena está escrita exclusivamente en letras mayúsculas (A-Z) y dígitos del 2 al 7, sin ninguna letra minúscula ni símbolos como + o /.
- El comando base64 -d arroja un error de entrada inválida (base64: entrada no válida o invalid input), ya que al encontrarse con más de dos signos = al final rompe la estructura de bloques de 4 caracteres que espera Base64 (y aunque ignorara el relleno, produciría datos binarios corruptos sin sentido legible).
```

**Para investigar.** *El texto obtenido es un principio de seguridad. ¿Qué significa? Poned un
ejemplo aplicado a un instituto.*

```
El principo de defensa en profundidad consiste en implementar múltiples capas de seguruidad independientes y superpuestas para proteger los sistemas y datos. De este modo, si un atacante logra vulnerar  o sortear una barrera, se encontrará con otras medidas que frenaran o detectaran la intrusion.
- Ejemplo aplicado a un instituto: Para proteger las notas y los datos personales de los alumnos en el servidor del centro no basta con tener solo una contraseña en la aplicación web. Se aplican varias capas: Un cortafuegos, segmentación mediante VLANs, autenticación con contraseñas robustas y doble factor y cifrado de la base de datos y copias de seguridad diarias.
```

**5. Uso de la IA**

| Pregunta que le hicimos | Qué aprendimos | ¿Se equivocó? ¿Cómo lo comprobamos? |
|---|---|---|
| ¿Cómo diferenciar visualmente una cadena Base32 de una Base64 y como decodificarlo? | Que la longitud del relleno (====) y la ausencia de minúsculas o los números 0, 1, 8, 9 delatan al algoritmo Base32 frente a Base64 | No se equivocó; se comprobó ejecutando tanto base32 (que devolvió el texto legible) como base64 -d (que devolvió error de formato). |

**6. Flag:** `flag{defensa_en_profundidad}`

**7. Verificación**

```
- Al ejecutar echo -n "MRSWMZLOONQV6ZLOL5YHE33GOVXGI2LEMFSA====" | base32 -d, el resultado es exactamente defensa_en_profundidad (22 caracteres en minúsculas separados por guiones bajos).

- La cadena original tiene una longitud de 40 caracteres, cumpliendo estrictamente con la estructura de bloques deel estándar RFC 4648 para Base32.
```

---

## Ficha 8 · Reto 8: el primer cifrado de la historia (ROT13)

> **Enunciado.** Descifra el texto `FrthevqnqCbeBfphevqnqAbShapvban`, cifrado con **ROT13**, y
> envía `flag{texto}`.

**1. Tipo de reto:** ☐ Hash ☐ Codificación x Cifrado ☐ Combinado

*¿Por qué esto sí es un cifrado y Base64 no lo era? ¿Cuál es la clave?*

```
Es un cifrado porque realiza una transformación matemática cuyo objetivo es ocultar el significado del mensaje mediante un parámetro secreto, a diferencia de Base64, cuyo único fin es cambiar el formato de representación de los datos usando un estándar público sin secreto alguno. En este caso, el algoritmo es el cifrado César y la clave es el desplazamiento 13. 
```

**2. Concepto.** *¿Qué es el cifrado César? ¿Qué es ROT13? ¿Por qué aplicar ROT13 dos veces
devuelve el texto original? ¿Qué relación tiene el 13 con un alfabeto de 26 letras?*

```
- Es un método de cifrado clásico por sustitución monoalfabética, en el que cada letra del texto original se reemplaza por otra que se encuentra un número fijo de posiciones más adelante en el alfabeto.

- Es un caso particular del cifrado César donde el desplazamiento fijo es exactamente de 13 posiciones.

- El alfabeto inglés estándar tiene 26 letras, y 13 es exactamente la mitad (26/2 = 13). Al desplazar una letra 13 posiciones hacia adelante y volver a desplazarla otras 13 posiciones, se avanza un total de 26 posiciones, dando la vuelta completa al alfabeto y regresando exactamente al carácter original. Por ello, es un cifrado simétrico e involutivo.
```

**3. Procedimiento.** Comando o herramienta y explicación:

| Parte del comando o paso | Qué hace |
|---|---|
| echo -n | Envía la cadena cifrada a la salida estándar sin añadir un salto de línea al final. |
| \| | Redirige la salida del comando echo como entrada para el comando tr. |
| tr | Herramienta de GNU Coreutils que sustituye o traduce caracteres de la entrada según dos conjuntos definidos. |
| 'A-Za-z' | Define el alfabeto original de entrada (todas las mayúsculas de la A a la Z y minúsculas de la a a la z). |
| 'N-ZA-Mn-za-m' | Define el alfabeto desplazado 13 posiciones (A se transforma en N, B en 0 ... hasta volver de Z a M), respetando mayúsculas y minúsculas. |

**4. Por qué lo hacemos así.** *¿Por qué el cifrado César es inseguro? ¿Cuántas claves posibles
tiene? ¿Cómo lo romperíais si no supierais que el desplazamiento es 13?*

```
- Es completamente inseguro porque su espacio de claves es diminuto: en un alfabeto de 26 letras solo existen 25 claves posibles. Además, al ser un cifrado de sustitución simple, mantiene intacta la frecuencia de aparicion de las letras del idioma original.

- Fuerza Bruta: Probar los 25 desplazamientos posibles en menos de un segundo mediante un pequeño script o herramienta y leer cuál de las 25 salidas tiene sentido en español.

Análisis de frecuencias: En textos largos, basta con contar que létra aparece más veces y calcular la distancia hasta esa letra para deducir el desplazamiento.
```

**Para investigar.** *El texto descifrado está relacionado con el reto 6. ¿Qué relación tiene con
el principio de Kerckhoffs?*

```
Esto conecta directamente con el Principìo de Kerckhoffs visto en el Reto 6: confiar la protección de un sistema únicamente a que nadie descubra el mecanismo o algoritmo utilizado es un error grave. Según Kerckhoffs, el algoritmo debe asumirse público y la seguridad real debe recaer exclusivamente en una clave robusta y secreta.
```

**5. Uso de la IA**

| Pregunta que le hicimos | Qué aprendimos | ¿Se equivocó? ¿Cómo lo comprobamos? |
|---|---|---|
| ¿Cómo descifrar ROT13 con tr y por qué ROT13 es su propia función inversa? | Que 'A-Za-z' 'N-ZA-Mn-za-m' mapea directamente las dos mitades del alfabeto inglés de 26 letras, haciendo que cifrar y descifrar sean exactamente la misma operación. | No se equivocó; se comprobó obteniendo el mensaje coherente SeguridadPorOscuridadNoFunciona y verificando manualmente las primeras letras. |

**6. Flag:** `flag{SeguridadPorOscuridadNoFunciona}`

**7. Verificación.** *Volved a aplicar ROT13 al resultado. ¿Qué obtenéis?*

```
Se obtiene exactamente la cadena cifrada original del enunciado: FrthevqnqCbeBfphevqnqAbShapvban, demostrando la propiedad simétrica e involutiva de ROT13.
```

---

## Ficha 9 · Reto 9: capa sobre capa (combinado) ⭐

> **Enunciado.** La cadena `NTA2NTZlNzQ2NTczNzQ2OTZlNjc0NTc0Njk2MzZm` está en **Base64**. Al
> decodificarla obtendrás **hexadecimal**; al decodificar este, una **palabra**. Calcula el
> **MD5** de esa palabra y envía `flag{md5}`.

**1. Tipo de reto:** ☐ Hash ☐ Codificación ☐ Cifrado x Combinado

*¿Qué técnicas de los retos anteriores se combinan?*

```
Se combinan dos técnicas de codificación (Base64 y Hexadecimal) seguidas de una función hash (MD5).
```

**2. Concepto.** *¿Por qué se usan varias capas de codificación? ¿Hace eso la información más
segura?*

```
- Se emplean habitualmente en retos de ciberseguridad o en la transmisión de datos para empaquetar información, ocultarla a simple vista o simular escenarios de análisis forense y desensamblado.

- No, al tratarse exclusivamente de capas de codifición sin claves secretas asociadas, no aportan seguridad criptográfica real. Cualquier persona que identifique los formatos puede deshacer las capas una a una de forma totalmente trivial.
```

**3. Procedimiento.** Completad la tabla con cada capa:

| Capa | Lo que tenéis | Cómo reconocéis el formato | Comando | Resultado |
|---|---|---|---|---|
| 1 | `NTA2NTZl…` | Mezcla de letras mayúsculas, minúsculas y números, con una longitud múltiplo de 4 y sin relleno = extraño. Formato Base64. | 'echo -n "NTA2NTZlNzQ2NTczNzQ2OTZlNjc0NTc0Njk2MzZm" /| base64 -d ' | 50656e74657374696e67457469636f |
| 2 | 50656e74657374696e67457469636f | Cadena de longitud par compuesta únicamente por dígitos del 0 al 9 y letras de la a a la f. Formato Hexadecimal | 'echo -n "50656e74657374696e67457469636f" /| xxd -r -p' | PentestingEtico |
| 3 | PentestingEtico | Palabra en texto plano resultante de decodificar el hexadecimal | 'echo -n "PentestingEtico" /| md5sum' | c784ae85751ffee70b053ec8ea30c92a |

**4. Por qué lo hacemos así.** *¿Cómo decidisteis el orden de las capas? ¿Qué pasaría si
intentarais decodificar el hexadecimal antes que el Base64?*

```
- Siguiendo el enunciado y la regla de oro al desapilar capas: se deshacen en orden inverso al que fueron aplicadas. Primero retiramos la capa más externa (Base64) para destapar la cadena intermedia, y después procesamos la capa interna (Hexadecimal) para revelar el texto plano.

- La cadena Base64 inicial contiene caracteres y combinaciones que no forman un flujo hexadecimal válido (o arrojaría un error de formato al intentar interpretarlo directamente como bytes hexadecimales).
```

**5. Uso de la IA**

| Pregunta que le hicimos | Qué aprendimos | ¿Se equivocó? ¿Cómo lo comprobamos? |
|---|---|---|
| ¿Cómo estructurar la decodificación en cadena de Base64 a Hexadecimal y luego aplicar MD5? | A encadenar correctamente los comandos y enternder el flujo inverso de las capas de codificación | No se equivocó; se comprobó paso a paso validando que la salida de cada comando correspondía exactamente al formato esperado antes de pasar a la siguiente capa.|

**6. Flag:** `flag{c784ae85751ffee70b053ec8ea30c92a}`

**7. Verificación**

```
- Verificamos que al aplicar base64 -d sobre la cadena original obtenemos un texto hexadecimal válido de 20 caracteres.

- Al aplicar xxd -r -p sobre dicho hexadecimal, obtenemos exactamente la palabra legible.

- Finalment. al calcular el resumen MD5 de dicha palabra, obtenemos el hash exacto que conforma la flag final.
```

---

## Reflexión final del equipo (opcional, se valora en «Uso reflexivo de la IA»)

*En 5 a 10 líneas: ¿en qué momento la IA os ayudó a entender algo? ¿Os dio alguna respuesta
incorrecta que supisteis detectar? ¿Cómo lo hicisteis?*

```
Durante la realización de esta práctica, la asistencia de la IA fue clave para comprender la distinción exacta entre codificación, cifrado y funciones hash, así como para automatizar pequeños comandos sin errores sintácticos. No se detectaron respuestas incorrectas relevantes; cada paso intermedio se contrastó analizando la longitud de las cadenas y las salidas de los comandos base64, sha1sum y xxd. Esto nos permitió comprobar de forma empírica conceptos teóricos como el Principio de Kerckhoffs y la diferencia entre seguridad real y simple oscuridad de formatos.
```

---