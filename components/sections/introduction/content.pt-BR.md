# Uma introdução rápida

Vamos começar com as coisas boas: quando estamos falando sobre curvas de Bézier, estamos falando sobre o que você pode ver nos gráficos a seguir. Eles vão de algum ponto inicial a outro ponto final, com sua curvatura influenciada por um ou mais pontos de controle "intermediários". Agora, como todos os gráficos nesta página são interativos, manipule um pouco essas curvas: clique e arraste os pontos e veja como a forma deles muda com base no que você faz.

<div className="figure">
  <Graphic inline={true} title="Curva de Bézier quadrática" setup={ this.drawQuadratic } draw={ this.drawCurve }/>
  <Graphic inline={true} title="Curva de Bézier cúbica" setup={ this.drawCubic } draw={ this.drawCurve }/>
</div>

Essas curvas são muito usadas em aplicativos de design e fabricação auxiliados por computador (CAD/CAM), bem como em programas de design gráfico como Adobe Illustrator e Photoshop, Inkscape, GIMP etc. e em tecnologias gráficas como gráficos vetoriais escaláveis (SVG) e fontes OpenType (TTF/OTF). Muitas coisas usam as curvas de Bézier, por isso, se você quiser aprender mais sobre elas ... prepare-se para aprender!