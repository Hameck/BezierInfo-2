# Algoritmo de "de Casteljau"

Se quisermos desenhar curvas de Bézier, podemos percorrer todos os valores de `t` de 0 a 1 e depois calcular a função de base ponderada em cada valor, obtendo os valores de `x/y` que precisamos plotar. Infelizmente, quanto mais complexa a curva fica, mais caro esse cálculo se torna. Em vez disso, podemos usar o *algoritmo de "de Casteljau"* para desenhar curvas. Essa é uma abordagem geométrica para desenhar curvas, e é realmente fácil de implementar. Tão fácil, de fato, que você pode fazer isso manualmente com um lápis e uma régua.

Em vez de usar nossa função de cálculo para encontrar valores `x/y` para `t`, vamos fazer isso:

- trate `t` como uma razão (e, de fato, é). t=0 é 0% ao longo de uma linha, t=1 é 100% ao longo de uma linha.
- Pegue todas as linhas ligando os pontos de definição da curva. Para uma curva da ordem `n`, são` n` linhas.
- Coloque marcadores ao longo de cada uma dessas linhas, na distância `t`. Portanto, se `t` é 0,2, coloque a marca em 20% desde o início e 80% no final.
- Agora forme linhas entre os `novos` pontos. Isso fornece linhas `n-1`.
- Coloque marcadores ao longo de cada uma dessas linhas na distância `t`.
- Formar linhas entre os `novos` pontos. Serão linhas `n-2`.
- Coloque marcadores, linhas de formulário, marcadores, etc.
- Repita isso até que você tenha apenas uma linha restante. O ponto `t` nessa linha coincide com o ponto da curva original em `t`.

<div className="howtocode">

### Como implementar o algoritmo de "de Casteljau"

Vamos usar o algoritmo que acabamos de especificar e implementá-lo:

```
function drawCurve(points[], t):
  if(points.length==1):
    draw(points[0])
  else:
    newpoints=array(points.size-1)
    for(i=0; i<newpoints.length; i++):
      newpoints[i] = (1-t) * points[i] + t * points[i+1]
    drawCurve(newpoints, t)
```

E pronto, esse é o algoritmo implementado. Exceto que geralmente você pode ser dar ao luxo de sobrecarregar("overload") o operador "+", então também fornecemos o código para quando você precisar trabalhar com os valores `x` e `y`:

```
function drawCurve(points[], t):
  if(points.length==1):
    draw(points[0])
  else:
    newpoints=array(points.size-1)
    for(i=0; i<newpoints.length; i++):
      x = (1-t) * points[i].x + t * points[i+1].x
      y = (1-t) * points[i].y + t * points[i+1].y
      newpoints[i] = new point(x,y)
    drawCurve(newpoints, t)
```

Então, o que isso faz? Isso desenha um ponto, se a lista de pontos passada tiver apenas 1 ponto. Caso contrário, ele criará uma nova lista de pontos que estão nas proporções <i>t</i> (ou seja, os "marcadores" descritos no algoritmo acima) e, em seguida, chamará a função draw para esta nova lista.

</div>

Para ver isso em ação, passe o mouse sobre o seguinte esboço. Mover o mouse altera o ponto da curva explicitamente avaliado usando o algoritmo de "de Casteljau", mover o cursor da esquerda para a direita (ou, é claro, da direita para a esquerda), mostra como uma curva é gerada usando essa abordagem.

<Graphictitle="Percorrendo uma curva usando o algoritmo de "de Casteljau"" setup={this.setup} draw={this.draw}/>
