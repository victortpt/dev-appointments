# dev-appointments

## Npm

Sistema de gestor de paquetes por defecto de Node.js

El fichero `package.json` es donde se indican las versiones de los paquetes y sus dependencias.

El fichero `package-lock.json` es interno del proyecto y las versionas estan encadenadas al proyecto en cuestión (lock).

--------

### npm basic commands

npm install
```
npm i
```

npm update
```
npm update
```

npm run: aqui se ejecutara lo que estea definido en el proyecto. P.E.: en el proyecto de Vue para hacer un arranque en servidor local:
```
npm run serve
```

--------

### npm audit

Herramienta de auditorias de vulnerabilidades del gestor npm

```bash
npm audit
```

*npm audit fix*

Esta opción se utlizará cuando tengamos vulnerabilidades en nuestras dependencias y querramos resolverlas de forma automática.

```bash
npm audit fix
```

En el caso de no poder llegar a resolverlas, se podrá optar por el flag `--force` el cual nos hará cambios bruscos (breaking changes) y por lo tanto podría dar problemas en el proyecto.

```bash
npm audit fix --force
```

*Trucos npm audit*

- Si necesitamos filtrar la salidad del audit podemos hacer un grep

```
npm audit | grep -E "(Severity: critical)" -B3 -A10
```

- Si queremos obtener difrentes nivel de vulnerabilidad: --audit-level=[nivel]

```
npm audit --audit-level=high
```

- Mostrar la información en formato json con la opción --json

```
npm audit --json --audit-level=high
```

- Resolución de vulnerabilidades cuando npm fix audit no llega

En varias ocasiones al detectar vulnerabilidades con un npm audit fix no es suficiente, por lo que deberás utilizar la opción `--force`. Esta hace que puedan romper dependencias entre paquetes y te dea problemas, pero si quieres llegar a resolver las vulnerabilidades puede ser una opción
```
npm audit fix --force
```
Si con esto no es suficiente, es posible que te dea el problema de `the upstream dependency conflict installing NPM packages`, que viene a decir que deberás resolverlo a mano. En el caso del proyecto de Vue donde estoy trabajando, modifiqué en el `package.json` la version donde estoy trabajando del plugin de babel a la 5.0.0.
```
"devDependencies": {
    "@vue/cli-plugin-babel": "~5.0.0",
    "@vue/cli-service": "^5.0.8",
    "babel-eslint": "^10.0.3",
    "cordova-plugin-whitelist": "^1.3.4",
    "ejs": "^3.1.8",
    "eslint": "^6.7.2",
    "eslint-plugin-vue": "^6.1.2",
    "loader-utils": "^3.2.0",
    "stylus": "^0.54.5",
    "stylus-loader": "^3.0.1",
    "vue-cli-plugin-vuetify": "~0.5.0",
    "vue-template-compiler": "^2.6.11",
    "vuetify-loader": "^1.0.5"
  },
```

Despues borraremos el directorio de `node_modules` y el fichero `package-lock.json` y seguidamente volveremos a ejecutar un `npm install`

--------

## Python

## Guía desarrollo Python

{{toc}}


### Información básica de Python

Python es un lenguaje interpretado que destaca por su sencilla sintaxis y legibilidad de código. Su uso se extiende a todo tipo de aplicaciones: pequeños scripts, APIs, aplicaciones web... Destacando en el mundo del dato, donde junto con R y SQL para el manejo de datos, es el rey indiscutible. También goza de popularidad en campos de vanguardia como la IA, el Big Data o la automatización (bots, webscrapping...)

El hecho de que sea un lenguaje interpretado hace que su uso se adecúe más a unos escenarios que  a otros. A continuación se analizan las ventajas y desventajas entre compilado y interpretado:

!clipboard-202211111118-mgegz.png!

### Variables

Las variables (y funciones) en Python siguen la nomenclatura denominada *snake_case* que se caracteriza por usar todo minúsculas y las palabras con sentido completo separadas por undersocre *_*

!clipboard-202211140828-pnmd1.png!

!clipboard-202211140828-ez5qt.png!

!clipboard-202211140828-rpd1q.png!


#### Integers

* Un integer o entero es un tipo primitivo de variable numérica que solo consta de parte entera.
* Se le pueden asignar valores positivos y negativos
* A diferencia de otros lenguajes, Python asigna memoria a las variable dinámicamente así que en principio podremos asignarle el valor que queramos con la única limitación de memoria de la máquina.

Se declara de la siguiente forma: nombre_variable = {valor}. Algunos ejemplos:

