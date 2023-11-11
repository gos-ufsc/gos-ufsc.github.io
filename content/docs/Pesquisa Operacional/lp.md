---
layout: post
title: Programaçao Linear
date: 2023-11-03 20:04 -0300
---
# Programação Linear, Inteira e Mista

## Introdução

A otimização de sistemas complexos permeia inúmeras aplicações industriais e econômicas. As técnicas de Programação Linear (PL), Inteira (PI) e Mista (PM) servem como pilares no campo da pesquisa operacional. Esta dissertação detalha esses conceitos, seus métodos de resolução e aplicações.

## Programação Linear (PL)

A PL é um método para encontrar o valor máximo ou mínimo de uma função linear sujeita a restrições lineares. A função objetivo e as restrições são representadas por equações ou inequações lineares.

### Método Simplex

O Método Simplex é uma técnica bem estabelecida e amplamente utilizada na programação linear (PL) para encontrar o valor máximo ou mínimo de uma função linear objetivo. Desenvolvido por George Dantzig em 1947, o método permanece um pilar na pesquisa operacional e na ciência da decisão. A abordagem opera iterativamente, movendo-se ao longo das arestas de um poliedro convexo para alcançar o ponto ótimo.

O Método Simplex é utilizado em diversas áreas, como economia, engenharia, transporte e logística. Pode ser usado para resolver problemas como alocação de recursos, otimização de rotas, planejamento de produção, e muito mais.

**Passo 1:** Transformar o problema em forma canônica

O primeiro passo é converter o problema original para uma forma padrão. Isso significa que todas as restrições devem ser convertidas para equações com variáveis não negativas. Fazemos isso introduzindo variáveis "slack" que transformam as inequações em equações.

Por exemplo, a inequação 

$$
3x_1 + 2x_2 \leq 12
$$

pode ser transformada em 

$$
3x_1 + 2x_2 + x_3 = 12, \\
 x_1, x_2, x_3 \geq 0,
$$

onde $x_3$ é a variável slack.

**Passo 2:** Encontrar uma solução básica viável

Uma Solução Básica Viável (SBV) é um ponto no espaço de soluções que satisfaz todas as restrições. Este ponto serve como o ponto de partida para as iterações do Simplex.

- **Método das Duas Fases**: Pode ser usado se uma SBV não for facilmente identificável.
- **Método do Big M**: Outra abordagem utilizada quando uma SBV não é óbvia.

**Passo 3:** Determinar a direção de movimento para melhorar a solução atual

Para melhorar a solução atual, o algoritmo identifica qual variável deve ser aumentada ou diminuída para otimizar a função objetivo. O critério comumente utilizado para isso é a **Regra da Razão Mínima**.

**Passo 4:** Continuar iterando até encontrar a solução ótima

O algoritmo continua movendo-se de vértice em vértice ao longo das arestas do poliedro convexo. Esta iteração continua até que nenhuma melhoria adicional possa ser feita ao valor da função objetivo.

**Critério de Parada**

O algoritmo para de iterar quando todos os coeficientes na linha da função objetivo são não-negativos (no caso de maximização) ou não-positivos (no caso de minimização). Formalmente, se estamos maximizando a função objetivo $Z$, o algoritmo para quando:

$$
\text{Se } c_j \geq 0 \text{ para todo } j, \text{ então a solução ótima foi alcançada.}
$$

Da mesma forma, para minimização:

$$
\text{Se } c_j \leq 0 \text{ para todo } j, \text{ então a solução ótima foi alcançada.}
$$

#### Exemplo

Considere o problema de programação linear abaixo:

$$
\begin{equation}
\begin{array}{llcc}
  \textrm{Maximize} & 5x_1 + 4x_2 + 3x_3 \\\
  \textrm{Sujeito a}: \\\
  & 2x_1 + 3x_2 + x_3 &\leqslant& 5 \\\
  & 4x_1 + x_2 + 2x_3 &\leqslant& 11 \\\
  & 3x_1 + 4x_2 + 2x_3 &\leqslant& 8 \\\
  & x_1, x_2, x_3 \geqslant 0
\end{array}
\label{lb6_eq_pbexsimplex_0}
\end{equation}
$$

Após adicionarmos variáveis de folga, o problema toma a forma a seguir:

