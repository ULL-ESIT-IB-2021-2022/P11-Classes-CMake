# Práctica 11. Introducción a la Programación Orientada a Objetos. Clases. La herramienta CMake.

# Factor de ponderación: 9

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Desarrolle programas sencillos en C++ utilizando clases, así como todas las características del lenguaje estudiadas anteriormente
* Conozca la herramienta CMake y sepa usarla para construir sus programas ejecutables
* Incluya en sus programas comentarios adecuados en el formato requerido por Doxygen
* Profundice en el uso de funciones en sus programas.
* Aloje todo el código fuente de sus programas en repositorios privados de GitHub
* Sepa depurar sus programas usando la interfaz de depuración del VSC


### Rúbrica de evaluacion de esta práctica
Todo el código que se presente a evaluación ha de cumplir los estándares definidos en la 
[Guía de Estilo de Google para C++](https://google.github.io/styleguide/cppguide.html).

Se señalan a continuación otros aspectos (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica.
El alumnado ha de acreditar que:

* Conoce los conceptos expuestos en el material de referencia de esta práctica.
* Ha realizado todos los ejercicios propuestos, así como que es capaz de desarrollar otros de complejidad similar.
* Es capaz de escribir un fichero CMakeLists.txt para automatizar el proceso de compilación de sus programas.
* Todos sus programas se estructuran en directorios diferentes para cada "proyecto" haciendo que cada uno de
  ellos contenga un fichero `CMakeLists.txt` con la configuración de despliegue del proyecto.
* Todas las prácticas realizadas hasta la fecha se encuentran alojadas en repositorios de
[GitHub](https://github.com/).
* Los programas deben contener comentarios adecuados en el formato requerido por 
  [Doxygen](https://www.doxygen.nl/index.html).
* Sus programas se compilan correctamente utilizando la utilidad `make` y un fichero `Makefile`.
* Todos los identificadores que utilice en su programa (constantes, variables, etc.) deberán ser
  siempre significativos. No utilice nunca identificadores de una única letra, tal vez con la excepción de las variables que utilice para iterar en un bucle.
* Sabe editar y modificar sus programas usando VSC con una conexión remota a la máquina virtual Linux de la asignatura.
* Ha realizado todos sus ejercicios en la máquina virtual Ubuntu de la asignatura.
* Todos los programas que desarrolla, antes de su ejecución imprimen en pantalla un mensaje indicando la finalidad del programa así como la información que precisará del usuario para su correcta ejecución.
* Todos sus programas contienen comentarios adecuados en el formato requerido por Doxygen.
* Todos los ficheros de código del proyecto correspondiente a esta práctica están alojados en un repositorio
  de GitHub
* Conoce las técnicas básicas de depuración usando VSC y su depurador integrado.

### La herramienta `cmake`
[CMake](https://es.wikipedia.org/wiki/CMake)
es lo que se conoce como un sistema de metaconstrucción. 
No se utiliza para construir (generar, *build* en inglés) el programa ejecutable de una aplicación sino
que produce ficheros de proyecto nativos para la plataforma de destino. 
Por ejemplo, CMake en Windows generará una solución para Visual Studio; 
en Linux generará un fichero Makefile; 
en macOS generará un proyecto para XCode y así sucesivamente. 
Eso es lo que la palabra *meta* indica: CMake construye sistemas de construcción 
(*builders*). 
La herramienta `make` es un sistema de construcción, posiblemente el más común.

Un proyecto basado en CMake siempre contiene un fichero `CMakeLists.txt`
que describe cómo se estructura el proyecto, la lista de ficheros 
de código fuente que se ha de compilar, lo que CMake debe generar a partir de él y así sucesivamente. 
Se trata en definitiva de un fichero de configuración para la herramienta CMake.
CMake leerá las instrucciones de ese fichero y producirá el resultado deseado. 

Una característica positiva de CMake es el llamado "out-of-source build". 
Cualquier fichero requerido para la construcción final, incluyendo los ejecutables, 
será almacenado en un directorio de construcción separado (habitualmente llamado `build/`). 
Esto evita que el directorio de origen que contiene el código fuente se llene de 
ficheros no deseados y hace que sea fácil volver a empezar: sólo hay que eliminar 
el directorio destino de la compilación (directorio `build`) y listo.

CMake es una herramienta muy potente que admite multitud de opciones.
En 
[la documentación](https://cmake.org/cmake/help/latest/index.html) 
de la herramienta se pueden estudiar en profundidad estas opciones, pero para la utilización que perseguimos
realizar en esta asignatura bastará con que estudie detenidamente 
[este breve tutorial](https://www.internalpointers.com/post/modern-cmake-beginner-introduction).

En el directorio raíz del repositorio de esta práctica hallará un subdirectorio `fibonacci_sum` con el
siguiente contenido:

```
  fibonacci_sum
  ├── CMakeLists.txt             // Fichero de configuración para CMake
  ├── doc                        // Documentación
  ├── fibonacci.Doxyfile         // Fichero de configuración para Doxygen
  ├── LEE_ME.txt
  └── src                        // Código fuente de la aplicación
      ├── fibonacci_main.cc
      ├── fibonacci_sum.cc
      ├── fibonacci_sum.h
      ├── tools.cc
      └── tools.h
```
Esa estructura de directorios (a la que se añadirán los directorios `build` y -opcionalmente `lib`-)
es habitual en proyectos de desarrollo de software.
En este ejemplo se ha tomado la aplicación `fibonacci_sum` que calcula la suma de términos pares de la serie
de Fibonacci y se ha fragmentado la aplicación en 5 ficheros de código (`*.cc` y `*.h`).
El fichero de configuración `CMakeLists.txt` contiene la configuración que se utiliza para el despliegue de la
aplicación.
Al efecto de ilustrar este proceso, se crea una librería `libtools.a` que se aloja en el directorio `lib`. 
El programa binario (`fibonacci_sum`) se construye enlazando esta librería con el resto del código objeto
producto de la compilación.

Para construir la aplicación, siga los siguientes pasos (que son los habituales):
```
$ cd fibonacci_sum
$ mkdir build
$ cd build
$ cmake ..
$ make
```

El comando `cmake`, usando el fichero de configuración `CMakeLists.txt`, creará en el directorio `build` el fichero `Makefile`
que utiliza el comando `make` para construir la aplicación, cuyo programa binario `fibonacci_sum` se crea
asimismo en el directorio `build`.

Experimente con este fichero de configuración entregado, `CMakeLists.txt` para adaptarlo a cada uno
de sus propios proyectos (ejercicios de la práctica).
No es necesario en principio, que construya librerías propias para sus programas.
La construcción de una librería se ha incluído en este ejemplo con la finalidad de ilustrar ese proceso.

### Trabajo previo
Antes de realizar los ejercicios de esta práctica, estudie detenidamente el Capítulo 12 (epígrafes 12.1-12.15) del
[tutorial learncpp](https://www.learncpp.com/cpp-tutorial/81-welcome-to-object-oriented-programming/).
Muchos de los ejemplos de ese tutorial son los mismos que se utilizan en las clases de la asignatura,
cuyo material (transparencias y códigos de ejemplo) debiera Ud. también estudiar.

### Ejercicios
* Al realizar los ejercicios cree dentro de su repositorio de esta práctica un directorio diferente
con nombre significativo (personas, rectangulos, circulos p. ej.) para cada uno de ellos 
y con un contenido similar al que se ha entregado para la aplicación de ejemplo `fibonacci_sum`.
* Tómese como ejemplo el primero de los ejercicios y haga que cada uno de sus programas conste de 3 ficheros:
  * Un fichero `personas.cc` (programa principal) que contendrá la función `main` e incluirá el fichero de cabecera `persona.h`.
  * El fichero `persona.h` que contendrá las declaraciones correspondientes a la clase `Persona`.
  * El fichero `persona.cc` que contendrá el código (definiciones) correspondientes a la clase `Persona`.
  * Obviamente si el programa principal (`personas.cc`) utiliza otras clases, debería incluir (`#include`) los
  correspondientes ficheros de cabecera.
  * Modifique estos nombres de ficheros para adaptarlos al ejercicio en cuestión.
* La compilación del programa correspondiente a cada ejercicio se automatizará con un fichero `CMakeLists.txt`
que se utilizará con `cmake`.
Así pues, la estructura de directorios y sus contenidos correspondiente al primero de los ejercicios
propuestos sería la siguiente:
```
personas
    ├── build           // Directorio inicialmente vacío para alojar el programa ejecutable
    ├── CMakeLists.txt  // Fichero de configuración para cmake
    └── src             // Directorio contenedor del código fuente del ejercicio
        ├── persona.cc
        ├── persona.h
        └── personas.cc
```
* Desarrolle cada ejercicio de forma incremental, probando cada una de las funciones que va Ud.
desarrollando. 
* Utilice el depurador integrado de VSC para depurar los programas de modo que funcionen correctamente.
* Todos estos programas han de tomar su entrada (si es que hay alguna) como parámetros pasados por línea de comandos.

1. Desarrolle una clase `Persona` cuyos objetos han de contener al menos atributos para representar nombre,
apellidos y la edad de la persona.
Incluya asimismo un método *Print()* que permita imprimir en pantalla la información de una instancia de la
clase.

2. Desarrolle una clase `Rectangulo` que contemple como atributos la anchura y altura del rectángulo.
Incluya métodos que permitan calcular el área y el perímetro del rectángulo representado y un método
*Display()* que permita mostrar la información correspondiente a un objeto rectánculo de la clase.

3. Desarrolle una clase `CuentaBancaria` que contemple como atributos 
* El número de la cuenta (20 dígitos)
* El nombre del titular
* El saldo de la cuenta

Incluya asimismo al menos los siguientes métodos:
* Un constructor que tome como parámetros el el número de cuenta, el titular y el saldo
* *Depositar* que permita aumentar el saldo de la cuenta en una cierta cantidad
* *Extraer* que permita retirar una cierta cantidad de dinero
* *Mostrar* que permita mostrar los detalles de la cuenta
* *Impuestos* que calcule un impuesto del 5% sobre el saldo de la cuenta

4. Desarrolle una clase `Point2D` para representar puntos en el espacio bidimensional a través de sus
coordenadas. 
Incluya al menos los siguientes métodos:
* *Show()* para mostrar en pantalla las coordenadas del punto
* *Move* para cambiar las coordenadas del punto
* *Distance* para calcular la 
[distancia](https://www.mathwarehouse.com/algebra/distance_formula/index.php)
entre dos puntos
* *Middle* para calcular el 
[punto medio](https://en.wikipedia.org/wiki/Midpoint)
del segmento que une dos puntos

5. Diseñe una clase `Circulo` que permita representar círculos utilizando como atributos el centro 
y el radio del círculo.
Incluya métodos *Area*, *Perimetro* y *Print* que permitan respectivamente calcular el área, el perímetro del
círculo así como imprimir en pantalla la información relativa al círculo en cuestión.
Incluya asimimsmo un método *EsInterior* que determine si un punto del espacio cartesiano `(x, y)` está o no
dentro del círculo.

6. La clase Fecha.

Desarrolle una clase `Fecha` que permita representar y gestionar fechas.
Incorpore en la clase los miembros de datos y métodos que considere adecuados para la finalidad que se
persigue en este ejercicio.
Incluya un método que permita determinar si el año correspondiente a una fecha es un año bisiesto o
no.
Realice un programa cliente `fechas.cc` que tome como parámetro una fecha, un número y un nombre de fichero:
```
./fechas - Gestión de fechas
Modo de uso: ./fechas dd/mm/aa N fichero_salida.txt
Pruebe ./fechas --help para más información
```
El programa deberá imprimir en el fichero de salida (tercer parámetro) las N (segundo parámetro) fechas cronológicamente posteriores a la
introducida (primer parámetro) con una separación de un día entre fechas sucesivas.

7. La clase Complejo.

Todo
[número complejo](https://es.wikipedia.org/wiki/N%C3%BAmero_complejo)
puede representarse como la suma de un número real y un número imaginario, de la forma `a + bi` donde el
término `a` es la parte real, `b` la parte imaginaria e `i` la
[unidad imaginaria](https://es.wikipedia.org/wiki/Unidad_imaginaria).

En este ejercicio se propone desarrollar una clase `Complejo` que permita operar con números complejos.

Separe el diseño de su clase `Complejo` en dos ficheros, `complejo.h` y `complejo.cc` conteniendo
respectivamente la declaración y la definición de la clase.
Siga las indicaciones del tutorial 
[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
para realizar esta separación de su clase en dos ficheros.
Siga igualmente las indicaciones del tutorial 
[Header guards](https://www.learncpp.com/cpp-tutorial/header-guards/)
para incluir (siempre de ahora en adelante) *header guards* (guardas de cabecera) en sus ficheros de
definiciones (`*.h`) de modo que se evite la inclusión múltiple del mismo fichero.

Desarrolle un programa cliente `complejos.cc` que permita operar con números complejos y haga uso
de la clase `Complejo` que diseñe.
La clase `Complejo` ha de contener al menos métodos que permitan (*print()*) imprimir un número 
complejo así como sumar (*Add()*) y restar (*Sub()*) números complejos.
Así la función *main* del programa `complejos.cc` podría contener sentencias como las siguientes:

```
main() {
  Complejo complejo1{4, 5}, complejo2{7, -8};
  Complejo resultado;
  resultado = add(complejo1, complejo2);
  resultado.print();
  resultado = sub(complejo1, complejo2);
  resultado.print();
}
```
que imprimirían en pantalla los resultados de la suma y referencia de números complejos indicada.

Incluya (discrecionalmente) cualesquiera otras operaciones que considere adecuadas como métodos en la clase
`Complejo`.

8. La clase Racional.

Un 
[número racional](https://en.wikipedia.org/wiki/Rational_number)
tiene un numerador y un denominador de la forma `p/q` donde `p` es el numerador y `q` el denominador.
Por ejemplo, 1/3, 3/4 y 10/4 son números racionales.

Un número racional no puede tener denominador 0, pero sí puede ser cero el numerador.
Todo número entero `n` es equivalente al racional `n/1`.
Los números racionales se utilizan en cálculos precisos que involucran fracciones.
Por ejemplo, `1/3 = 0.33333 ...`.
Este número no puede ser representado de forma precisa en formato de punto flotante utilizando los tipos float o double.
Para obtener resultados precisos es conveniente usar números racionales.

C++ dispone de tipos de datos para enteros y números en punto flotante, pero no para racionales.
En este ejercicio se propone el diseño de una clase para representar números racionales.

Desarrolle un programa cliente `racionales.cc` que permita operar con números racionales y haga uso
de la clase `Racional` que ha de diseñarse.

Las siguientes deben tomarse como especificaciones del programa a desarrollar:
* Separe el diseño de su clase `Racional` en dos ficheros, `racional.h` y `racional.cc` conteniendo
  respectivamente la declaración y la definición de la clase.
* La clase `Racional` incluirá al menos métodos para:
    * Crear objetos de tipo `Racional`. Se debe implementar un constructor por defecto y uno parametrizado.
    * Escribir un objeto de tipo `Racional`.
    * Leer un objeto de tipo `Racional`.
    * Sumar dos objetos de tipo `Racional`.
    * Restar dos objetos de tipo `Racional`.
    * Multiplicar dos objetos de tipo `Racional`.
    * Dividir dos objetos de tipo `Racional`.
    * Comparar objetos de tipo `Racional`.
* El programa ha de permitir leer un fichero de texto en el que figuran pares de números racionales
separados por espacios de la forma:

```
a/b c/d
e/f g/h
  ...
```

y para cada par de números racionales, el programa ha de imprimir en otro fichero de salida todas las operaciones posibles
con cada uno de los pares de números del fichero de entrada, de la forma:

```
a/b + c/d = n/m
  ...
```

Si el programa se ejecuta sin pasar parámetros en la línea de comandos, debemos obtener el siguiente mensaje:

```
./racionales -- Números Racionales
Modo de uso: ./racionales fichero_entrada fichero_salida
Pruebe ./racionales --help para más información
```

Si el programa se ejecuta pasando como parámetro la opción `--help` se ha de obtener:

```
./racionales -- Números Racionales
Modo de uso: ./racionales fichero_entrada fichero_salida 

fichero_entrada: Fichero de texto conteniendo líneas con un par de números racionales: `a/b c/d` separados por un espacio
fichero_salida:  Fichero de texto que contendrá líneas con las operaciones realizadas: `a/b + c/d = n/m`
```

### Referencias
* [CMake](https://es.wikipedia.org/wiki/CMake)
* [Introduction to modern CMake for beginners](https://www.internalpointers.com/post/modern-cmake-beginner-introduction)
* [Welcome to object-oriented programming - Tutorial learnCPP](https://www.learncpp.com/cpp-tutorial/81-welcome-to-object-oriented-programming/).
* [Números complejos](https://es.wikipedia.org/wiki/N%C3%BAmero_complejo)
* [Rational Number](https://en.wikipedia.org/wiki/Rational_number)
*	[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
* [Header guards](https://www.learncpp.com/cpp-tutorial/header-guards/)
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
* [Comments](https://google.github.io/styleguide/cppguide.html#Comments)
* [Documenting C++ Code](https://developer.lsst.io/cpp/api-docs.html)
* [Doxygen](https://en.wikipedia.org/wiki/Doxygen)
