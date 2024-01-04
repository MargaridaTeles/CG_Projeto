# **Relatório CG - Interior Mapping Shader**

**Trabalho realizado por:** Margarida Teles, a22204247

## O que é?

O Interior Mapping Shader é basicamente um efeito de parallax com um shader que projeta textura numa superfície, em seguida mapeia essa textura de uma maneira que distorce a imagem em relação à visão da câmera. É uma ótima técnica para simular profundidade atrás de uma janela.

## Funcionamento do Shader

 **Distorção da Câmera**
 A distorção é um aspeto fundamental que ajuda a criar a ilusão de profundidade e tridimensionalidade quando projetamos texturas 2D em superfícies planas. A distorção é essencial para garantir que a projeção se pareça correta e realista, especialmente quando é vista de diferentes ângulos.
 
 **Direção da Visualização** - A distorção começa por receber a direção da visualização, ou seja, a direção para que nos encontramos a olhar e a posição da câmera em relação ao objeto com o shader.
 **Mapeamento de Coordenadas** - O shader utiliza técnicas de mapeamento de coordenadas para associar cada ponto na superfície do objeto a uma posição correspondente na textura. Estas coordenadas são ajustadas de acordo com a posição e a direção da câmera.
 **Transformação da Projeção** - Com base nas informações da câmera, o shader aplica transformações às coordenadas da textura. Estas transformações tratam-se de rotações, escalas e translações que ajudam alinhar a textura com a vista, dando assim a ilusão de profundidade.

 **Shader Graph**
 Os nodes usados na criação do shader foram:
 - **Sub Graph** - Criado para distorcer a câmera, através da direção de visualização, mapeamento de coordenadas e transformação da projeção, anteriormente referidas.
 - **Tilling** - Controla o padrão de repetição do mapeamento da textura.
 - **Depth** - A profundidade da textura.
 - **CubeMap** - Textura mapeada em um cubo.
 - **Lerp** - Combina dois valores baseados em interpolação.
 - **Checkerboard** - Gere um padrão.
	- **Frequency** - Define a quantidade de repetições do padrão em ambas as direções.

 **Sub Graph "interiorCubeMap"**
 Os nodes usados foram: 
- **Tilling** - SubGraph usada como função relacionada à repetição de Texturas. Define um deslocamento bidimensional.
- **Math » Basic » Subtract** - Subtrai dois valores ou texturas
- **UV » Tilling and Offset** - Combina o conceito de **Tilling** com um deslocamento. Permitindo que se repita um padrão e se desloque ao mesmo tempo.
- **Input » Geometry » UV** - Refere as coordenadas da textura.
- **Math » Range » Fraction** - Retorna a parte fracionária de um número.
- **Math » Basic » Multiply** - Mutiplicação entre dois valores ou textura.
- **Channel » Split** - Divide o valor recebido pelos componentes (R, G, B).
- **Input » Basic » Vector3** - Determina as coordenadas (x, y, z).
- **Utility » Preview** - Usado para visualizar valores em tempo real.
- **Math » Basic » Divide** - Divide os valores recebidos.
- **Math » Advanced » Absolute** - Garante que componentes são positivas.
- **Input » Geometry » View Direction** - Este node serve para fornecer a direção de visualização da câmera no espaço 3D. A  **View Direction** é essencial para calcular como a textura será distorcida ao ser projetada na superfície do objeto.
- **Properties » Depht** -  Representa a profundidade da textura.
- **Texture » Sample Reflected Cubemap** - Mostra a textura cubemap, guarda informações de cor do ambiente em todas as direções (cima, baixo, frente, trás, esquerda e direita).
- **Output** - Envia a saída processada para a renderização.

## Como usar?

 - **CubeMap:**
		 Os CubeMaps podem ser criados de duas maneiras:
	 - **Imagem:**
		 - Através da Imagem, apenas necessitamos de importar uma imagem para dentro do nosso projeto, alterar "Texture Shape" para Cube e temos o nosso CubeMap feito.
		 ![CubeMap através de Imagem](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/inspector_Image.png)

	 - **Montar cenário:**
		 - Para fazer a montagem do cenário necessitamos de assets (eu usei os assets feitos pelo meu grupo em DJD2). Após montar o cenário que neste caso é o interior de uma casa, posicionamos a câmara no meio do cenário para fazer a "quarta parede" e usamos um script para renderizar o CubeMap.
  
     		![CubeMap montagem de cenário](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Montagem_cenario.png)
   
     		O script cria uma secção no "*MenuItem*" que se chama "*Toolbox*" e lá dentro temos uma função que se chama "*Cubemap Wizard*".

		 	![CubeMap Toolbox](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Toolbox.png)

     		Ao selecionarmos essa função é nos pedida a posição da câmara criada anteriormente e podemos clicar no botão em baixo que diz "*Render*".

		 	![CubeMap Render](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Render.png)

     		Após clicarmos no botão e formos ao projeto conseguimos ver que fui criada automaticamente uma pasta dentro dos "*Assets*" chamada "*Cubemaps*" que lá dentro contêm o CubeMap criado com o nome da câmara.
			
		 	![CubeMap Repositorio Cubemaps](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/repositorio.png)

## Resultados Finais

1º Teste
<p align="center">
  <img width="460" height="300" src="https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Gif_Test.gif">
</p>

Cenário Montado
<p align="center">
  <img width="460" height="300" src="https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Gif_BuildRoom.gif">
</p>

Interior Shader Map
<p align="center">
  <img width="460" height="300" src="https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Gif_InteriorShaderMap.gif">
</p>

Utilização no projeto de DJD2
<p align="center">
  <img width="460" height="300" src="https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Gif_ProjectDJD2.gif">
</p>

## Curiosidade

O Interior Mapping Shader é bastante usado em alguns jogos, como por exemplo em Spider-Man.
Para eles corrigirem a alteração das paredes nos cantos, eles decidiram não usar o shader, nas janelas que são juntas e para dar a sensação de que as salas são diferentes optaram por colocar "cortinas" à frente das janelas.
<p align="center">
  <img width="460" height="300" src="https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/Gif_SpiderMan.gif">
</p>

## Conclusões Finais

Durante esta disciplina e este projeto, ganhei algum conhecimento à cerca de shaders. Não tinha noção que eram usados shaders para tanta coisa e como usá-los pode facilitar a nossa vida em termos de desenvolvimento, antes acreditava que muitas coisas nos jogos eram reais e agora consigo perceber que muita coisa não passa de simulação, desenvolvida através da matemática.
Ao perceber que muitas coisas nos jogos são simulação, fiquei mais fascinada e interessada para perceber como funcionam e consegui reproduzir os meus próprios para usar nos meus projetos.

## Bibliografia
- **[PDF Interior Mapping Shader](https://www.proun-game.com/Oogst3D/CODING/InteriorMapping/InteriorMapping.pdf)**