$$
\begin{equation}
\begin{array}{l}
\begin{array}{lrrrrrrrrr}
  \textrm{Maximize} & \delta & = & 0 & +& 5x_1 & + & 4x_2 & + & 3x_3 \\\
  \textrm{Sujeito a}: \\\
  & w_1 & = &  5 & - & 2x_1 & - & 3x_2 & - & x_3 \\\
  & w_2 & = & 11 & - & 4x_1 & - &  x_2 & - & 2x_3 \\\
  & w_3 & = & 8  & - & 3x_1 & - & 4x_2 & - & 2x_3 \\\
\end{array}  \\\
  \hspace{2.5cm} x_1, x_2, x_3, w_1, w_2, w_3 \geqslant 0
\end{array}
\label{lb6_pl_1}
\end{equation}
$$

O sistema $\eqref{lb6_pl_1}$ coloca o problema de programação linear em uma forma conhecida por "dicionário'', na qual a função objetivo e um subconjunto de variáveis variáveis básicas com cardinalidade igual ao número de restrições são expressos em termos das variáveis restantes em variáveis não básicas.
As variáveis não básicas assumem valores nulos e, portanto, uma solução pode ser obtida diretamente a partir do dicionário.

Para o dicionário acima, a base é formada pelas variáveis $w_1$, $w_2$ e $w_3$, enquanto que as variáveis não básicas são $x_1$, $x_2$ e $x_3$. Já que as variáveis não básicas assumem valores nulos, obtemos diretamente os valores das variáveis básicas: $w_1 = 5$, $w_2=11$ e $w_3 = 8$.

Note que a solução obtida é factível para o problema em questão uma vez que todas as variáveis (básicas e não básicas) são não negativas.
Além disso, a função objetivo corrente tem valor $\delta = 0$.

O método Simplex é um processo iterativo que inicia com uma solução $y^0 = (x_1^0\ \ldots\ x_n^0\ w_1^0\ \ldots\ w_m^0)^T$, onde $n=3$e$m=3$, satisfazendo as equações de $\eqref{lb6_eq_pbexsimplex_0}$.

Partindo do dicionário $\eqref{lb6_pl_1}$, o Simplex busca uma nova solução $y^1$tal que:$5 x_1^1 + 4x_2^1 + 3x_3^1 > 5 x_1^0 +4x_2^0 + 3x_3^0$. Para tanto, é necessário fazer uma solução não básica com coeficiente positivo na equação de $\delta$ entrar na base que, por sua vez, fará a variável não básica aumentar e consequentemente elevar o valor da função objetivo. Obviamente, a variável que entra na base não pode aumentar seu valor indefinidamente, a menos que o problema seja ilimitado. A primeira variável básica a se tornar nula  passa a ser uma variável não básica na iteração seguinte. O processo então se repete até que se convirja para  uma solução ótima ou até que se detecte que o problema é ilimitado.

**Inicialização:** Para iniciarmos o processo, necessitamos de uma solução factível, tal como:

$$
x_1^0 = 0,\ x_2^0 = 0,\ x_3^0 = 0,\ w_1^0 = 5,\ w_2^0 = 11,\ w_3^0 = 8
$$

Esta solução $y^0$ induz o valor $\delta = 0$ para a função objetivo.

**Passo 1:** A solução corrente não é ótima. Qualquer acréscimo no valor de $x_1$aumenta o valor de$\delta$. Mas não podemos aumentar o valor de $x_1$ ilimitadamente já que este está limitado pelas desigualdades abaixo:

