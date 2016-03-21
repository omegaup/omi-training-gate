[TOC]

Teoría de números
===============

Pre-requisitos
-----------------
* [Inferencia][inference]
* [Demostraciones][proof]
* [Notación asintótica][asymptotic-notation]
* [Complejidad][complexity]
* Exponenciación binaria

 [inference]: http://tbd
 [proof]: http://tbd
 [asymptotic-notation]: http://tbd
 [complexity]: http://tbd
 
Divisibilidad
---------------
### Definición
> Si $a$ y $d\neq0$ son enteros, se dice que "$d$ divide a $a$" $$d|a$$ si existe un entero $q$ tal que $a = dq$.

Aquí, $a$ se le llama dividendo, $d$ el divisor y $q$ el cociente (q por "quotient" en inglés).
Por ejemplo, 63 divide a 2016, porque existe el entero 32 tal que $2016 = 63\times32$. Por otro lado, 63 no divide a 2017, porque no existe ningun entero que multiplicado por 63 de como resultado 2017. Esto lo podemos verificar con el siguiente algoritmo:
```
def es_divisor(a, d):
	if d == 0:  # 0 nunca es un divisor.
		return False
	q = 0
	while d*q < a:
		q += 1
	return a == d*q

print "63 divide a 2016:", es_divisor(2016, 63)
print "63 divide a 2017:", es_divisor(2017, 63)
```
Por simplicidad, suponemos que $a$ y $d$ son positivos. El algoritmo intenta encontrar algún cociente $q$ que cumpla la igualdad $a = dq$.
El valor del producto $dq$ crece por $d$ en cada iteración; como supusimos que $d>=1$, $dq$ en algún momento va a alcanzar o rebasar el valor de $a$, y el algoritmo termina.
Cualquier valor mayor para $q$ implicaría un producto $dq>a$ por lo que no hace falta revisar más enteros más allá del primer valor que cumpla $dq \geq a$.
Si al terminar el ciclo, la igualdad no se cumple, sabemos que no hay ningún entero que cumpla la condición de divsibilidad (porque probamos todos los posibles candidatos!).

También podemos reescribir el algoritmo anterior como:
```
def es_divisor_div(a, d):
	if d == 0:  # 0 nunca es un divisor.
		return False
	q = a / d   # Si a y d son enteros, q es el piso de a / d.
	return a == d*q
print "63 divide a 2016:", es_divisor_div(2016, 63)
print "63 divide a 2017:", es_divisor_div(2017, 63)
```
Dado que la definición de división de enteros en lenguajes de programación comunes es el piso de la división, tenemos que:
$$q = \lfloor a / d \rfloor$$
que es el mayor **entero** menor o igual que el valor de $a / d$. Si ese entero cumple la definición de divisbilidad, la respuesta es `True`, de lo contrario, cualquier valor mayor de $d$ sería mayor que el valor real de la división, por lo que al calcular el producto, éste sería mayor que $a$ (y la respuesta sería `False`). Esto es, basta con probar ese y sólo ese valor posible para $q$.

### Propiedades
Supongamos que $a$, $b$, $c$ y $d\neq0$ son enteros.
1. Si $d|a$, entonces $d|ac$.
2. Si $d|a$ y $d|b$, entonces $d|a+b$.
4. En general, si $x$ y $y$ son enteros, entonces $d|ax+by$.
5. Si $d|a$ y $a|b$, entonces $d|b$.
6. Si $d|a$ y $d|a+b$, entonces $d|b$.
**TODO(pmag):** Desigualdades
### Ejercicios
CodeChef: Suma maxima de divisores de un comun multiplo

Números primos
--------------------
### Definición
> Un número primo es un entero positivo que tiene exactamente dos divisores positivos.

Por ejemplo: 2, 3, y 17 son números primos. Sus divisores positivos son 1 y ellos mismos. Pero 0 no es primo, todo entero diferente de cero es un divisor, es decir, tiene una infinidad de divisores.
1 no es primo, porque tiene solo 1 divisor, que es el mismo 1.
4 no es divisor porque tiene 3 divisores: 1, 2, 4.

### Teorema fundamental de la Aritmética
### Teorema: Existe una infinidad de números primos
### Primality tests

Existen varias formas para determinar si un número es primo o no. Cuál es la mejor depende del caso. Si sólo se necesita responder la pregunta para un número o si se necesita contestar para muchos.

#### Trial division
La forma trivial de determinar si un número es primo o no es probando todos los posibles divisores. Sabemos que para un entero dado $n$, 1 y $n$ siempre son divisores, entonces podemos buscar algún divisor entre esos dos. Por ejemplo:
```
def es_primo(n):
	if n <= 1:  # Solo enteros >= 2 pueden ser primos.
		return False

	for d in xrange(2, n):
		if n % d == 0:
			return False

	return True
```
Para un número $n$, entonces, este algoritmo intenta $n-2$ divisiones, por lo que su tiempo de ejecución es $O\left(n\right)$.
Esto es suficiente para resolver el problema para un sólo número razonablemente pequeño.
**TODO(pmag):** Ejemplo de problema.

