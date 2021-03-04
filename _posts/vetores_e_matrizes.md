---
layout: post
title: "Vetores e matrizes"
author: "RN Cernic"
categories: journal
tags: [math]
image:
---


# <span style='color:blue'>Vetores e matrizes</span>

Neste pequeno recordatório sobre vetores e matrizes abordamos algumas notações, operações e propriedades, além disso alguns exemplos ilustrativos serão apresentados códigos utilizando a biblioteca ***numpy*** de forma a estabelecer uma ponte entre os conceitos e a implantação na prática.

O objetivo é abordar os pontos essenciais que são utulizados em cursos introdutórios de Ciência de Dados, portanto não abordamos demonstrações matemáticas, casos gerais etc.

Adicionalmente daremos uma pincelada em sistemas de equações, visto que estes são muito utilizados em algorítmos de aprendizagem de máquina, como, por exemplo, em regressões lineares.

Primeiramente vamos importar a biblioteca ***numpy***, que utilizaremos nos exemplos.


```python
# importação da biblioteca numpy
import numpy as np
```

## Sumário

- [Notação básica](#notacao)
- [Matrizes especiais](#especiais)
    - [Matriz quadrada](#quadrada)
    - [Matriz nula](#nula)
    - [Matriz identidade](#identidade)
    - [Vetores](#vetores)
- [Operações aritméticas](#aritmetica)
    - [Adição e subtração](#adicao)
    - [Multiplicação por escalar](#multiplicacao_escalar)
    - [Multiplicação de matrizes](#multiplicacao_matrizes)
- [Determinante](#determinante)
- [Matriz inversa](#inversa)
- [Matriz transposta](#transposta)
- [Sistemas de equações](#sistemas)
- [Material útil](#material)
    - [Propriedades](#propriedades)
    - [Referências](#referencias)


## Notação básica <a class="anchor" id="notacao"></a>

Toda matriz tem uma dimensão ou tamanho que podemos denominar $n \times m$, onde $n$ representa o número de linhas e $m$ o número de colunas. Cada elemento da matriz é denominado $a_{ij}$, onde $i$ é o número da linha e $j$ o da coluna. Por exemplo, $a_{13}$ representa o elemento que se encontra na 1a linha e 3a coluna.

Uma matriz pode ser escrita conforme a seguir:

$$
\large \mathbf{A} = 
\begin{pmatrix}
a_{11} & a_{12} & ... & a_{1m} \\ 
a_{21} & a_{22} & ... & a_{2m} \\ 
\vdots & \vdots &        & \vdots \\ 
a_{n1} & a_{n2} & ... & a_{nm}
\end{pmatrix}_{n \times m} =
(a_{ij})_{n \times m}
$$

A dimensão da matriz ($n \times m$) é apresentada na forma de subescrito, quando isso for relevante para a situação específica. Na grande maioria dos casos práticos essa informação acaba sendo omitida, contudo a dimensão é uma informação importante, visto que algumas operações somente são permitidas para dimensões específicas.

## Matriz especiais <a class="anchor" id="especiais"></a>

Existem algumas matrizes especiais que podem ser úteis em diversas circunstâncias, portanto é interessante conhecê-las. É o que faremos a seguir.

### *Matriz quadrada* <a class="anchor" id="quadrada"></a>

A primeira matriz especial é a matriz quadrada, que é assim denomidada por apresentar o número de linhas $n$ igual ao número de columas $m$; ou seja, apresenta um número igual de linhas e colunas. Neste caso a dimensão é dita $n \times n$ e a diagonal que começa no elemento $a_{11}$ e termina no elemento $a_{nn}$ recebe a denominação de **diagonal principal**. A seguir apresentamos a notação de uma matriz quadrada.

$$
\large \mathbf{A} = 
\begin{pmatrix}
a_{11} & a_{12} & ... & a_{1n} \\ 
a_{21} & a_{22} & ... & a_{2n} \\ 
\vdots & \vdots &        & \vdots \\ 
a_{n1} & a_{n2} & ... & a_{nn}
\end{pmatrix}_{n \times n} =
(a_{ij})_{n \times n}
$$

### *Matriz nula* <a class="anchor" id="nula"></a>

A segunda matriz especial é a matriz nula, denominada $\mathbf 0_{n \times m}$. Nessa matriz todos os elementos $a_{ij}$ têm valor zero. Ela se assemelha ao número 0 nas operações com números reais.

$$
\large \mathbf{0}_{n \times m} = 
\begin{pmatrix}
0 & 0 & ... & 0 \\ 
0 & 0 & ... & 0 \\ 
\vdots & \vdots &  & \vdots \\ 
0 & 0 & ... & 0
\end{pmatrix}_{n \times m}
$$

A matriz nula pode ser criada usando-se a biblioteca *numpy* conforme o código a seguir:


```python
z = np.zeros((4,5)) # cria uma matriz nula (ou de zeros) com 4 linhas e 5 colunas
print(z,z.shape)    # imprime a dimensão da matriz
```

    [[0. 0. 0. 0. 0.]
     [0. 0. 0. 0. 0.]
     [0. 0. 0. 0. 0.]
     [0. 0. 0. 0. 0.]] (4, 5)


### *Matriz identidade* <a class="anchor" id="identidade"></a>

Outra matriz especial é a matriz identidade, que **deve** ser quadrada e é denominada de $I_{n}$, onde todos os elementos de sua diagonal principal têm valor 1. Ela se assemelha ao número 1, mas operações convencionais com números reais.

$$
\large \mathbf{I}_{n} = 
\begin{pmatrix}
1 & 0 & ... & 0 \\ 
0 & 1 & ... & 0 \\ 
\vdots & \vdots & \ddots & \vdots \\ 
0 & 0 & ... & 1
\end{pmatrix}_{n \times n}
$$

**Propriedade:** qualquer matriz $\mathbf A$ multiplicada pela matriz identidade retorna a própria matriz $\mathbf A$. A matriz identidade pode ser criada usando-se a biblioteca numpy conforme o código a seguir:


```python
i = np.eye(4)      # cria a matriz identidade de dimensão 4
print(i, i.shape)  # imprime a dimensão da matriz
```

    [[1. 0. 0. 0.]
     [0. 1. 0. 0.]
     [0. 0. 1. 0.]
     [0. 0. 0. 1.]] (4, 4)


### *Vetores* <a class="anchor" id="vetores"></a>

O último caso de matrizes especiais é o das matrizes coluna e matrizes linha. A matriz coluna consiste de apenas uma coluna com $n$ linhas, enquanto da matriz linha tem apenas uma linha com $m$ colunas. A seguir apresntamos a notação para os dois casos.

$$
\begin{align}
\large \mathbf{x} & = 
\begin{pmatrix}
x_{1} \\ 
x_{2} \\ 
\vdots \\ 
x_{n}
\end{pmatrix}_{n \times 1}
\\
\\
\large \mathbf{y} & = 
\begin{pmatrix}
y_{1} & 
y_{2} & 
... &
y_{m}
\end{pmatrix}_{1 \times m}
\end{align}
$$

Essas matrizes com apenas uma linha ou uma coluna são denominadas **vetores** e são largamente utilizadas. O código a seguir mostra como criá-las com a biblioteca *numpy*.


```python
# vetor coluna
x = np.matrix([[1],[2],[3]])
print(x, x.shape)
```

    [[1]
     [2]
     [3]] (3, 1)



```python
# vetor linha
y = np.matrix([1, 2, 3])
print(y, y.shape)
```

    [[1 2 3]] (1, 3)


## Operações aritméticas <a class="anchor" id="aritmetica"></a>

Agora que já conhecemos a notação matricial e as matrizes especiais podemos explorar as operações aritméticas envolvendo matrizes.

### *Adição e subtração* <a class="anchor" id="adicao"></a>

A adição ou subtração de duas matrizes $\mathbf A$ e $\mathbf B$, de **mesma dimensão**, resulta em uma matriz $\mathbf C$ com esta mesma dimensão, cujos elementos representam a adição ou subtração dos respectivos elementos das matrizes $\mathbf A$ e $\mathbf B$. Por exemplo, $c_{11} = a_{11} \pm b_{11}$. A notação para estas operações é a seguinte: 

$$ \large \mathbf A_{n \times m} \pm \mathbf B_{n \times m} = (a_{ij})_{n \times m} \pm (b_{ij})_{n \times m} = (a_{ij} \pm b_{ij})_{n \times m} $$

### *Multiplicação por escalar* <a class="anchor" id="multiplicacao_escalar"></a>

A multiplicação de uma matriz por um escalar, ou seja, por uma constante, é feita pela multiplicação de cada termo individual da matriz por esse escalar. A notação para essa operação é a seguinte:

$$ \large \alpha\mathbf A_{n \times m} = \alpha(a_{ij})_{n \times m} = (\alpha a_{ij})_{n \times m} $$

---
#### <span style="color:red">Exemplo de multiplicação e subtração</span>

Neste exemplo colocaremos em prática a multiplação por escalar e a subtração de matrizes.

Dadas as matrizes A e B queremos computar o valor de $A - 5B$

$$
\large \mathbf{A} = 
\begin{pmatrix}
3 & -2 \\ 
-9 & 1
\end{pmatrix}
\; \; \; \; \;
\mathbf{B} = 
\begin{pmatrix}
-4 & 1 \\ 
0 & -5
\end{pmatrix}
$$

Aplicando-se as definições mencionadas acima, teremos:

$$
\begin{align}
\large
A-5B & = 
\begin{pmatrix}
3 & -2 \\ 
-9 & 1
\end{pmatrix}
-5
\begin{pmatrix}
-4 & 1 \\ 
0 & -5
\end{pmatrix}
\\
\\
\large
A-5B & = 
\begin{pmatrix}
3 & -2 \\ 
-9 & 1
\end{pmatrix}
-
\begin{pmatrix}
-20 & 5 \\ 
0 & -25
\end{pmatrix}
\\
\\
\large
A-5B & = 
\begin{pmatrix}
23 & -7 \\ 
-9 & 26
\end{pmatrix}
\end{align}
$$

Fazendo uso do ***numpy*** teremos:


```python
a = np.matrix([[3,-2],[-9,1]])
b = np.matrix([[-4,1],[0,-5]])
print("Matriz A\n", a)
print("\nMatriz B\n", b)
print("\nA-5B\n",a-5*b)
```

    Matriz A
     [[ 3 -2]
     [-9  1]]
    
    Matriz B
     [[-4  1]
     [ 0 -5]]
    
    A-5B
     [[23 -7]
     [-9 26]]


---

### *Multiplicação de matrizes* <a class="anchor" id="multiplicacao_matrizes"></a>

A multiplicação de duas matrizes **somente é possível** se a primeira matriz $\mathbf A$ tiver o número de colunas igual ao número de linhas da segunda matrix $\mathbf B$. Se a matriz $\mathbf A$ tiver a dimensão $n \times p$ e a $\mathbf b$ a dimensão $p \times m$ a matriz $\mathbf C$ resultante terá a dimensão $n \times m$. O valor de $c_{ij}$ é encontrado somando-se o produto da linha $i$ da matriz $\mathbf A$ com coluna $j$ da matriz $\mathbf b$ elemento a elemento. Isso ficará mais claro com o exemplo a seguir.

$$
\large \mathbf A_{n \times p} \mathbf B_{p \times m} = \mathbf C_{n \times m} = (c_{ij})_{n \times m}
$$

onde:

$$
\begin{align}
\large c_{ij} & = \sum_{k=1}^{n} a_{ik} b_{kj}\\
& = a_{i1}b_{1j} + a_{21}b_{2j} + a_{i3}b_{3j} + \dots + a_{in}b_{nj} 
\end{align}
$$

---
#### <span style="color:red">Exemplo de multiplicação de matrizes</span>

Dadas as matrizes A e B queremos computar o valor de $AB$

$$
\large \mathbf{A} = 
\begin{pmatrix}
2 & -1 & 0 \\ 
-3 & 6 & 1
\end{pmatrix}
\; \; \; \; \;
\mathbf{B} = 
\begin{pmatrix}
-4 & 1 & 3 \\ 
0 & -5 & 1 \\
-1 & 1 & 2
\end{pmatrix}
$$

Aplicando-se a definição para alguns elementos, temos:

$$
\begin{align}
\large
c_{11} & = 2*(-4) + (-1)*0 + 0*(-1) = -8
\\
\\
\large
c_{12} & = 2*1 + (-1)*(-5) + 0*1 = 7
\end{align}
$$

O resultdo final será:

$$
\large
\mathbf{C} = 
\begin{pmatrix}
-8 & 7 & 5 \\ 
11 & -32 & -1
\end{pmatrix}
$$


<div class="alert alert-block alert-info">
<b>Importante:</b> Note que neste exemplo podemos fazer porduto $\mathbf AB$ e não o $\mathbf BA$ por causa das dimensões das matrizes. O fato de o produto $\mathbf AB$ existir não significa que o produto $\mathbf BA$ também exista. Adicionalmete, se ambos os produtos existirem os resultados podem ou não serem iguais.
</div>

Usando o ***numpy*** temos:


```python
a = np.matrix([[2,-1,0],[-3,6,1]])
b = np.matrix([[-4,1,3],[0,-5,1],[-1,1,2]])
print("Matriz A\n", a)
print("\nMatriz B\n", b)
print("\nA*B\n",a*b)
```

    Matriz A
     [[ 2 -1  0]
     [-3  6  1]]
    
    Matriz B
     [[-4  1  3]
     [ 0 -5  1]
     [-1  1  2]]
    
    A*B
     [[ -8   7   5]
     [ 11 -32  -1]]


---

## Determinante <a class="anchor" id="determinante"></a>

O determinante é uma operação matemática que transforma uma matriz **quadrada** em um único número real. A fórmula do determinante é bastante complexa e não a abordaremos. Apenas mostraremos como calcular o determinante de matrizes ${2 \times 2}$.

**O determinate é uma função importante, pois permite saber se a matriz tem ou não inversa, visto que as que não têm são precisamente aquelas cujo determinante é igual a 0.**

Uma matriz com determinate zero é dita singular e não singular quando o determinante for diferente de zero.

A notação utilizada para indicar o determinante é:

$$\large det(\mathbf A) = |\mathbf A|$$

Para uma matriz $2 \times 2$ a fórmula para cálculo do determinate é:

$$
\large
\left|
\begin{matrix}
a & c \\
b & d
\end{matrix}
\right| = ad - cb
$$

---
#### <span style="color:red">Exemplo do cálculo do determinante</span>

Calcular o determinate da matriz $\mathbf A$

$$
\large \mathbf{A} = 
\begin{pmatrix}
2 & -1 \\ 
-3 & 6
\end{pmatrix}
$$

$$
\large
det(\mathbf A) =
\left|
\begin{matrix}
2 & -1 \\
-3 & 6
\end{matrix}
\right| = 2*6 - (-1)*(-3) = 9
$$

Usando o ***numpy*** temos:


```python
a = np.matrix([[2,-1],[-3,6]])
print("Matriz A\n", a)
print("\ndet(A)\n",np.linalg.det(a))
```

    Matriz A
     [[ 2 -1]
     [-3  6]]
    
    det(A)
     9.000000000000002


<br>
Para a matriz $3 \times 3$, teremos:

$$
\large
\mathbf{A} = 
\begin{pmatrix}
-4 & 1 & 3 \\ 
0 & -5 & 1 \\
-1 & 1 & 2
\end{pmatrix}
$$


```python
a = np.matrix([[-4,1,3],[0,-5,1],[-1,1,2]])
print("Matriz A\n", a)
print("\ndet(A)\n",np.linalg.det(a))
```

    Matriz A
     [[-4  1  3]
     [ 0 -5  1]
     [-1  1  2]]
    
    det(A)
     27.999999999999996


---

## Matriz inversa <a class="anchor" id="inversa"></a>

O processo manual de cálculo da matriz inversa é bastante tedioso e não o abordaremos. Apenas focaremos nas suas propriedades. Dada uma matriz **quadrada** $\mathbf A$ de dimensão $n \times n$ se pudermos encontrar uma outra matriz $\mathbf B$, de mesma dimensão, que safisfaça:

$$\large \mathbf{A} \mathbf{B} = \mathbf{B} \mathbf{A} = \mathbf {I}_{n}$$

então a matirz $\mathbf B$ é denominada de inversa de $\mathbf A$ e representada por $\mathbf B = \mathbf A^{-1}$. Se uma matriz é **inversível**, ou seja, possui uma inversa, então essa inversa é única.

$$
\large
\mathbf{A} = 
\begin{pmatrix}
1 & -1 & 0 \\ 
1 & 0 & -1 \\
-6 & 2 & 3
\end{pmatrix}
\; \; \; \; \;
\mathbf{A}^{-1} = 
\begin{pmatrix}
-2 & -3 & -1 \\ 
-3 & -3 & -1 \\
-2 & -4 & -1
\end{pmatrix}
$$


---
#### <span style="color:red">Exemplo do cálculo da inversa</span>

Usando o ***numpy*** podemos calcular a matriz inversa como segue:


```python
a = np.matrix([[1,-1,0],[1,0,-1],[-6,2,3]])
a_inv = np.linalg.inv(a)
print("Matriz A\n", a)
print("\nInversa de A\n",a_inv)
```

    Matriz A
     [[ 1 -1  0]
     [ 1  0 -1]
     [-6  2  3]]
    
    Inversa de A
     [[-2. -3. -1.]
     [-3. -3. -1.]
     [-2. -4. -1.]]


Podemos confirmar que a matriz é inversível aplicando-se a definição: $\mathbf{A} \mathbf{A}^{-1} = \mathbf{A}^{-1} \mathbf{A} = \mathbf {I}_{n}$

Vejamos o produto de $\mathbf A$ por sua inversa $\mathbf A^{-1}$:


```python
a * a_inv
```




    matrix([[ 1.00000000e+00, -4.44089210e-16,  0.00000000e+00],
            [ 0.00000000e+00,  1.00000000e+00,  0.00000000e+00],
            [-2.22044605e-16,  0.00000000e+00,  1.00000000e+00]])



Nota-se pelo resultado que a trata-se da matriz $\mathbf I_{n}$, cujos elementos da diagonal principal têm valor 1 e os demais valor 0. Alguns valores são muito pequenos, mas não exatamente zero, por conta de erros de aproximação durante os cálculos. A seguir avaliamos a produto da inversa $\mathbf A^{-1}$ por $\mathbf A$ e constata-se que o resultado também é a matriz identidade $\mathbf I_{n}$, comprovando-se assim a definição $\mathbf{A} \mathbf{A}^{-1} = \mathbf{A}^{-1} \mathbf{A} = \mathbf {I}_{n}$


```python
a_inv * a
```




    matrix([[ 1.00000000e+00,  0.00000000e+00,  3.33066907e-16],
            [ 2.22044605e-16,  1.00000000e+00, -1.11022302e-16],
            [-6.66133815e-16,  0.00000000e+00,  1.00000000e+00]])



---

## Matriz transposta <a class="anchor" id="transposta"></a>

A transposta de uma matriz, denominada de $\mathbf A^{T}$, é obtida escrevendo-se as suas linhas como colunas.

$$
\large
\mathbf{A} = 
\begin{pmatrix}
a_{11} & a_{12} & ... & a_{1m} \\ 
a_{21} & a_{22} & ... & a_{2m} \\ 
\vdots & \vdots &        & \vdots \\ 
a_{n1} & a_{n2} & ... & a_{nm}
\end{pmatrix}_{n \times m}
\; \; \; \;
\mathbf{A}^{T} = 
\begin{pmatrix}
a_{11} & a_{21} & ... & a_{1n} \\ 
a_{12} & a_{22} & ... & a_{2n} \\ 
\vdots & \vdots &        & \vdots \\ 
a_{1m} & a_{2m} & ... & a_{mn}
\end{pmatrix}_{m \times n}
$$

---
#### <span style="color:red">Exemplo do cálculo da transposta</span>

Calcular a transposta das seguintes matrizes:

$$
\large
\mathbf{A} = 
\begin{pmatrix}
2 \\ 
8
\end{pmatrix}
\; \; \; \;
\mathbf{B} = 
\begin{pmatrix}
1 & 2 & 3 \\ 
4 & 5 & 6 \\
7 & 8 & 9
\end{pmatrix}
$$

temos:

$$
\large
\mathbf{A}^{T} = 
\begin{pmatrix}
2 & 8
\end{pmatrix}
\; \; \; \;
\mathbf{B}^{T} = 
\begin{pmatrix}
1 & 4 & 7 \\ 
2 & 5 & 8 \\
3 & 6 & 9
\end{pmatrix}
$$

Usando o ***numpy*** temos:


```python
a = np.matrix([[2],[8]])
a_t = a.T
print("Matriz A\n", a)
print("\nTransposta de A\n",a_t)
```

    Matriz A
     [[2]
     [8]]
    
    Transposta de A
     [[2 8]]



```python
b = np.matrix([[1,2,3],[4,5,6],[7,8,9]])
b_t = b.T
print("Matriz B\n", b)
print("\nTransposta de B\n",b_t)
```

    Matriz B
     [[1 2 3]
     [4 5 6]
     [7 8 9]]
    
    Transposta de B
     [[1 4 7]
     [2 5 8]
     [3 6 9]]


---

## Sistemas de equações <a class="anchor" id="sistemas"></a>

O uso da notação matricial e as operações com matrizes são muito conveninentes na representação e resolução de sistemas de equações e possuem diversas aplicações.

Um sistema de equações tem a seguinte forma genérica:

$$
\large
\begin{align}
a_{11}x_{1} + a_{12}x_{2} + \dots + a_{1n}x_{n} & = b_{1} \\
a_{21}x_{1} + a_{22}x_{2} + \dots + a_{2n}x_{n} & = b_{2} \\
\vdots \\
a_{n1}x_{1} + a_{n2}x_{2} + \dots + a_{nn}x_{nn} & = b_{n}
\end{align}
$$

<br>
Se convertermos esse sistema para a notação matricial, obtemos:
<br><br>

$$
\large
\begin{pmatrix}
a_{11}x_{1} + a_{12}x_{2} + \dots + a_{1n}x_{n} \\ 
a_{21}x_{1} + a_{22}x_{2} + \dots + a_{2n}x_{n} \\
\vdots \\
a_{n1}x_{1} + a_{n2}x_{2} + \dots + a_{nn}x_{nn}
\end{pmatrix} =
\begin{pmatrix}
b_{1} \\
b_{2} \\
\vdots \\
b_{n}
\end{pmatrix}
$$

<br>
Aplicando-se os conceitos vistos podemos rescrever a notação acima como segue:
<br><br>

$$
\large
\begin{pmatrix}
a_{11} + a_{12} + \dots + a_{1n} \\ 
a_{21} + a_{22} + \dots + a_{2n} \\
\vdots \\
a_{n1} + a_{n2}x_{2} + \dots + a_{nn}
\end{pmatrix}
\begin{pmatrix}
x_{1} \\ 
x_{2} \\
\vdots \\
x_{n}
\end{pmatrix} =
\begin{pmatrix}
b_{1} \\
b_{2} \\
\vdots \\
b_{n}
\end{pmatrix}
$$

<br>
Simplificando a notação, temos:
<br><br>

$$\large \mathbf{A}\mathbf{x} = \mathbf{b}$$

<br>
Agora podemos determinar os valores de $\mathbf x$ aplicando as seguintes transformações:
<br><br>

$$
\large
\begin{align}
\mathbf{A}\mathbf{x} & = \mathbf{b} \\
\mathbf{A}^{-1}\mathbf{A}\mathbf{x} & = \mathbf{A}^{-1}\mathbf{b} \\
\mathbf{I}\mathbf{x} & = \mathbf{A}^{-1}\mathbf{b} \\
\mathbf{x} & = \mathbf{A}^{-1}\mathbf{b} \\
\end{align}
$$


---
#### <span style="color:red">Exemplo de resolução de um sistema de equações</span>

Suponhamos o seguinte sistema de equações:

$$
\large
\begin{align}
2x+3y+z & = -1\\
3x+3y+z & = 1\\
2x+4y+z & = -2
\end{align}
$$

onde queremos determinar o valor de $x$, $y$ e $z$.

Usando a notação matricial podemos escrever:

$$
\large
\begin{pmatrix}
2 & 3 & 1 \\ 
3 & 3 & 1 \\
2 & 4 & 1
\end{pmatrix}
\begin{pmatrix}
x \\ 
y \\
z
\end{pmatrix}
=
\begin{pmatrix}
-1 \\ 
1 \\
-2
\end{pmatrix}
$$

Para resolvermos o sistema de equações basta calcularmos:

$$
\large
\begin{align}
\begin{pmatrix}
x \\ 
y \\
z
\end{pmatrix}
& =
\begin{pmatrix}
2 & 3 & 1 \\ 
3 & 3 & 1 \\
2 & 4 & 1
\end{pmatrix}^{-1}
\begin{pmatrix}
-1 \\ 
1 \\
-2
\end{pmatrix}
\\
\\
\begin{pmatrix}
x \\ 
y \\
z
\end{pmatrix}
& =
\begin{pmatrix}
-1 & 1 & 0 \\ 
-1 & 0 & 1 \\
6 & -2 & -3
\end{pmatrix}
\begin{pmatrix}
-1 \\ 
1 \\
-2
\end{pmatrix}
\\
\\
\begin{pmatrix}
x \\ 
y \\
z
\end{pmatrix}
& =
\begin{pmatrix}
2 \\ 
-1 \\
-2
\end{pmatrix}
\end{align}
$$

Agora vejamos isso usando o ***numpy***.


```python
a = np.matrix([[2,3,1],[3,3,1],[2,4,1]])
b = np.matrix([[-1],[1],[-2]])
np.linalg.inv(a) * b
```




    matrix([[ 2.],
            [-1.],
            [-2.]])



---

## Material útil <a class="anchor" id="material"></a>

### Propriedades <a class="anchor" id="propriedades"></a>

#### Soma de matrizes e multiplicação por escalar

Se $\mathbf A$, $\mathbf B$ e $\mathbf C$ são matrizes $n \times m$ e $c$ e $d$ são escalares, as propriedades a seguir são válidas:


1. Cumulativa da adição: $\color{red}{\mathbf A + \mathbf B = \mathbf B + \mathbf A}$
2. Associativa da adição: $\color{red}{\mathbf A + (\mathbf B + \mathbf C) = (\mathbf A + \mathbf B) + \mathbf C}$ 
3. Associativa da multiplicação: $\color{red}{(cd)\mathbf A = c(d\mathbf A)}$
4. Elemento neutro multiplicativo: $\color{red}{\mathbf I \mathbf A = \mathbf A}$
5. Distributiva: $\color{red}{c(\mathbf A + \mathbf B)= c \mathbf A + c \mathbf B}$
6. Ditributiva: $\color{red}{(c+d)\mathbf A = c \mathbf A + d \mathbf A}$


#### Multipicação de matrizes

Se $\mathbf A$, $\mathbf B$ e $\mathbf C$ são matrizes, com dimensões tais que os produtos das matrizes estejam definidos, e $c$ é um escalar, então as propriedades a seguir são válidas:

1. Associativa da multiplicação: ${\color{red}{\mathbf A(\mathbf B \mathbf C) = (\mathbf A \mathbf B) \mathbf C}}$
2. Distributiva: ${\color{red}{\mathbf A(\mathbf B+\mathbf C) = \mathbf A\mathbf B + \mathbf A\mathbf C}}$
3. Distributiva: ${\color{red}{(\mathbf A + \mathbf B)\mathbf C = \mathbf A\mathbf C + \mathbf B\mathbf C}}$
4. Distributiva: ${\color{red}{c(\mathbf A\mathbf B) = (c\mathbf A)\mathbf B = \mathbf A(c\mathbf B)}}$

#### Matriz identidade

Se a matriz $\mathbf A$ de dimensão $n \times m$, as propriedades a seguir são válidas:

1. $\color{red}{\mathbf A\mathbf I_{m} = \mathbf A}$
2. $\color{red}{\mathbf I_{n}\mathbf A = \mathbf A}$

#### Soma de vetores e multiplicação por escalar em $R^{n}$

Sejam $\mathbf u$, $\mathbf v$ e $\mathbf w$ vetores em $R^{n}$ e $c$ e $d$ escalares, então as propriedades a seguir são válidas:

1. Fechamento para soma: $\color{red}{\mathbf u + \mathbf v \text{ é um vetor em } R^{n}}$
2. Comutativa da soma: $\color{red}{\mathbf u + \mathbf v = \mathbf v  + \mathbf u}$
3. Associativa da soma: $\color{red}{(\mathbf u + \mathbf v) + \mathbf w = \mathbf u + (\mathbf v + \mathbf w)}$
4. Elemento neutro da soma: $\color{red}{\mathbf u + \mathbf 0 = \mathbf u}$
5. Elemento oposto da soma: $\color{red}{\mathbf u + (-\mathbf u) = \mathbf 0}$
6. Fechamento para multiplicação por escalar: $\color{red}{c\mathbf u}$ é um vetor em $\color{red}{R^{n}}$
7. Distributiva: $\color{red}{c(\mathbf u + \mathbf v) = c\mathbf u + c\mathbf v}$
8. Distributiva: $\color{red}{(c+d)\mathbf u = c\mathbf u + d\mathbf u}$
9. Associativa da multiplicação: $\color{red}{c(d\mathbf u) = cd(\mathbf u)}$
10. Elemento neutro multiplicativo: $\color{red}{1(\mathbf u) = \mathbf u}$ 

#### Transposta

Se $\mathbf A$ e $\mathbf B$ são matrizes,  com dimensões tais que os produtos das matrizes estejam definidos, e $c$ é um escalar, então as propriedades a seguir são válidas:

1. Transposta de uma transposta: $\color{red}{(\mathbf{A}^{T})^{T} = \mathbf A}$  
2. Transposta da soma: $\color{red}{(\mathbf A + \mathbf B)^{T} = \mathbf{A}^{T} + \mathbf{B}^{T}}$  
3. Transposta de um produto por escalar: $\color{red}{(c\mathbf A)^{T} = c(\mathbf A)^{T}}$  
4. Transposta de um produto de matrizes: $\color{red}{(\mathbf A \mathbf B)^{T} = \mathbf{B}^{T}\mathbf{A}^{T}}$  

### Referências <a class="anchor" id="referencias"></a>

Larson, R - *Elementos de Algebra Linear* - São Paulo, SP: Cengage, 2017
