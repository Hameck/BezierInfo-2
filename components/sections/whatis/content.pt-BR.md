# Então o que faz uma Curva de Bézier?

Brincar com os pontos das curvas pode lhe dar uma ideia de como as curvas de Bézier se comportam, mas o que *são* realmente as curvas de Bézier? Existem duas maneiras de explicar o que é uma curva de Bézier, e elas acabam sendo equivalentes, mas uma delas usa uma matemática mais complicada e a outra usa uma realmente simples. Então ... vamos começar com a explicação simples:

Curvas de Bézier são o resultado de [interpolações lineares](https://en.wikipedia.org/wiki/Linear_interpolation). Isso parece complicado, mas você faz interpolação linear desde criança: sempre que precisava apontar algo entre duas coisas, aplicava interpolação linear. É simplesmente "escolher um ponto entre dois pontos".

Se soubermos a distância entre esses dois pontos e desejarmos um novo ponto que seja, digamos, a 20% de distância do primeiro ponto (e, portanto, a 80% de distância do segundo ponto), poderemos calcular isso com muita facilidade :

\[
Given \left (
  \begin{aligned}
    p_1 &= algum\ ponto \\
    p_2 &= algum\ outro\ ponto \\
    distancia &= (p_2 - p_1) \\
    razão &= \frac{percentage}{100} \\
  \end{aligned}
\right ),\ nosso\ novo\ ponto = p_1 + distancia \cdot ratio
\]

Então, vejamos isso em ação: o gráfico a seguir é interativo, pois você pode usar as teclas de seta para cima e para baixo para aumentar ou diminuir a taxa de interpolação e ver o que acontece. Começamos com três pontos, o que nos dá duas linhas. A interpolação linear sobre essas linhas nos dá dois pontos, entre os quais podemos executar novamente a interpolação linear, produzindo um único ponto. E esse ponto — e todos os pontos que podemos formar dessa maneira para todas as razões juntas — formam nossa curva de Bézier:

<Graphic title="Interpolação linear levando a curvas de Bézier" setup={this.setup} draw={this.draw} onKeyDown={this.onKeyDown}/>

E isso nos leva à matemática complicada: cálculo.

Embora não pareça que foi o que acabamos de fazer, na verdade apenas desenhamos uma curva quadrática, em etapas, e não de uma só vez. Uma das partes fascinantes das curvas de Bézier é que ambas podem ser descritas em termos de funções polinomiais, bem como em termos de interpolações muito simples de interpolações de [...]. Isso, por sua vez, significa que podemos ver o que essas curvas podem fazer com base nas "matemáticas reais" (examinando as funções, suas derivadas e todas essas coisas), bem como na composição "mecânica" (que nos diz, por exemplo, que uma curva nunca se estenderá além dos pontos que usamos para construí-la).

Então, vamos começar a examinar as curvas de Bézier um pouco mais profundamente: suas expressões matemáticas, as propriedades que podemos derivar delas e as várias coisas que podemos fazer com as curvas de Bézier.