<pre><code class="python">
a = 3
b = 0b100
c = 0x17
d = 0o720
e = 1_000
print(a, type(a)) #3 <class 'int'>
print(b, type(b)) #4 <class 'int'>
print(c, type(c)) #23 <class 'int'>
print(d, type(d)) #464 <class 'int'>
print(e, type(e)) #1000 <class 'int'>
</code></pre>

#### Floats

* Un float o flotante es un tipo primitivo de variable numérica que cuenta con parte decimal.
* Se le pueden asignar valores positivos y negativos
* Se almacena de una forma particular, denominado en coma flotante. Se explica en el estándar IEEE 734 (https://en.wikipedia.org/wiki/IEEE_754)

Se declara de la siguiente forma: nombre_variable = {valor}. Algunos ejemplos:
<pre><code class="python">
a = 2.5
b = -0.4
c = .4
d = 4.
e = 3E8
print(a, type(a)) #2.5 <class 'float'>
print(b, type(b)) #-0.4 <class 'float'>
print(c, type(c)) #0.4 <class 'float'>
print(d, type(d)) #4.0 <class 'float'>
print(e, type(e)) #300000000.0 <class 'float'>
</code></pre>

#### Strings

* Un string o cadena es un tipo primitivo *inmutable* donde almacenamos secuencias de caracteres.
* Tampoco tienen un límite de tamaño.
* Importante el uso de las comillas a la hora de declarar, que pueden ser *dobles* " o *simples* '

Se declara de la siguiente forma: nombre_variable = {"valor"}. Algunos ejemplos:

<pre><code class="python">
str1 = "hello"
str2 = 'hello'
str3 = r"long live metal \m/" # raw string
str4 = f"{str1}. I would like to say {str3}" # string interpolation
str5 = "This is a message for {}".format("John") # string format
str6 = """
This is a here-doc string with
multiple lines
"""
str7 = str4[6:8] # string slice
</code></pre>

* Caracter de escape para introducir una comilla dentro: \" y para salto de línea: \n
* *Formateo de strings*: Podremos usar el operador *+* para concatenar otras cadenas o numeros, casteándolos utilziando *str(<obj>)* . También podremos formatear usando el operador *%* o usando .format.
* *Ejemplos de formateo*:

<pre><code class="python">
s = "Esto es una comilla doble \" de ejemplo" # Esto es una comilla doble " de ejemplo
x = 5
s = "El número es: " + str(x) #El número es: 5
s = "Los números son %d y %d." % (5, 10) #Los números son 5 y 10.
s = "Los números son {} y {}".format(5, 10) #Los números son 5 y 10.
</code></pre>

#### Booleans

Tipo de datos booleano que en Python se define de la siguiente forma:
<pre><code class="python">
boolean_truthy = True
boolean_falsy = False
</code></pre>

#### Lists

* Estructura de datos que permiten almacenar un conjunto arbitrario de datos. Esto es, a diferencia de otros lenguajes, pueden contener datos de otros tipos en la misma lista.
* Propiedades:
1. Son ordenadas, mantienen el orden en el que han sido definidas
2. Pueden ser formadas por tipos arbitrarios
3. Pueden ser indexadas con [i].
4. Se pueden anidar, es decir, meter una dentro de la otra.
4. Son mutables, ya que sus elementos pueden ser modificados.
6. Son dinámicas, ya que se pueden añadir o eliminar elementos.
* Se puede declarar con los símbolos *[]* y separando sus elementos por comas. Veamos unos ejemplos

<pre><code class="python">
list1 = [1, 2 , 3, 4, 5]
list2 = [1, "two", 3]   # multiple types
list3 = list1 + list2 # list concatenation

# Listas encadenadas
x = [1, 2, 3, ['p', 'q', [5, 6, 7]]]
print(x[3][0])    #p
print(x[3][2][0]) #5
print(x[3][2][2]) #7
</code></pre>


* Acceso a elementos de una lista

<pre><code class="python">
first_element = list1[0]
last_element = list1[-1]
</code></pre>

* Métodos principales: append(<obj>), extend(<iterable>), insert(<index>, <obj>), remove(<obj>), pop(index=-1), reverse(), sort(), index(<obj>)...

#### List Comprehensions

Las  list comprenhension es una funcionalidad de python que nos permite crear listas sobre la marcha implementando la lógica en la misma expresión de declaración. Un ejemplo de esto:

<pre><code class="python">
my_list = [i+1 for i in range(5)] # [1,2,3,4,5]
</code></pre>

#### Sets

Los sets son similares a las listas, con la diferencia de que *no puede haber elementos duplicados*. Además son *desordenados* y sus elementos *inmutables*. Algunos ejemplos:

<pre><code class="python">
set1 = {1, 2, 3, 4, 5}
set2 = {1, 1, 2, 2, 3, 3, 4} # print(set2) => {1, 2, 3, 4}
print(set1 & set2)   # {1, 2, 3, 4} intersección
print(set1 - set2) # {5} diferencia, objetos no incluidos en set2
print(set1 | set2) # {1, 2, 3, 4, 5} unión, elementos que pertenecen al menos a uno de los conjuntos
</code></pre>

#### Tuples

Las tuples o tuplas son similares a las listas, con la diferencia de que son *inmutables*. Una vez declaradas no pueden ser modificadas. Algunos ejemplos:
<pre><code class="python">
ted = "Ted", "Neward", 46
print(ted) # {"Ted", "Neward", 46}
charlotte = ("Charlotte", "Neward", 39)
first, last, age = charlotte # de-estructuración de objeto
print(first) # Charlotte
</code></pre>

#### Dictionaries

Colección de elementos, donde cada uno de ellos está compuesto por una llave (key) y una valor (value).
 
* Se declaran con los símbolos *{}* y los elementos separados por comas en el formato key:value

Propiedades de los dict:
* *Dinámicos*: pueden crecer o decrecer, se pueden añadir o eliminar elementos.
* *Indexados*: los elementos del diccionario son accesibles a través del key.
* *Anidados*: un diccionario puede contener a otro diccionario en su campo value.

Acceso y modificación de elementos:

* Se puede acceder utilizando *[]* o la función *get()*
* Para todas las llaves con *keys()*
* Para todas los valores con *values()*
* Para todas los elementos con *items()*

<pre><code class="python">
dict1 = {"captain": "Antilles"}
dict1["admiral"] = "Ackbar"
k = dic1.keys()
v = dict1.values()
kv = dict1.items()
another_dict = dict(name="Ted", age=19)
print(another_dict) # {'name': 'Ted', 'age': 19}
</code></pre>

#### Arithmetic operators

+, -, *, / (siempre produce un float como resultado)
 // (integer division, redondeo por abajo)
% (módulosobre integer division)
** (usa right-sided binding)


!clipboard-202211140828-cliur.png!

#### Dates 

En python no tenemos un tipo de dato date como tal, sino que importamos un módulo llamado *datetime* para trabajar con fechas

<pre><code class="python">
import datetime

x = datetime.datetime.now()
y = datetime.datetime(2020, 5, 17)
print(x)
print(y)
</code></pre>

### Functions

* Function names should be lowercase, with words separated by underscores as necessary to improve readability.
* Variable names follow the same convention as function names.

* Argumentos por posición

<pre><code class="python">
def introduction(first_name, last_name):
    print("Hello, my name is", first_name, last_name)

introduction( "James", "Bond")
</code></pre>

* Argumentos por palabra clave (keyword)

<pre><code class="python">
def introduction(first_name, last_name):
 print("Hello, my name is", first_name, last_name)
introduction(first_name = "James", last_name = "Bond")
</code></pre>

* Argumentos de longitud variable

<pre><code class="python">
def suma(*numeros):
    print(type(numeros))
    # <class 'tuple'>
    total = 0
    for n in numeros:
        total += n
    return total
suma(1, 3, 5, 4) # 13
</code></pre>

* Uso de *args

Gracias a los *args en Python, podemos definir funciones cuyo número de argumentos es variable.

<pre><code class="python">
def suma(*args):
    s = 0
    for arg in args:
        s += arg
    return s

suma(1, 3, 4, 2)
#Salida 10

suma(1, 1)
#Salida 2
</code></pre>

* Valores por defecto

<pre><code class="python">
def introduction(first_name, last_name="Smith"):
 print("Hello, my name is", first_name, last_name)
print(dir(__builtins__))
print.__doc__
sum.__doc__
</code></pre>

* Documentación

<pre><code class="python">
def hello():
 """this is the funcion documentation hello.__doc__"""
 print("Hello world")
print(hello.__doc__)
</code></pre>

* Another examples

<pre><code class="python">
def my_print(prefix, *rest):
 message = prefix
 for r in rest:
   message + = " " + r
 print(message)
my_print("hello", "world")

def speak(**args):
   for key, value in args.items():
   print(key+ ":"+value)
 speak(message="one")

def capit(x):
 return x.upper()
messages = ["Hello", "Guten morgen"]
upper_messages = map(capit, messages) # HELLO, GUTEN MORGEN
upper_messages2 = map(lambda x: x.upper, messages)   # annonimous functions
</code></pre>

#### Decorators

Los decoradores son funciones de python que modifican el comportamiento de otras. De esta manera podemos conseguir acortar el código y/o reutilizarlo.

<pre><code class="python">
def restricted(func):
    def wrapper(*args, **kargs):
        if 7 <= datetime.now().hour < 22:
            return func(*args, **kargs)
        else:
            pass
        return wrapper

// my_script.py
@restricted
def say_whee():
 print("whee")
</code></pre>

#### Generators

Funciones que devuelven un objeto de tipo generador.

* Se caracteriza por tener la sentencia *yield* en lugar del return de una funcion.
* Una función generadora se difrencia de una normal en que el control se le devuelve a quien la llamó una vez ejectuada la sentencia yield.

<pre><code class="python">
def generador():
    yield 3

# Salida: <generator object generador at 0x00000266C9149C40>>
</code></pre>

Como vemos no devuelven el valor 3 sino un objeto de clase generator.

* Podemos iterar los generadores con *iter()* y *next()*

<pre><code class="python">
a = generador()
print(next(a))
# Salida: 5
</code></pre>

Si seguimos iterando nos devolverá una exception StopIteration ya que el generador en este caso solo devuelve un valor

#### Lambdas

Tipo de funciones que son definidas en una linea y son utilizadas para pequeños calculos o campos calculados.

<pre><code class="python">
suma = lambda a, b: a + b
suma(2,4) # 6
</code></pre>


### Estructuras de control e iteración


#### Loops e iteradores

<pre><code class="python">
Bucles con foreach
for i in range(6):
 print(i**2)
for i, color in enumerate(colors):
 print(i, "-->", color)

Iterar sobre array orden inverso
for name in reversed(names):
 print(name)

Iterar sobre varias listas
names = [John, Alice]
colors = [red, blue]
for name, color in zip(names, colors):
 print(name, color)

usando iterador
for name, color in izip(names, colors):
 print(name, color)

### Loops ###

# While

my_condition = 0

while my_condition < 10:
    print(my_condition)
    my_condition += 2
else: # Es opcional
    print("Mi condición es mayor o igual que 10")

print("La ejecución continúa")

while my_condition < 20:
    my_condition += 1
    if my_condition == 15:
        print("Se detiene la ejecución")
        break
    print(my_condition)

print("La ejecución continúa")

# For

my_list = [35, 24, 62, 52, 30, 30, 17]

for element in my_list:
    print(element)

my_tuple = (35, 1.77, "Brais", "Moure", "Brais")

for element in my_tuple:
    print(element)

my_set = {"Brais","Moure", 35}

for element in my_set:
    print(element)

my_dict = {"Nombre":"Brais", "Apellido":"Moure", "Edad":35, 1:"Python"}

for element in my_dict:
    print(element)
    if element == "Edad":
        break
else:
    print("El bluce for para diccionario ha finalizado")

print("La ejecución continúa")

for element in my_dict:
    print(element)
    if element == "Edad":
        continue
    print("Se ejecuta")
else:
    print("El bluce for para diccionario ha finalizado")

</code></pre>


### POO. Programación Orientada a Objetos

El paradigma de OOP (Object Oriented Programming) o en español POO (Programación Orientada a Objetos), nos permite organizar el código de una manera más estructurada y de forma más cercana a la vida real.
Las cosas y conceptos que encontramos en la vida real como un coche, una persona, una receta de cocina... Puede ser representada como un clase con sus cualidades (variables) y acciones (funciones).

#### Classes

Las clases son propias del paradigma de orientación a objetos (POO) y nos permiten definir un conjunto de variables y funciones en una misma entidad.
De esta manera si consideramos la entidad persona (Person), esta tiene un nombre, unos apellidos y una edad. De la misma manera esa persona puede realizar ciertas acciones como codificar.
Todo esto se puede representar en una clase como vemos a continuación:

<pre><code class="python">
class Person:
    def __init__(self, fn, ln, a):
        self.first_name = fn # instance variables
        self.last_name = ln
        self.age = a

    def code(self): # instance method
        print(self.first_name + " is coding")
ted = Person("Ted", "Neward", 48)
ted.code()
</code></pre>

Partes de una clase:

* Variables
* __init__: constructor de la clase. Los métodos que comienzan por doble underscore __ se les conoce como métodos mágicos ya que son especiales del lenguaje,
* Funciones

#### Diferenciación de variable de clase y de instancia.

* Una variable de clase es única y compartida por todas sus instancias. Esto significa que es accesible por todas las instancias. 
* Una variable de instancia es exclusiva y particular de cada instancia.
* En Python, las variables de clase se definen fuera de los métodos y las de instancia dentro de ellos. Lo vemos mejor con un ejemplo, utilizaremos la clase Person definida anteriormente pero añadiendo variables de clase.


<pre><code class="python">
class Person:

    species = 'mamífero' # Variable de clase

    def __init__(self, fn, ln, a):
        self.first_name = fn # variable de instancia
        self.last_name = ln
        self.age = a

    def code(self): # instance method
        print(self.first_name + " is coding")
ted = Person("Ted", "Neward", 48)
vic = Person("Vic", "Bus", 24)

print(f'{ted.first_name} es un {ted.species} y {vic.first_name} también es un {vic.species}') # Ted es un mamífero y Vic también es un mamífero
print(f'Todas las instancias de Person son de especie {Person.species}') # Todas las instancias de Person son de especie mamífero

# Pero si ahora la instancia Vic desea modificar la variable de clase ya que tiene acceso pasa lo siguiente:

vic.species = 'peixe'
print(f'Todas las instancias de Person son de especie {Person.species}') # Todas las instancias de Person son de especie mamífero
print(f'{vic.first_name} es de especie {vic.species}') # Vic es de especie peixe

# Esto ocurre porque Python, a diferencia de otros lenguajes, no modifica el atributo de clase, sino que crea una variable de instancia a la instancia con el mismo nombre que
# el que se desea modificar del atributo de clase y con el valor asignado

</code></pre>

La POO está basada en *6 pilares* :
1. Herencia
2. Cohesión
3. Abstracción
4. Polimorfismo
5. Acoplamiento
6. Encapsulamiento

#### Inheritance

Proceso mediante el cual podemos crear una clase hija que hereda de una padre, heredando de esta manera sus atributos y métodos (funciones). Con el ejemplo de persona:

<pre><code class="python">
class Student(Person): # herencia
    def study(self, subject):
        print(self.first_name + " is studying " + subject)

</code></pre>

De esta manera el estudiante (Student), a parte de tener estudiar una asignatura study(subject), también tendra nombre, apellidos, edad y la habilidad de codificar.

* Class property y @property (como getters y setters)
* Metaprograming, añadir comportamientos de forma dinámica

<pre><code class="python">
Person.another_method = lambda: "There is only Python"
Person.code_better= lambda self: sefl.first_name + " is coding"
</code></pre>

### Buenas prácticas

Iterar con enumerate()

<pre><code class="python">
data = [1, 2, 3, -1]
for idx, num in enumerate(data):
print(idx, num)
</code></pre>


list comprehension

<pre><code class="python">
data = [i for i in range(10)]
print(data)
</code></pre>

sorted()

<pre><code class="python">
to_sort = [5, 6, 8, 2, 1]
print(sorted(to_sort))
to_sort = [5, 6, 8, 2, 1]
print(sorted(to_sort, reverse=True))
data_to_sort = [{"name": "Alex", "age": 10}, {"name": "Alice", "age": 20}]
print(sorted(data_to_sort, key=lambda x: x.get("age")))
</code></pre>

Valores únicos con Set

<pre><code class="python">
list = [5, 1, 1, 1, 2, 3, 4]
aset = set(list)
print(aset)
</code></pre>

Ahorra memoria Generators

<pre><code class="python">
# Genera elementos de 1 en uno (lazy)
generated = (i for i in range(1000))
print(sum(generated))
</code></pre>

Default values en dictionaries

<pre><code class="python">
my_dic = {"name":"Alex", "age": 10}
my_dic.setdefault("telf", "No Telf")
print(my_dic.get("address", "NA"))
print(my_dic.get("telf"))
</code></pre>

Count hashtable con collections.Counter

<pre><code class="python">
list = [5, 1, 1, 1, 2, 3, 4]
counter = Counter(list)
print(counter)
most_common = counter.most_common()
print(most_common)
</code></pre>

Concatenate Strings

<pre><code class="python">
names = ["Alex", "Alice", "Bob"]
print(", ".join(names))
</code></pre>

Mergear dictionaries

<pre><code class="python">
dic1 = {"name": "Alex", "age": 10}
dic2 = {"name": "Alex", "address": "City name"}
merged = {**dic1, **dic2}
print(merged)
</code></pre>

Simple if-statement in list (contains)

<pre><code class="python">
my_list = ["red", "green", "blue"]
if "green" in my_list:
print("Green is in the list")
</code></pre>

<pre><code class="python">
# En diccionarios d.keys() devuelve un array con las claves

# Usar nombres de parámetros en llamadas a funciones
twitter_search('Obama', retweets=False, numtweets=20)

# Usar named tuples
test_results = namedtuple('TestResults', ['failed', 'attempted'])
# desempaquetar variables
p = 'Raymond', 'Hettinger', 30, 'rhettinger@example.com'
name, lname, age, email = p

# Simultaneous state update - Actualizar varias variables al mismo tiempo, asegura que se actualizan almismo tiempo
x, y = y, x+y

# No concatenar strings, usar ', '.join(names)
</code></pre>


### Error management

#### Exceptions

Las excepciones son comunes en lenguajes modernos debido a que nos permiten tratar de controlar el comportamiento de un software cuando se produce un error y que no se produzca una interrupción del programa.

* Levantar una excepción con *raise*

<pre><code class="python">
# Sin parámetro
raise ZeroDivisionError
# Con un parámetro de mensaje personalizado
raise ZeroDivisionError("Información de la excepción")
</code></pre>

* Uso de *try* y *except*

Sirven para capturar las excepciones y ser manejadas como queramos.

<pre><code class="python">
a = 5; b = 0
try:
    c = a/b
except ZeroDivisionError:
    print("No se ha podido realizar la división")
</code></pre>


#### Error types

A continuación, unos ejemplos de errores más habituales

<pre><code class="python">
### Error Types ###

# SyntaxError
#print "¡Hola comunidad!" # Descomentar para Error
print("¡Hola comunidad!")

# NameError
language = "Spanish" # Comentar para Error
print(language)

# IndexError
my_list = ["Python", "Swift", "Kotlin", "Dart", "JavaScript"]
print(my_list[0])
print(my_list[4])
print(my_list[-1])
#print(my_list[5]) # Descomentar para Error

# ModuleNotFoundError
#import maths # Descomentar para Error
import math

# AttributeError
#print(math.PI) # Descomentar para Error
print(math.pi)

# KeyError
my_dict = {"Nombre":"Brais", "Apellido":"Moure", "Edad":35, 1:"Python"}
print(my_dict["Edad"])
#print(my_dict["Apelido"]) # Descomentar para Error
print(my_dict["Apellido"])

# TypeError
#print(my_list["0"]) # Descomentar para Error
print(my_list[0])
print(my_list[False])

# ImportError
#from math import PI # Descomentar para Error
from math import pi
print(pi)

# ValueError
#my_int = int("10 Años")
my_int = int("10") # Descomentar para Error
print(type(my_int))

# ZeroDivisionError
#print(4/0) # Descomentar para Error
print(4/2)
</code></pre>

### Modules management

#### Modules

Los *módulos* son ficheros de python que contienen un conjunto de variables, funciones o clases que pueden ser reutilizados en otros módulos. Ejemplo:

<pre><code class="python">
# mimodulo.py
def suma(a, b):
    return a + b

def resta(a, b):
    return a - b
</code></pre>

Y su uso en otro módulo:

<pre><code class="python">
# otromodulo.py
import mimodulo

print(mimodulo.suma(4, 3))   # 7
print(mimodulo.resta(10, 9)) # 1
</code></pre>

#### Pip

También tendremos acceso, al tener instalado Python, a un gestor de paquetes llamado Pip. Su uso es muy sencillo. En la terminal:

pip install NOMBRE_PAQUETE

<pre><code class="bash">
pip install pymongo
</code></pre>

### Gestión de Recursos en Python

#### Context Manager

Lo context manager sirven para lidiar con recuros externos como pueden ser, ficheros, locks o conexiones (de red, de bases de datos...).
Python nos permite crear nuestros propios context manager para gestionar estor recursos de una manera customizada.


#### Operador with

Este statement crea un contexto de ejecución que nos permite correr un conjunto de instrucciones dentro del mismo. Esto lo hace más seguro y reusable que utilizando cláusulas try...except como se hacía anteriormente.
El formato es el siguiente:

<pre><code class="python">
with expression as target_var:
    do_something(target_var)
</code></pre>

Y es muy utilizado para la gestión de ficheros:

<pre><code class="python">
with open("hello.txt", mode="w") as file:
    file.write("Hello, World!")
</code></pre>

Y para las conexiones:

<pre><code class="python">
from contextlib import closing

import mysql.connector


query = "SELECT * FROM table"

db_conn_info = {
    "user": "root",
    "passwd": "",
    "host": "localhost",
    "port": 5000,
    "database": "database_name"
}

with closing(mysql.connector.connect(**db_conn_info)) as conn:
    with closing(conn.cursor()) as cur:
        cur.execute(query)
        result = cur.fetchall()

</code></pre>


### Files management

#### Files handling

En Python tiene gran importancia el File Handling, y disponemos de módulos como *os, json, csv, xml*... con los que podemos manejarlos a nuestro antojo.

Algunos ejemplos a continuación. Los archivos de pruebas se encuentran adjuntos en esta wiki

<pre><code class="python">

### File Handling ###

import os

# .txt file

txt_file = open("Intermediate/my_file.txt", "w+") # Leer, escribir y sobrescribir si ya existe

txt_file.write("Mi nombre es Brais\nMi apellido es Moure\n35 años\nY mi lenguaje preferido es Python")

#print(txt_file.read())
print(txt_file.read(10))
print(txt_file.readline())
print(txt_file.readline())
for line in txt_file.readlines():
    print(line)

txt_file.write("\nAunque también me gusta Kotlin")
print(txt_file.readline())

txt_file.close()

with open("Intermediate/my_file.txt", "a") as my_other_file:
    my_other_file.write("\nY Swift")

#os.remove("Intermediate/my_file.txt")

# .json file

import json

json_file = open("Intermediate/my_file.json", "w+")

json_test = {
    "name":"Brais", 
    "surname":"Moure", 
    "age":35, 
    "languages":["Python", "Swift", "Kotlin"],
    "website":"https://moure.dev"}

json.dump(json_test, json_file, indent = 2)

json_file.close()

with open("Intermediate/my_file.json") as my_other_file:
    for line in my_other_file.readlines():
        print(line)

json_dict = json.load(open("Intermediate/my_file.json"))
print(json_dict)
print(type(json_dict))
print(json_dict["name"])

# .csv file

import csv

csv_file = open("Intermediate/my_file.csv", "w+")

csv_writer = csv.writer(csv_file)
csv_writer.writerow(["name", "surname", "age", "language", "website"])
csv_writer.writerow(["Brais", "Moure", 35, "Python", "https://moure.dev"])
csv_writer.writerow(["Roswell", "", 2, "COBOL", ""])

csv_file.close()

with open("Intermediate/my_file.csv") as my_other_file:
    for line in my_other_file.readlines():
        print(line)


</code></pre>

### Regular Expresions

#### Regular Expresions

El uso de expresiones regulares está muy extendido, especialmente en el desarrollo web donde debemos comprobar y validar datos de entrada en los formularios por ejemplo.
En Python contamos con el m´ódulo *re* para realizar todo tipo de acciones en lo relativo a regex. A continuación algunos ejemplos:

<pre><code class="python">
### Regular Expressions ###

import re

# match

my_string = "Esta es la lección número 7: Lección llamada Expresiones Regulares"
my_other_string = "Esta no es la lección número 6: Manejo de ficheros"

match = re.match("Esta es la lección", my_string, re.I)
print(match)
start, end = match.span()
print(my_string[start:end])

match = re.match("Esta no es la lección", my_other_string)
#if not(match == None): # Otra forma de comprobar el None
#if match != None: # Otra forma de comprobar el None
if match is not None:
    print(match)
    start, end = match.span()
    print(my_other_string[start:end])

print(re.match("Expresiones Regulares", my_string))

# search

search = re.search("lección", my_string, re.I)
print(search)
start, end = search.span()
print(my_string[start:end])

# findall

findall = re.findall("lección", my_string, re.I)
print(findall)

# split

print(re.split(":", my_string))

# sub

print(re.sub("[l|L]ección", "LECCIÓN", my_string))
print(re.sub("Expresiones Regulares", "RegEx", my_string))

### Regular Expressions Patterns ###

# Para aprender y validar expresiones regulares: https://regex101.com

pattern = r"[lL]ección"
print(re.findall(pattern, my_string))

pattern = r"[lL]ección|Expresiones"
print(re.findall(pattern, my_string))

pattern = r"[0-9]"
print(re.findall(pattern, my_string))
print(re.search(pattern, my_string))

pattern = r"\d"
print(re.findall(pattern, my_string))

pattern = r"\D"
print(re.findall(pattern, my_string))

pattern = r"[l].*"
print(re.findall(pattern, my_string))

email = "mouredev@mouredev.com"
pattern = r"^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z-.]+$"
print(re.match(pattern, email))
print(re.search(pattern, email))
print(re.findall(pattern, email))

email = "mouredev@mouredev.com.mx"
print(re.findall(pattern, email))
</code></pre>

### Crear un venv con instalación de requirements.txt

* Inicialmente necesitaremos tener instalados Python y pip en nuestra máquina.


* En Python 3 venv ya viene con el intérprete así que no tendremos que instalar nada
* Una vez creado el directorio del proyecto (si no lo tenemos lo creamos, mkdir proyecto), creamos el venv

<pre><code class="bash">
python3 -m venv venv
</code></pre>


* Activamos el entorno

En Windows
<pre><code class="bash">
venv\Scripts\activate
</code></pre>

En Linux
<pre><code class="bash">
. venv/bin/activate
</code></pre>

* Cuando lo activemos pondrá un alias en nuestra linea de comando con el nombre del entorno, en nuestro caso `venv`

<pre><code class="bash">
(venv) C:\Users\<YOUR_USERNAME>\<YOUR_WORKING_FOLDER>\microservice-archetype-python>
</code></pre>

* Seguidamente, hacer una instalación de los requirements

<pre><code class="bash">
pip install -r requirements.txt
</code></pre>



* Una vez dentro del entorno podremos pasar las instalaciones que hayamos hecho (dentro del entorno) con pip al requirements usando el siguiente comando

<pre><code class="bash">
pip3 freeze > requirements.txt
</code></pre>

### Debugger en Pycharm

#### Preparación de Pycharm

* Una vez abierto el proyecto en Pycharm iremos a la parte superior derecha y pincharemos en el *input de configuraciones* -> Edit Configurations


* Pincharemos en el icono + para añadir una nueva configuración


* Añadimos un nombre a la configuración y elegimos un intérprete (recomendable que sea el de tu entorno). El resto de las opciones las dejamos igual


* Seleccionamos nuestro fichero base como working directory.


* Para arrancar en modo Debug seleccionamos el icono del bug en la parte superior derecha


#### Uso del debugger

* Podremos añadir *breakpoints* en las líneas de nuestro código pulsando al lado derecho del número de línea


* Una vez arrancado el Debugger accederemos a la parte de la aplicación que ejecute nuestro código y veremos la vista del debugger detallada.


#### Ejemplo práctico debugger


<pre><code class="python">
import math


class Solver:

    def demo(self, a, b, c):
        d = b ** 2 - 4 * a * c
        if d > 0:
            disc = math.sqrt(d)
            root1 = (-b + disc) / (2 * a)
            root2 = (-b - disc) / (2 * a)
            return root1, root2
        elif d == 0:
            return -b / (2 * a)
        else:
            return "This equation has no roots"


if __name__ == '__main__':
    solver = Solver()

    while True:
        a = int(input("a: "))
        b = int(input("b: "))
        c = int(input("c: "))
        result = solver.demo(a, b, c)
        print(result)
</code></pre>

* Colocamos breakpoints


* Empezamos la sesión de debugger


* El debugger arranca y nos deja insertar valores en la consola de debug. (También puedes usar funciones  de Python)


*   Cuando los ejecutamos para en el primer breakpoint y vemos el *inline debugging* , donde se puede ver la dirección de memoria de `solver` y los valores que hemos aportado


* Steps: tenemos una toolbar con flecha que indican los difrentes steps que hay para moverse por el código en tiempo de ejecución.


* Podemos probar a darle a step over (F8), que nos moverá a ala siguiente línea mostrándonos valores


* Si probamos con step into (F7), no solo nos moveremos por nuestras lineas sino que se meterá en la implementación de los métodos de Python que aparezcan, Por ejemplo el método input al llegar a las líneas que lo contienen:


* También nos permite ver el valor de las variables, lo que se conoce como *watching*


* Finalmente nos permite evaluar expresiones en el propio debugger


### Referencias y enlaces de interés

Página oficial de Python (https://www.python.org/)

Guía oficial de estilo para código Python (https://peps.python.org/pep-0008/)

Tutorial oficial de Python en español (https://docs.python.org/es/3/tutorial/index.html)

Curso en vídeos en español por Brais Moure (https://github.com/mouredev/Hello-Python)

Guía con ejemplos en español (https://ellibrodepython.com/)

Repo en Github de ejemplos con +16k Stars y casi 4k forks (https://github.com/Asabeneh/30-Days-Of-Python)

Creación de entorno virtualenv Python (https://davidcasr.medium.com/c%C3%B3mo-crear-un-entorno-o-ambiente-virtual-en-python-57a1607a4180)

Vídeo de buenas prácticas en youtube (https://www.youtube.com/watch?v=OSGv2VnC0go&t=1666s)

Debugger de Pycharm, Jetbrains Docs (https://www.jetbrains.com/help/pycharm/part-1-debugging-python-code.html#hex-format)