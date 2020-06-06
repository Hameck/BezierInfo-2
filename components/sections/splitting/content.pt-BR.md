# Dividir curvas

Usando o algoritmo de Casteljau, também podemos encontrar todos os pontos necessários para dividir uma curva de Bézier em duas curvas menores, que juntas formam a curva original. Quando construímos o esqueleto de Casteljau com algum valor `t`, o procedimento nos fornece todos os pontos necessários para dividir uma curva com esse valor `t`: uma curva é definida por todos os pontos internos do esqueleto encontrados antes da nossa curva ponto, com a outra curva sendo definida por todos os pontos do esqueleto interno após o nosso ponto na curva.

<Graphic title="Dividindo uma curva" setup={this.setupCubic} draw={this.drawSplit} />

<div className="howtocode">

### implementação da divisão de curvas

Podemos implementar a divisão de curvas adicionando um trecho que registra informações na função de Casteljau:

```
left=[]
right=[]
function drawCurve(points[], t):
  if(points.length==1):
    left.add(points[0])
    right.add(points[0])
    draw(points[0])
  else:
    newpoints=array(points.size-1)
    for(i=0; i<newpoints.length; i++):
      if(i==0):
        left.add(points[i])
      if(i==newpoints.length-1):
        right.add(points[i+1])
      newpoints[i] = (1-t) * points[i] + t * points[i+1]
    drawCurve(newpoints, t)
```

Depois de executar esta função para algum valor `t`, os arrays `left` e `right` conterão todas as coordenadas para duas novas curvas - uma "à esquerda" do nosso valor `t` e a outra "à direita". Essas novas curvas terão a mesma ordem que a curva original e podem ser sobrepostas exatamente na curva original.

</div>

Isso é melhor ilustrado com um gráfico animado (clique para reproduzir / pausar):

<Graphic title="Dividindo uma curva de Bézier" setup={this.setupCubic} draw={this.drawAnimated} onClick={this.togglePlay} />
