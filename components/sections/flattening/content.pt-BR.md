# Desenho simplificado

Também podemos simplificar o processo de desenho tirando "amostras" da curva em determinados pontos e juntando esses pontos com linhas retas, um processo conhecido como "discretização", pois estamos reduzindo uma curva a uma sequência simples de segmentos de reta.

Podemos fazer isso dizendo "queremos X segmentos" e, em seguida, amostrando a curva em intervalos igualmente espaçados, de modo que terminemos com o número de segmentos que desejávamos. A vantagem desse método é que ele é rápido: em vez de avaliar 100 ou mesmo 1000 coordenadas da curva, podemos obter um número muito menor e ainda terminar com uma curva que parece boa o suficiente. A desvantagem, é claro, é que perdemos a precisão de trabalhar com "a curva real"; portanto, geralmente não podemos usar a curva achatada para realizar uma verdadeira detecção de interseção ou alinhamento de curvatura.

<Graphic title="Discretizando uma curva quadrática" setup={this.setupQuadratic} draw={this.drawFlattened} onKeyDown={this.onKeyDown}/>
<Graphic title="Discretizando uma curva cúbica" setup={this.setupCubic} draw={this.drawFlattened} onKeyDown={this.onKeyDown} />

Tente clicar no esboço e use as teclas de seta para cima e para baixo para diminuir o número de segmentos para a curva quadrática e cúbica. Você notará que, para certas curvaturas, um número baixo de segmentos funciona muito bem, mas para curvaturas mais complexas (tente isso para a curva cúbica), é necessário um número maior para capturar as alterações de curvatura corretamente.

<div className="howtocode">

### Como implementar a discretização de curvas

Vamos apenas usar o algoritmo que acabamos de especificar e implementar isso:

```
function flattenCurve(curve, segmentCount):
  step = 1/segmentCount;
  coordinates = [curve.getXValue(0), curve.getYValue(0)]
  for(i=1; i <= segmentCount; i++):
    t = i*step;
    coordinates.push[curve.getXValue(t), curve.getYValue(t)]
  return coordinates;
```

E pronto, esse é o algoritmo implementado. Isso deixa desenhar a "curva" resultante como uma sequência de linhas:

```
function drawFlattenedCurve(curve, segmentCount):
  coordinates = flattenCurve(curve, segmentCount)
  coord = coordinates[0], _coord;
  for(i=1; i < coordinates.length; i++):
    _coord = coordinates[i]
    line(coord, _coord)
    coord = _coord
```

Começamos com a primeira coordenada como ponto de referência e depois desenhamos linhas entre cada ponto e seu próximo ponto.

</div>
