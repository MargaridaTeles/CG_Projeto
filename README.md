# **Relatório CG - Interior Mapping Shader**

**Trabalho realizado por:** Margarida Teles, a22204247

## Funcionamento do Shader

 - **CubeMap:**
		 Os CubeMaps podem ser criados de duas maneiras:
	 - **Imagem:**
		 - Através da Imagem, apenas necessitamos de exportar uma imagem para dentro do nosso projeto, alterar "Texture Shape" para Cube e temos o nosso CubeMap feito.
		 ![CubeMap através de Imagem](https://github.com/MargaridaTeles/CG_Projeto/blob/main/Images/inspector_Image.png)
	 - **Montar cenário:**
		 - Para fazer a montagem do cenário necessitamos de assets (eu usei os assets feitos pelo meu grupo em DJD2). Após montar o cenário que neste caso é o interior de uma casa, posicionamos a câmara no meio do cenário para fazer a "quarta parede" e usamos um script para renderizar o CubeMap. O script cria uma secção no "*MenuItem*" que se chama "*Toolbox*" e lá dentro temos uma função que se chama "*RenderCubemapWizard*". Ao selecionarmos essa função é nos pedida a posição da câmara criada anteriormente e podemos clicar no botão em baixo que diz "*Render*". Após clicarmos no botão e formos ao projeto conseguimos ver que fui criada automaticamente uma pasta dentro dos "*Assets*" chamada "*Cubemaps*" que lá dentro contêm o CubeMap criado com o nome da câmara.
	 

 

## Bibliografia
- **[PDF Interior Mapping Shader](https://www.proun-game.com/Oogst3D/CODING/InteriorMapping/InteriorMapping.pdf)**
