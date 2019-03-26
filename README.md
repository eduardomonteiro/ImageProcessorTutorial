Em linhas gerais, as imagens são as responsáveis pela maior parte dos *bytes* transferidos em uma página Web.  
Com isso se torna importante a otimização das mesmas para que as páginas se tornem mais leves e fluídas. Ainda mais necessário atualmente onde muitos utilizam dispositivos móveis conectados por redes 3G.

Veja um exemplo:

![alt text](http://git.SITE.com.br:8000/tutoriais/imageprocessor/raw/master/Resources/Screenshot_1.png "Imagem 1")

Perceba que, apesar das imagens serem exibidas numa proporção menor (*style="width:200px;"*) as mesmas continuam com o tamanho original.

Isso acontece porque, primeiro o recurso é baixado, e somente após isso é aplicado o redimensionamento do lado do cliente.

O correto nesse caso seria o servidor servir uma imagem já tratada e redimensionada ao cliente.

Existem várias bibliotecas para manipulação de imagens em C#. Mas dessa vez falarei das que permitem manipulação *on-the-fly*. Ou seja, que sua imagem seja manipulada de forma dinâmica através de parâmetros passados pela URL.

Elas manipulam as imagens pelo pipeline do ASP.NET através de HttpModules.

Só pra ilustrar o que de mais básico é possível fazer:

![alt text](http://git.SITE.com.br:8000/tutoriais/imageprocessor/raw/master/Resources/Screenshot_2.png "Imagem 2")

Talvez as duas mais conhecidas para .NET sejam a  **ImageResizer** ([https://imageresizing.net](https://imageresizing.net)) e a  **ImageProcessor** ([http://imageprocessor.org/](http://imageprocessor.org/)).

O **ImageResizer** é bastante conhecido e utilizado em grandes projetos (em alguns projetos da SITE inclusive como [GP Brasil de F1](https://www.gpbrasil.com.br/) por exemplo).

É uma biblioteca bem completa, testada e ainda possui uma gama absurda de plugins para manipulação de imagens. A desvantagem é que algumas funções mais avançadas são pagas. E são **bem caras**.

## ImageProcessor

O **ImageProcessor** ([http://imageprocessor.org/](http://imageprocessor.org/)) é uma opção *free* e *open-source* para manipulação de imagens em .NET. 

Para instalar o pacote:

    Install-Package ImageProcessor.Web

Após isso basta configurar nas saídas das imagens as dimensões desejadas.

Por exemplo:

    http://site.com.br/images/image1.jpg?width=200&height=200

É possível ainda manipular cores, adicionar marcas dagua e muitas outras configurações.

Para outras opções acesse o site do projeto.

Resultado:

![alt text](http://git.SITE.com.br:8000/tutoriais/imageprocessor/raw/master/Resources/Screenshot_3.png "Imagem 3")

## Conclusão

Com a manipulação de imagens *on-the-fly* não precisamos mais nos preocuparmos em redimensionar no momento de *upload*. O cliente pode subir a melhor imagem possível e passamos a manipular as mesmas no momento de servi-las aos dispositivos.

Desse modo poderíamos dispor imagens com tamanhos customizados para celulares, tablets e desktops a partir da original. Caso o *layout* mude, basta alterar o parâmetro da URL para adaptar a imagem ao novo *layout*.

O **ImageProcessor** já vem com um sistema de *disk cache* free embutido. 
Com isso a imagem é redimensionada uma vez e salvo um resultado no disco. As requisições posteriores passam a usufruir desse cache.

![alt text](http://git.SITE.com.br:8000/tutoriais/imageprocessor/raw/master/Resources/Screenshot_4.png "Imagem 4")

Caso você deseje configurar manualmente as opções mais avançadas, instale o pacote:

    Install-Package ImageProcessor.Web.Config