$$
\left \\{ \begin{array}{rcrrr}
  w_1 &=& 5 - 2x_1 & \geqslant & 0 \\\
  w_2 &=& 11 -4x_1 & \geqslant & 0 \\\
  w_3 &=& 8 -3x_1 & \geqslant & 0
\end{array}
\right . \Rightarrow \left \\{ \begin{array}{lllcr}
 x_1 & \leqslant & 5/2 &=& 2.5 \\\
 x_1 & \leqslant & 11/4 &=& 2.75 \\\
 x_1 & \leqslant & 8/3 &=& 2.667
\end{array}
\right .
$$

Assim, o valor de $x_1$ na próxima iteração é o menor dentre $\{5/2, 11/4, 8/3\}$, o que leva a igualdade:

$$
\begin{equation}
 x_1  =  \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2 -\frac{1}{2}x_3
\label{lb6_eqpl_2}
\end{equation}
$$

Substituindo-se $\eqref{lb6_eqpl_2}$ no sistema $\eqref{lb6_pl_1}$ de maneira atransferir-se a variável$w_1$ para o lado direito, obtém-se:

$$
\begin{equation}
\begin{array}{lll}
  x_1 & = & \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2 -\frac{1}{2}x_3 \\\
  w_2 & = & 11 - 4\left ( \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2 -\frac{1}{2}x_3
​       \right ) - x_2 - 2x_3 \\\
​     & = & 1 + 2w_1 + 5x_2 \\\
  w_3 & = & 8 - 3 \left ( \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2 -\frac{1}{2}x_3
​       \right ) - 4x_2 - 2x_3 \\\
​      & = & \frac{1}{2} + \frac{3}{2}w_1 + \frac{1}{2}x_2 - \frac{1}{2}x_3 \\\
  \delta & = & 5 \left (  \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2 -\frac{1}{2}x_3
​       \right )
​         + 4x_2 + 3x_3 \\\
​    & = & \frac{25}{2} - \frac{5}{2} w_1 -\frac{7}{2} x_2 +
​             \frac{1}{2}x_3
\end{array} \label{lb6_eqpl_3}
\end{equation}
$$

Agora, substituindo as equações $\eqref{lb6_eqpl_3}$ no "dicionário'' (\ref{lb6_pl_1}), obtém-se o dicionário abaixo:

$$
\begin{equation}
\begin{array}{lrrrrrr}
\textrm{Max} & \delta &=& \frac{25}{2} & -\frac{5}{2}w_1 & -\frac{7}{2}x_2 & +\frac{1}{2}x_3 \\\
 & x_1 &=& \frac{5}{2} & -\frac{1}{2}w_1 & -\frac{3}{2}x_2 & -\frac{1}{2}x_3 \\\
 & w_2 &=& 1 & +2w_1 & + 5x_2 \\\
 & w_3 &=& \frac{1}{2} & + \frac{3}{2}w_1 & + \frac{1}{2}x_2 & -\frac{1}{2}x_3\\\
\end{array} \label{lb6_pl_2}
\end{equation}
$$

A solução induzida pelo dicionário $\eqref{lb6_pl_2}$ é 

$$
y^1 =
(x_1^1, x_2^1, x_3^1, w_1^1, w_2^1, w_3^1) =
 ( \frac{5}{2}, 0, 0, 0, 1, \frac{1}{2})
$$

cujo valor da função objetivo é $\delta = \frac{25}{2}$.

Neste dicionário, as variáveis $x_1$, $w_2$, e $w_3$ são ditas variáveis básicas tal que o conjunto $\mathbb{B} = \{x_1, w_2, w_3\}$ contém as variáveis básicas. As demais variáveis são ditas não básicas, sendo o conjunto $\mathbb{N} = \{x_2, x_3, w_1\}$ o conjunto das variáveis não básicas.

**Passo 2:** A solução corrente não é ótima! Note que um pequeno acréscimo no valor de $x_3$ invariavelmente aumenta o valor de $\delta$.

Mas não podemos aumentar o valor de $x_3$ ilimitadamente uma vez que isto poderia tornar a solução infactível (outras variáveis poderiam assumir valores negativos).

Para que a solução resultante seja factível, as desigualdades abaixo devem ser respeitadas:

$$
\left \\{
\begin{array}{cclll}
 x_1 &=& \frac{5}{2} - \frac{1}{2}x_3 & \geqslant & 0 \\\
 w_3 &=& \frac{1}{2} - \frac{1}{2}x_3 & \geqslant & 0
\end{array}
\right .
\Rightarrow
\left \\{
\begin{array}{lll}
 x_3 \leqslant 5 \\\
 x_3 \leqslant 1
\end{array}
\right .
$$

Portanto, $w_3$ deve sair da base para que a variável $x_3$ possa entrar na base sem violar as restrições.

Após substituirmos a equação $x_3 = 1 + 3w_1 + x_2 - 2w_3$ nas equações do dicionário $\eqref{lb6_pl_2}$, obtemos:

$$
\begin{equation}
\begin{array}{lll}
 x_1 & = & \frac{5}{2} - \frac{1}{2}w_1 - \frac{3}{2}x_2
​         - \frac{1}{2}\left ( 1 + 3w_1 + x_2 - 2w_3 \right ) \\\
   & = & 2 - 2w_1 - 2x_2 + w_3 \\\
 \\\
 \delta & = & \frac{25}{2} - \frac{5}{2}w_1 - \frac{7}{2}x_2
​     + \frac{1}{2} \left ( 1 + 3w_1 + x_2 - 2w_3 \right ) \\\
   & = & 13 - w_1 - 3x_2 - w_3
\end{array}  \label{lb6_eqpl_4}
\end{equation}
$$

Substituindo as equações do dicionário $\eqref{lb6_pl_2}$ pelas equações $\eqref{lb6_eqpl_4}$ obtemos um novo dicionário:

$$
\begin{equation}
\begin{array}{lrrrrrr}
\textrm{Max} & \delta &=&  13 & - w_1 & - 3x_2 & - w_3 \\\
 & x_1 &=&  2 &- 2w_1 &- 2x_2 &+ w_3  \\\
 & w_2 &=&  1 & +2w_1 & + 5x_2 \\\
 & x_3 &=&  1 &+ 3w_1 &+ x_2 &- 2w_3\\\
\end{array} \label{lb6_pl_5}
\end{equation}
$$

cuja base é $\mathbb{B} = \{x_1, x_3, w_2\}$.

A solução dada pelo dicionário $\eqref{lb6_pl_5}$ é ótima: $x_1 = 2$, $x_2 = 0$, $x_3 = 1$, $w_1 = 0$, $w_2 = 1$, $w_3 = 0$, e $\delta = 13$é uma solução ótima pois os coeficientes das variáveis não básicas na equação de $\delta$, no dicionário correspondente dado pelo sistema $\eqref{lb6_pl_5}$, são todos negativos;  aumentando o valor de qualquer variável não básica reduzirá o valor da função objetivo.

---


### Dualidade em Programação Linear

A dualidade é um conceito fundamental em programação linear que oferece uma relação simbiótica entre um problema de otimização original (chamado problema primal) e um problema derivado (chamado problema dual). Este relacionamento permite que insights e soluções sejam transferidos de um problema para o outro.

O problema primal em Programação Linear pode ser formulado da seguinte maneira:

$$
\begin{align*}
& \text{minimizar } & c^T x \\
& \text{s.a. } & Ax \geq b \\
& x \geq 0
\end{align*}
$$

onde $c \in \mathbb{R}^n$, $x \in \mathbb{R}^n$, $A \in \mathbb{R}^{m \times n}$e$b \in \mathbb{R}^m$.

**Dual através do Lagrangeano**

Para construir o problema dual através da teoria do Lagrangeano, introduzimos multiplicadores Lagrangeanos $\lambda \geq 0$ para as restrições $Ax \geq b$.

O Lagrangeano $L(x, \lambda)$ é então dado por:

$$
L(x, \lambda) = c^T x - \lambda^T (Ax - b)
$$

**Problema Dual de Lagrange**

O problema dual associado envolve a maximização do limite inferior do problema primal, dado por:

$$
\begin{align*}
\text{maximizar } & \inf_x L(x, \lambda) \\
\text{s.a. } & \lambda \geq 0
\end{align*}
$$

Para resolver isso, precisamos encontrar o infimo de $L(x, \lambda)$para cada$\lambda$. No caso da programação linear, isso é feito resolvendo:

$$
\inf_x L(x, \lambda) = \inf_x (c^T x - \lambda^T (Ax - b))
$$

Se $\lambda \geq 0$, então o infimo é alcançado quando $Ax = b$ se tal $x$ existir, ou$-\infty$ caso contrário. Portanto, o problema dual se torna:

$$
\begin{align*}
\text{maximizar } & b^T \lambda \\
\text{s.a. } & A^T \lambda \leq c \\
& \lambda \geq 0
\end{align*}
$$

**Relações entre Primal e Dual**

1. **Dual Unbounded**: Se o problema dual é ilimitado, então isso implica que o problema primal é inviável.

2. **Dual Optimal**: Se o problema dual tem uma solução ótima, então o problema primal também tem, e seus valores objetivos são iguais. Isso é conhecido como "dualidade forte".

**Variáveis Básicas e Não Básicas**

Na programação linear, especialmente na forma padrão, uma base $B$ é um conjunto de $m$ colunas linearmente independentes de $A$. As variáveis correspondentes a essas colunas são chamadas de variáveis básicas. O restante das variáveis são chamadas de variáveis não básicas e são geralmente definidas como zero para encontrar uma solução básica viável.

**Custos Reduzidos**

O custo reduzido $d_j$ de uma variável não básica $x_j$ em um simplex é dado por:

$$
d_j = c_j - \sum_{i=1}^{m} \lambda_i A_{ij}
$$

onde $c_j $é o coeficiente de custo da variável $ x_j $ e $ \lambda $ é o vetor de preços sombra. $ d_j $fornece informações sobre o quanto a função objetivo irá melhorar se$ x_j $ for aumentada a partir de zero.

#### Dualidade Fraca

A dualidade fraca, em termos de variáveis básicas e custos reduzidos, pode ser vista como uma afirmação de que se $\lambda$ é uma solução viável do dual, então $c_B = \lambda^T B$ (onde $c_B$ são os custos das variáveis básicas e $B$ é a matriz básica), e $d_j \geq 0$ para todas as variáveis não básicas $x_j$.

$$
d_j = c_j - \lambda^T A_{*j} \geq 0, \quad \forall j \in \text{variáveis não básicas}
$$

#### Dualidade Forte

Se $\lambda^{\star} $ e $x^{\star} $ são soluções ótimas para o dual e o primal, respectivamente, e ambos os problemas têm uma solução finita, então:

$$
c^T x^* = b^T \lambda^\star
$$

Isso implica que os custos reduzidos para todas as variáveis não básicas devem ser exatamente zero, e $\lambda^\star$ deve satisfazer $c_B = \lambda^{\star T} B$.

#### Complementaridade Slack

Na solução ótima, as condições de complementaridade slack são satisfeitas:

$$
d_j \cdot x^*_j = 0, \quad \forall j
$$

$$
\lambda_i^* \cdot s_i = 0, \quad \forall i
$$

Aqui $s_i$ é a folga na restrição $i$-ésima do primal, e $\lambda_i^\star$ é o multiplicador de Lagrange dual associado a essa restrição. Isso significa que se uma variável não básica $x_j$ é positiva na solução ótima, então o custo reduzido correspondente $d_j$ deve ser zero.

Essas são maneiras mais rigorosas de ver a dualidade e a complementaridade slack em termos de programação linear, levando em consideração as variáveis básicas e os custos reduzidos.


#### Importância da Dualidade

**Eficiência Computacional:** Às vezes, o problema dual pode ser mais fácil de resolver do que o primal. Resolver um leva automaticamente à solução do outro.

**Insights Econômicos:** A dualidade pode oferecer interpretações econômicas, como a relação entre recursos e preços.

**Sensibilidade e Análise Pós-Otimização:** A dualidade auxilia na análise de como mudanças nos parâmetros afetam a solução ótima.

---

### Implementação Real do Simplex Dual e Suas Utilidades

O algoritmo Simplex é uma das ferramentas mais poderosas em pesquisa operacional e otimização. No entanto, a implementação real do Simplex, especialmente a versão dual, vai além do algoritmo básico ensinado em cursos introdutórios. Vamos explorar algumas das técnicas avançadas e "truques" usados na indústria.

#### Utilidade em Branch-and-Bound

O Simplex Dual é particularmente útil em métodos de Branch-and-Bound para resolver problemas de programação inteira. Uma das principais vantagens é que ele permite a adição de restrições adicionais ao problema sem perder a factibilidade do tableau do Simplex. Isso é crucial em Branch-and-Bound, onde frequentemente adicionamos restrições para dividir o espaço de soluções.

#### Steepest Edge Rule

Na implementação padrão do Simplex, a escolha da variável a entrar na base é feita com base no custo reduzido. No entanto, essa abordagem nem sempre é a mais eficiente. A regra do "Steepest Edge" escolhe a variável que maximiza o avanço na direção do gradiente do objetivo. Isso pode acelerar a convergência do algoritmo.

#### Pricing Strategies

Em problemas grandes, calcular o custo reduzido para todas as variáveis pode ser computacionalmente caro. Estratégias de "pricing" como o Devex pricing ou o método de múltiplos pivôs são usadas para tornar essa etapa mais eficiente.

#### Degeneracy and Anti-cycling

A degenerescência é um problema bem conhecido no Simplex, podendo levar a um grande número de iterações. Técnicas como a regra de Bland ou perturbações lexicográficas são usadas para evitar ciclos infinitos.

#### Warm Starts

Em cenários onde o modelo é resolvido várias vezes com pequenas modificações, como em algoritmos de decomposição, o "warm start" pode ser usado para iniciar o Simplex Dual a partir de uma solução factível próxima, economizando tempo de computação.

#### Paralelização e Distribuição

O Simplex Dual também pode ser adaptado para execução em paralelo ou em ambientes distribuídos, embora isso possa ser bastante desafiador devido à natureza sequencial do algoritmo.

Essas técnicas e estratégias tornam o Simplex Dual uma ferramenta poderosa e flexível, adaptável a uma ampla gama de problemas industriais e de pesquisa.

---

### Degeneração

O método Simplex é um algoritmo popular para resolver problemas de programação linear. Embora seja extremamente eficiente na prática, há casos em que o método pode ser ineficiente devido à degeneração. Degeneração ocorre quando o método Simplex visita mais de um vértice adjacente que tem o mesmo valor da função objetivo, potencialmente causando um número excessivo de iterações.

**Definição Matemática da Degeneração**

Em qualquer iteração do método Simplex, uma solução básica factível (BFS) é obtida, e a degeneração ocorre quando essa BFS tem mais de um vértice adjacente com o mesmo valor da função objetivo.

**Consequências**

- **Ciclagem:** Em casos raros, o método Simplex pode entrar em um ciclo infinito, o que é mais provável em problemas degenerados.

- **Ineficiência Computacional:** Mesmo que a ciclagem não ocorra, a degeneração pode causar um aumento no número de iterações necessárias para encontrar a solução ótima.

**Estratégias para Lidar com Degeneração**

1. **Regra do Menor Índice**: Escolher o vértice adjacente de menor índice se houver empate na razão mínima pode evitar a ciclagem.

2. **Perturbação**: Adicionar uma pequena quantidade $\epsilon$ao lado direito$b$ pode remover a degeneração, mas pode introduzir erros na solução.

3. **Método de Bland**: Este é um critério de seleção de variável específico que garante a terminação do método Simplex, mesmo na presença de degeneração.

4. **Revisão Lexicográfica**: Esta é uma outra maneira de resolver empates em degeneração, considerando múltiplos critérios em vez de apenas um.

O problema de degeneração é um aspecto importante do método Simplex que pode afetar a eficiência do algoritmo. No entanto, várias estratégias podem ser empregadas para lidar com esta questão, tornando o método Simplex uma ferramenta robusta para resolver problemas de programação linear.

---

### Shadow Price

O conceito de "shadow price" ou "preço sombra" é um conceito-chave na programação linear e na otimização. Em termos simples, o shadow price associa um valor à restrição de um recurso limitado em um problema de otimização. Esse valor representa quanto a função objetivo irá melhorar (ou piorar) com uma unidade adicional do recurso.

**Definição Matemática**

Considere um problema de programação linear em forma padrão:

$$
\begin{align} 
\text{maximizar } Z = c_1 x_1 + c_2 x_2 + \ldots + c_n x_n  \nonumber \\\
a_{11} x_1 + a_{12} x_2 + \ldots + a_{1n} x_n  \leq b_1,  \nonumber \\\
a_{21} x_1 + a_{22} x_2 + \ldots + a_{2n} x_n  \leq b_2,  \nonumber \\\
\vdots  \vdots  \nonumber \\\
a_{m1} x_1 + a_{m2} x_2 + \ldots + a_{mn} x_n  \leq b_m,  \nonumber \\\
x_1, x_2, \ldots, x_n \geq 0 \nonumber 
\end{align}
$$

Onde:

- $Z$ é a função objetivo
- $x_1, x_2, \ldots, x_n$ são as variáveis de decisão
- $c_1, c_2, \ldots, c_n$ são os coeficientes da função objetivo
- $a_{ij}$ são os coeficientes das restrições
- $b_1, b_2, \ldots, b_m$ são os limites das restrições

O "shadow price" $\lambda_i$ da i-ésima restrição é definido como a taxa de variação da função objetivo ótima $Z$ com relação a uma pequena variação na i-ésima restrição $b_i$. Ou seja, matematicamente:

$$
\frac{dZ}{db_i} = \lambda_i
$$

- **Interpretação Econômica**

Em um contexto econômico, o "shadow price" pode ser interpretado como o valor adicional que um objetivo derivado (como o lucro) poderia ganhar se uma unidade adicional de um recurso (como mão-de-obra, material, etc.) fosse disponibilizada.

- **Nota**

É importante observar que os shadow prices são válidos apenas dentro de uma região específica em torno da solução ótima. Se a variação em $b_i$ é muito grande, o modelo pode precisar ser resolvido novamente para obter novos shadow prices.

---

### Método Matricial do Simplex

O Método Matricial do Simplex é uma forma de implementar o algoritmo Simplex usando matrizes, o que torna mais fácil a computação e a automação do método. Nesta abordagem, todas as informações sobre as restrições e a função objetivo são armazenadas em matrizes, e as operações matriciais são usadas para navegar pelo espaço de soluções até encontrar a solução ótima.

**Forma Padrão do Problema**

Para o Método Matricial do Simplex, é crucial que o problema de programação linear esteja em forma padrão. Um problema de maximização em forma padrão pode ser representado como:

$$
\begin{align*}
\text{Maximizar: }  Z = c_1x_1 + c_2x_2 + \ldots + c_nx_n \\
\text{Sujeito a: }  Ax = b \\
 x \geq 0
\end{align*}
$$

Aqui, $A$ é a matriz das restrições, $x$ é o vetor coluna das variáveis de decisão, $b$ é o vetor coluna dos termos constantes das restrições e $c$ é o vetor linha dos coeficientes da função objetivo.

**Inicialização**

1. Escolher uma solução básica viável inicial, frequentemente dada pela matriz identidade.
2. Calcular o custo relativo $\bar{c}$ usando a fórmula $\bar{c} = c - B^{-1}AN$, onde $B$ é a matriz das variáveis básicas e $N$ é a matriz das variáveis não-básicas.

**Iteração**

Para cada iteração, siga os seguintes passos:

1. **Identificar a variável a entrar na base**: Selecionar $j$ tal que $\bar{c}_j < 0$ (para maximização).
2. **Identificar a variável a sair da base**: Utilizar a Regra da Razão Mínima. Calcular $\Delta x_B = B^{-1}a_j$ e escolher $i$ tal que $\frac{\Delta x_{B_i}}{x_{B_i}}$ seja mínimo.
3. **Atualizar a base**: Utilizar transformações de Gauss-Jordan para atualizar $B$.

**Critério de Parada**

O algoritmo para quando $\bar{c} \geq 0$ para todas as componentes (em um problema de maximização), indicando que a solução ótima foi alcançada.

Deste modo, o Método Matricial do Simplex permite uma execução mais eficiente e precisa do algoritmo Simplex, especialmente quando se trata de problemas de grande escala.

---

### Outros

**Desafios e Limitações**

**Complexidade Computacional:** Em casos muito raros, o algoritmo pode ter uma complexidade exponencial, embora na maioria das situações seja altamente eficiente.

---

## Programação Inteira (PI)

A Programação Inteira é uma extensão da Programação Linear onde as variáveis de decisão são restritas a serem inteiros. A formulação matemática básica para um problema de Programação Inteira é:

$$
\begin{align*}
\text{minimizar } & c^T x \\
\text{s.a. } & Ax \geq b \\
& x \in \mathbb{Z}^n
\end{align*}
$$

Aqui, $\mathbb{Z}^n$ indica que as variáveis de decisão $x$ são inteiras.

### Arredondamento em LP e Falhas

A abordagem de arredondamento pode falhar de várias maneiras. Uma delas é que o arredondamento da solução ótima de um LP pode resultar em uma solução inviável para o PI original. Além disso, mesmo que seja viável, não há garantia de que a solução arredondada seja ótima.

Suponha que a solução ótima para o LP relaxado seja $x^*$ e após o arredondamento obtenhamos $\hat{x}$. A seguinte desigualdade pode ocorrer:

$$
c^T \hat{x} > c^T x^* \geq \text{OPT}_{\text{PI}}
$$

onde $\text{OPT}_{\text{PI}}$ é o valor ótimo do problema de PI.

### Formulação Ideal e $\text{conv}(X)$

Para qualquer problema de Programação Inteira, o conjunto $X$ é o conjunto de todas as soluções inteiras viáveis. O fechamento convexo deste conjunto, $\text{conv}(X)$, é a menor região convexa que contém todas as soluções inteiras. Em termos matemáticos:

$$
\text{conv}(X) = \text{convex hull}(X) = \left \\{ \sum_{i=1}^{k} \lambda_i x_i \,|\, x_i \in X, \, \lambda_i \geq 0, \, \sum_{i=1}^{k} \lambda_i = 1 \right \\}
$$

A formulação ideal para um problema de PI é aquela cujo conjunto viável é exatamente $\text{conv}(X)$.

O poliedro integral é essencialmente o poliedro $\text{conv}(X)$ e é útil porque quaisquer pontos extremos desse poliedro são soluções inteiras. O objetivo ao resolver problemas de PI muitas vezes é encontrar uma representação deste poliedro integral ou aproximar-se dele de forma eficaz.

### Relação com LP

Métodos como o branch-and-bound ou o branch-and-cut são técnicas comuns para resolver problemas de PI, e esses métodos frequentemente usam soluções de problemas de LP como subproblemas. Esses métodos tentam aproximar $\text{conv}(X)$ de forma eficiente para encontrar uma solução ótima do problema de PI.

---

## Programação Inteira-Mista (MIP)

A PM permite uma combinação de variáveis contínuas e inteiras, possibilitando maior flexibilidade na modelagem de problemas complexos.

O uso de métodos híbridos, combinando aspectos do Simplex com técnicas de PI, permite resolver problemas de PM.

### Branch-and-Bound

**Inicialização:**

- Relaxação Linear: Comece resolvendo a relaxação linear do problema original, ou seja, o problema sem as restrições de integralidade. Isso fornece uma solução contínua que serve como um limite superior inicial (para problemas de minimização) ou limite inferior (para problemas de maximização).
- Seleção do Nó Raiz: O problema relaxado é o nó raiz da árvore de pesquisa.

**Ramificação (Branching):**

- Seleção de Variável: Escolha uma variável que tenha um valor fracionário na solução ótima da relaxação linear.

- Divisão: Crie dois subproblemas (nós filhos), um com a restrição de que a variável selecionada seja arredondada para baixo e outro com a restrição de que seja arredondada para cima.

- Construção da Árvore de Pesquisa: Esses subproblemas tornam-se nós em uma árvore de pesquisa, onde o nó raiz é o problema original e os nós folha são problemas com todas as variáveis inteiras.

**Avaliação de Limites (Bounding):**

- Cálculo de Limites: Resolva a relaxação linear de cada subproblema para obter limites para a solução ótima.
- Corte (Pruning): Se o limite de um subproblema for pior que a melhor solução inteira encontrada até agora, esse subproblema pode ser descartado.

**Seleção de Nós:**

- Estratégia de Seleção: Escolha o próximo nó a ser explorado com base em uma estratégia, como "melhor limite primeiro" ou "profundidade primeiro".
- Exploração: Explore a árvore de pesquisa seguindo a estratégia de seleção, repetindo as etapas de ramificação e corte.

**Terminação:**

- Condição de Parada: Continue o processo até que não haja mais nós a serem explorados ou até que outros critérios de parada sejam atendidos.
- Solução Ótima: A melhor solução inteira encontrada durante o processo é a solução ótima.

#### Exemplo

Vamos considerar um pequeno problema de programação inteira mista:

$$
\begin{align*}
\text{maximizar } & z = x + 2y \\\
\text{s.a. } & x + y \leq 1.5 \\\
& x, y \geq 0 \\\
& x \in \mathbb{R}, \, y \in \mathbb{Z}
\end{align*}
$$

Aqui, $x$ é uma variável contínua e $y$ é uma variável inteira.

**Inicialização**
Primeiro, resolvemos a relaxação linear do problema:

$$
\begin{align*}
\text{maximizar } & z = x + 2y \\\
\text{s.a. } & x + y \leq 1.5 \\\
& x, y \geq 0
\end{align*}
$$

A solução ótima da relaxação é $x^* = 1, y^* = 0.5$ com $z = 2$. Como $y$ é fracionário, precisamos continuar.

**Ramificação (Branching)**

Selecionamos $y$ para ramificação.

1. No primeiro subproblema, $y$ é arredondado para baixo, i.e., $y \leq 0$.
2. No segundo subproblema, $y$ é arredondado para cima, i.e., $y \geq 1$.

**Avaliação de Limites (Bounding)**

1. No primeiro subproblema (com $y=0$), a solução ótima é $x = 1.5, y = 0$ com $z = 1.5$.
2. No segundo subproblema (com $y=1$), a solução ótima é $x = 0.5, y = 1$ com $z = 2.5$.

Como $z = 2.5$ é a solução inteira com maior valor para nosso problema de maximização, ela é a solução ótima do problema PI.

**Conclusão**

Pelo método de branch-and-bound, determinamos que a solução ótima do problema de PI é $x = 0.5, y = 1$ com $z = 2.5$.

#### Vantagens e Desvantagens

**Vantagens:**

- Garante a obtenção da solução ótima global.
- Pode ser mais eficiente que a enumeração exaustiva.

**Desvantagens:**

- Pode ser computacionalmente caro para problemas grandes.
- A eficiência depende da estratégia de seleção e da qualidade dos limites.

A Programação Linear, Inteira e Mista abarca uma gama rica e diversificada de técnicas de otimização. Os algoritmos e métodos associados a essas técnicas oferecem soluções práticas e eficazes para uma variedade de problemas complexos encontrados em campos como engenharia, economia e ciências sociais.