Para implementar un algoritmo más eficiente, notemos que si $n$ es un número compuesto, se puede escribir como $$n = ab$$.
Sin perdida de generalidad, supongamos que $a \leq b$, entonces, multiplicando ambos lados por $a$, tenemos:
$$a^2 \leq ab = n$$
$$a \leq \sqrt{n}$$
Es decir, si existe un factor de $n$, lo debemos encontrar dentro de los primeros $\sqrt{n}$ enteros.
Con esto, podemos cortar el tiempo de ejecución de la prueba de primalidad de $O\left(n\right)$ a $O\left(\sqrt{n}\right)$.
```
def es_primo_sqrt(n):
	if n <= 1:
		return False
	d = 2
	while d*d <= n:
		if n % d == 0:
			return False
		d += 1
	return True
```
**TODO(pmag):** Ejemplo de problema que requiera esto. HackerRank 30 days - day 25.

#### Fermat
#### Miller-Rabin
##### Versión determinística
### Ejercicios
Cuántas veces divide m a n!; Cuantos ceros a la derecha tiene n!.

Criba de Eratóstenes
------------------------
### Definición
#### Número de divisores $\tau\left(n\right)$
#### Suma de divisores $\sigma\left(n\right)$

Aritmética modular
-----------------------
### Congruencias
### Teorema de Fermat
### Teorema de Euler
#### Factorizando
#### Usando una criba

Inverso multiplicativo
--------------------------
### Definición
> Si $a$ y $m$ son enteros, el inverso multiplicativo de $a$ módulo m es el entero $b = a^{-1}\pmod m$ tal que $ab \equiv 1 \pmod m$.

### Extended GCD
### Teorema de Euler
Si recordamos el Teorema de Euler, sabemos que
$$a^{\phi(n)} \equiv 1 \pmod n$$
Para $a$ y $n$ primos relativos. Eso quiere decir, que el inverso multiplicativo de $a$ es $a^{\phi(n)-1}$. Utilizando exponenciación binaria, este se puede calcular en forma eficiente suponiendo que conocermos $\phi(n)$.
Afortunadamente, para muchos problemas de programación el módulo que se utiliza es primo (típicamente $10^9+7$), y sabemos que para números primos $\phi(n) = n-1$, de manera que el inverso multiplicativo es simplemente $a^{n-2}$.

Máximo común divisor (GCD) y Mínimo común múltiplo
------------------------------------------------------------------


### Tables

**Markdown Extra** has a special syntax for tables:

Item     | Value
-------- | ---
Computer | $1600
Phone    | $12
Pipe     | $1

You can specify column alignment with one or two colons:

| Item     | Value | Qty   |
| :------- | ----: | :---: |
| Computer | $1600 |  5    |
| Phone    | $12   |  12   |
| Pipe     | $1    |  234  |


### Fenced code blocks

GitHub's fenced code blocks are also supported with **Highlight.js** syntax highlighting:

```
// Foo
var bar = 0;
```

> **Tip:** To use **Prettify** instead of **Highlight.js**, just configure the **Markdown Extra** extension in the <i class="icon-cog"></i> **Settings** dialog.

> **Note:** You can find more information:

> - about **Prettify** syntax highlighting [here][5],
> - about **Highlight.js** syntax highlighting [here][6].


### Footnotes

You can create footnotes like this[^footnote].

  [^footnote]: Here is the *text* of the **footnote**.


### SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                  | ASCII                        | HTML              |
 ----------------- | ---------------------------- | ------------------
| Single backticks | `'Isn't this fun?'`            | 'Isn't this fun?' |
| Quotes           | `"Isn't this fun?"`            | "Isn't this fun?" |
| Dashes           | `-- is en-dash, --- is em-dash` | -- is en-dash, --- is em-dash |

```
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
```

### UML diagrams

You can also render sequence diagrams like this:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

And flow charts like this:

```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

> **Note:** You can find more information:

> - about **Sequence diagrams** syntax [here][7],
> - about **Flow charts** syntax [here][8].

  [1]: http://math.stackexchange.com/
  [2]: http://daringfireball.net/projects/markdown/syntax "Markdown"
  [3]: https://github.com/jmcmanus/pagedown-extra "Pagedown Extra"
  [4]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
  [5]: https://code.google.com/p/google-code-prettify/
  [6]: http://highlightjs.org/
  [7]: http://bramp.github.io/js-sequence-diagrams/
  [8]: http://adrai.github.io/flowchart.js/
