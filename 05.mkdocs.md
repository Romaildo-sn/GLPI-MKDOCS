<img src="https://dashboard.snapcraft.io/site_media/appmedia/2019/12/61556938-3c337400-aa63-11e9-9ec1-a3ba5643a1a6.png" width=180% >

&nbsp;

O MkDocs é um gerador de site estático **rápido** , **simples** e **absolutamente lindo** , voltado para a construção de documentação de projetos. Os arquivos de origem da documentação são escritos em Markdown e configurados com um único arquivo de configuração YAML. Ele foi projetado para ser fácil de usar e pode ser estendido com temas de terceiros, plugins e extensões Markdown.

## Instalando o MkDocs

Aqui no nosso projeto começaremos inslando além do MkDocs, alguns pacotes extras de temas para o mesmo; utilizaremos o comando `apt isntall mkdocs mkdocs-material mkdocs-bootstrap mkdocs-nature`, e aguardaremos a conclusão da instalação.

![1 comando mkdocs .png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/1%20comando%20mkdocs%20.png?raw=true)![02.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/02.png?raw=true)

Após a conlusão seguiremos criando um novo projeto de site par o MkDocs utilizaremos a instrução (aqui utilizaremos o nome glpi-project): `mkdocs new glpi-project` 

Será criado o diretório com um arquivo `mkdocs.yml` e um subdiretório **docs** com um arquivo `index.md` dentro. Agora podemos efetuar as configurações de acordo com o desejado para o nosso projeto.

![04 - criação do site.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/04%20-%20cria%C3%A7%C3%A3o%20do%20site.png?raw=true)

## Configurando o Site

Acessaremos o diretório do nosso site que aqui chamamos de **glp-project**: `cd glp-project`. Dentro do diretório começaremos editando o arquivo `mkdocs.yml`. Esse arquivo contem a configuração da estrutura do nosso site, nele dfiniremos o menu da nossa ducumentação, temas e outras paramêtros.
Abra o editor através do coamdno `nano mkdocs.yml`. Aqui editamos o nosso layout como na imagem

![04 edição do mkdocs yml.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/04%20edi%C3%A3o%20do%20mkdocs%20yml.png?raw=true)

Após a edição podemos testar nosso site no navegador. Para isso é necessário inicar o serviço do mkdocs com o endereço para acesso, em nosso caso utilizaremos o ip 192.168.0.91:5000. No terminal execute o comando `mkdocs serve -a 192.168.0.91:5000`, e após abriremos nosso site no navegador. 

![06 testando o site via terminal.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/06%20testando%20o%20site%20via%20terminal.png?raw=true)

Abaixo temo o resultado:

![Captura de tela 2024-07-02 020234.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/Captura%20de%20tela%202024-07-02%20020234.png?raw=true)

Agora para podermos fornecer as informações para cada menu, é necessário criarmos os arquivos de extensão .md (extenção padrão do Markdown), os quais serão editados com o conteúdo a ser carregado para o site.

Para nosso exemplo partimos a partir do arquivo index.md, localizado na pasta docs, utilizamos o comando `cp index.md` acompanhando do nome do novo arquivo a ser criado conforme verificado abaixo:

![09 gerando os arquivos .md das sesscos .png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/09%20gerando%20os%20arquivos%20.md%20das%20sesscos%20.png?raw=true)

Após a criação dos mesmo, basta editá-los criando o conteúdo em sintaxe Markdown para ser carregado ao site.
Como como meio a falitar nosso processo produtivo, preferimos utilizar aqui a ferramenta [SatckEdit](https://stackedit.io/app#); que consiste em um editor em sintaxe Markdown com previsualização do resultado da ediação. Após a construção dos textos no [StackEdit](https://stackedit.io/app#) foi realizada a edição final dos arquivos .md no diretório criado no servidor onde os serviços estão configurados.

![11 stackedit home.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/11%20stackedit%20home.png?raw=true)![16 nano home.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/16%20nano%20home.png?raw=true)

O mesmo processo das imagens acima foi repetido para todos os outros arquivos integrantes da documentação.

## Execultando o Build do Site

Após a finalização do preocesso criativo podemo efetuar o comando de build do site, assim criaremos um edereço estático acessível apartir do servidor web, que nosso caso é o Apache.

Para efetuarmos esta tarefa utilizaremos o comando `mkdocs build`, o processo criará uma pasta por nome `site` a qual copiaremos para o diretório `/var/www/html/` utilizando o comando `cp -R site /var/www/html`, assim concluiremos a criação do nosso site de documentação.

![24 cp site.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/24%20cp%20site.png?raw=true)

Ao final conseguiremos acessar nossa página de documentação pleo endreço http://192.168.0.91/site/

![tela final.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Mkdocs/imagens/tela%20final.png?raw=true)

[Getting Started]: ../mkdocks.md
