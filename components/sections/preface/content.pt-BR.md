# Prefácio

Para desenhar coisas em 2D, geralmente contamos com linhas, que geralmente são classificadas em duas categorias: linhas retas e curvas. A primeira delas é tão fácil de ser desenhada à mão quanto por um computador. Dê ao computador o primeiro e o último ponto da linha e BAM! linha reta. Sem perguntas.

As curvas, no entanto, são um problema muito maior. Embora possamos desenhar curvas com certa facilidade à mão livre, os computadores são um pouco prejudicados por não conseguirem desenhar curvas, a menos que exista uma função matemática que descreva como ela deve ser desenhada. Na verdade, eles ainda precisam disso para linhas retas, mas a função é ridiculamente fácil, então tendemos a ignorar isso; todas as linhas são "funções", independentemente de serem retas ou curvas. No entanto, isso significa que precisamos criar funções rápidas de computação que levem a curvas de aparência agradável em um computador. Existem várias, e neste artigo, focaremos em uma função específica que recebeu bastante atenção e é usada em praticamente qualquer coisa que possa desenhar curvas: as curvas de Bézier.

Elas têm o nome de [Pierre Bézier](https://en.wikipedia.org/wiki/Pierre_B%C3%A9zier), que é o principal responsável por torná-las conhecidas no mundo como curvas adequadas para trabalhos de design (publicando suas investigações em 1962 enquanto trabalhava para a Renault), embora ele não tenha sido o primeiro, ou único, a "inventar" esse tipo de curva. Pode-se ficar tentado a dizer que o matemático [Paul de Casteljau](https://en.wikipedia.org/wiki/Paul_de_Casteljau) foi o primeiro, quando começou a investigar a natureza dessas curvas em 1959 enquanto trabalhava na Citroën e veio com uma maneira realmente elegante de saber como desenhá-las. No entanto, de Casteljau não publicou seu trabalho, tornando difícil responder a pergunta de "quem foi o primeiro?". Ou será que é? As curvas de Bézier são, em sua essência, "polinômios de Bernstein", uma família de funções matemáticas investigadas por [Sergei Natanovich Bernstein](https://en.wikipedia.org/wiki/Sergei_Natanovich_Bernstein), cujas publicações datam de ao menos 1912.

De qualquer forma, isso são só curiosidades, é mais provável que você se importe em como essas curvas são convenientes: você pode vincular várias curvas de Bézier para que a combinação pareça uma única curva. Se você já desenhou "caminhos" com o Photoshop ou trabalhou com programas de desenho vetorial como Flash, Illustrator ou Inkscape, essas curvas que você desenhou são curvas de Bézier.

Mas e se você precisar programá-los você mesmo? Quais são as armadilhas? Como você os desenha? Quais são as caixas delimitadoras, como você determina interseções, como você pode extrudar uma curva, em resumo: como você faz tudo o que deseja quando usa essas curvas? É para isso que serve este artigo. Prepare-se para ser matemátizado!

<div className = "print">
## PS: compre um café para mim?

Se você gostou deste livro o suficiente para imprimi-lo, pode estar se perguntando se há alguma maneira de retribuir. Para responder a essa pergunta: você sempre pode me comprar um café, não importa onde você mora, ou se você quiser pagar um preço justo por este livro, pode me comprar um café realmente caro =)

Ao longo dos anos, este livro cresceu de uma pequena cartilha para um e-book equivalente a mais de 100 páginas impressas sobre o tema das curvas de Bézier, e muito café foi produzido. Não me arrependo de um minuto que passei escrevendo, mas sempre posso fazer mais café para continuar escrevendo! Visite https://pomax.github.io/bezierinfo e clique no link no prefácio on-line para doar um dinheiro para o café.
</div>

—Pomax (ou no mundo do tweet, [@TheRealPomax] (https://twitter.com/TheRealPomax))

<div className = "note">

## Nota: praticamente todos os gráficos de Bézier são interativos.

Esta página usa exemplos interativos, contando com o [Bezier.js](http://pomax.github.io/bezierjs), bem como fórmulas matemáticas que são digitadas no SVG usando o sistema de escrita [XeLaTeX][XeLaTeX](https://ctan.org/pkg/xetex) e [pdf2svg](https://github.com/dawbarton/pdf2svg) por [David Barton](http://www.cityinthesky.co.uk/). A página é gerada offline como um aplicativo React.

## Este livro é de código aberto.

Este livro é um projeto de software de código aberto e vive em dois repositórios do github. O primeiro é o [https://github.com/pomax/bezierinfo](https://github.com/pomax/bezierinfo) e é a versão puramente para apresentação que você está visualizando agora. O outro repositório é [https://github.com/pomax/BezierInfo-2](https://github.com/pomax/BezierInfo-2), que é a versão de desenvolvimento, contendo todo o HTML, JavaScript e CSS. Você pode bifurcar qualquer um desses e fazer com eles o que quiser, exceto passar por seu próprio trabalho por atacado, é claro =)

## Quão complicada será a matemática?

A maioria das matemáticas nesta cartilha é de matemática do ensino médio. Se você entende aritmética básica e sabe ler português, deve se dar bem. Às vezes haverá matemática *muito* mais complicada, mas se você não quiser digeri-las, poderá ignorá-las com tranquilidade, ignorando as "caixas de detalhes" na seção ou pulando para o final de uma seção com matemática que parece muito envolvente. O final das seções geralmente lista as conclusões para que você possa trabalhar diretamente com esses valores.

## Perguntas, comentários:

Se você tiver sugestões para novas seções, acesse o [Github issue tracker](https://github.com/pomax/BezierInfo-2/issues) (também acessível a partir do repositório vinculado no canto superior direito). Se você tiver dúvidas sobre o material, não há nenhuma seção de comentários enquanto estou reescrevendo, mas você pode usar o rastreador de problemas também. Depois que a reescrita estiver concluída, adicionarei uma seção de comentários gerais novamente, e talvez um sistema mais prático "selecione esta seção do texto e pressione o botão 'pergunta' para fazer uma pergunta sobre isso". Veremos.

## Ajude a apoiar o livro!

Se você gostou deste livro, ou simplesmente o achou útil para algo que estava tentando realizar, e estava se perguntando como me informar que gostou deste livro, você tem duas opções: pode ir até o [Patreon](https://patreon.com/bezierinfo) deste livro, ou se você preferir fazer uma doação única, vá até o [compre um café do Pomax](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=QPRDLNGDANJSW). Este trabalho passou de uma pequena cartilha para um leitor equivalente a mais de 100 páginas impressas sobre o assunto das curvas de Bézier ao longo dos anos, e muito café foi produzido. Não me arrependo de um minuto que passei escrevendo, mas sempre posso fazer mais café para continuar escrevendo!

</div>