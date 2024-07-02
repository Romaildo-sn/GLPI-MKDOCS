![](https://www.ambientelivre.com.br/media/k2/items/cache/3f4808b525a42a0bb340252b3c0de1d3_XL.jpg)

O [Glpi](https://glpi-project.org/pt-br/) (sigla em francês: _**Gestionnaire Libre de Parc Informatique**_, ou "Gestor de Equipamentos de TI de Código Aberto", em português) é um sistema de código aberto para Gerenciamento de Ativos de TI, rastreamento de problema e central de serviços. É escrito em PHP e distribuído sob a GNU General Public License.

Este guia tem como objetivo fornecer uma visão geral do GLPI para administradores e usuários, contendo o processo de instalação e configuração, bem como demonstração básica do serviço.

# Instalando o GLPI

Abordaremos o processo de instalação apartir da perspectiva da utilização de uma máquina servidora com sistema operacional linux. Os dados detalhados do servidor utilizados podem ser conferidos em [Sobre](about.md).

## Preparando os pré-requisitos

Para instalação do Glpi precisaremos instalar os serviços necessários como, Apache, php, banco de dados etc. Aqui utilizaremos a instação em lote para os serviços contidos no código abaixo:

    sudo apt update && apt install apache2 php libapache2-mod-php php-mysql php-curl php-gd php-intl php-ldap php-apcu php-xml php-zip php-imap php-mbstring mariadb-server mariadb-client
    
![01 Comandos PréRequisitos.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/01%20Comandos%20Pr%C3%A9Requisitos.png?raw=true)
![03 professor 2.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/03%20professo%202.png?raw=true)

Após a instalação dos pacotes necessários partiremos para a configuração do Banco de dados para o Glpi.
Usaremos o comando `mysql_secure_installation` onde podemos configurar alguns parametros para nosso gerenciador de banco de dados (mysql).

![04 configuração do bd mysql_secure_installation.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/04%20configuracao%20do%20bd%20mysql_secure_installation.png?raw=true)

Após podemos criar nosso banco de dados e configurá-lo com usuários e senha, bem como as permissões para o mesmo. Usamos o comando `mysql -u root -p` para acessarmos no cliente do banco de dados (MariaDB), e podemos proceder como abaixo.

![05 criação do banco e usuário.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/05%20criacao%20do%20banco%20e%20usuario.png?raw=true)
![06 configuração de privilégios.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/06%20configuracao%20de%20privilegios.png?raw=true)

## Baixando e instalando o pacote do Glpi

Antes de iniciarmos o download do pacote acessaremos o diretório onde ficaram alocados os arquivos do Glpi, no nosso caso utilizaremos o diretório **_/var/www/html/_**, 

Após acessarmos o diretório procederemos com o download do pacote
````
wget https://github.com/glpi-project/glpi/releases/download/10.0.15/glpi-10.0.15.tgz
````

> Link disponível no repositório ofical no GitHub: https://github.com/glpi-project/glpi/releases

![08 baixando o glpi do github.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/08%20baixando%20o%20glpi%20do%20github.png?raw=true)

Descompacte os arquivos baixados `tar -xzvf tar -xzvf glpi-10.0.15.tgz`

![09 desconpactando.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/09%20desconpactando.png?raw=true)

Modificaremos a configuração do diretório para diretório web e também suas permissões:

    chown www-data:www-data glpi
    chown www-data:www-data glpi/*
    chmod -R 755 glpi
    
![11 mudando as leis na pasta gpli.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/11%20mudando%20permiss%C3%B5es%20na%20pasta%20gpli.png?raw=true)

Assim concluímos a primeira parte da instalão do sistema, passando agora para as configurações via navegador.

## Configução Web (Browser)

Abriremos o nosso navegador e informaresmo o endreço ip da máquina onde o sistema está hospedado no nosso caso **192.168.0.115/glpi**, e então será apresentada a tela abaixo:

![12 Tela inicial do navegador.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/12%20Tela%20inicial%20browser.png?raw=true)

Avançaremos e aceitaremos os termos continuando com a isntalação

![12 termos.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/12%20termos.png?raw=true)

Na tela abaixo, temos um resumo da verificação da compatibilidade do ambiente para a execução do glpi. Nela temos alguns itens obrigatórios que devem está devidamente configurados para que a instação possa prosseguir; caso haja algo pendente será dada a informação, aqui prosseguiremos visto não haver nenhum item impedindo a continuidade do processo:

![14 verificação de ambiente 1.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/14%20%20verifica%C3%A7%C3%A3o%20de%20ambiente%201.png?raw=true)![14 verificação de ambiente 2.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/14%20%20verifica%C3%A7%C3%A3o%20de%20ambiente%202.png?raw=true)

### Conexão com o Banco de dados

A seguir necessitaremos efetuar a conexão com o banco de dados, informando as credenciais de acesso configuradas anteriormente.

![](https://blog.remontti.com.br/wp-content/uploads/2016/09/GLPI_DEBIAN_5.png)

Após a conexão, podemos criar um banco de dados novo, ou utilizarmos um já existente. Aqui utilizaremos o banco glpi, criado anteriormente via terminal.

![15 coenxão bd.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/15%20coenx%C3%A3o%20bd.png?raw=true)![16 conslusão da conexão .png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/16%20conslus%C3%A3o%20da%20conex%C3%A3o%20.png?raw=true)

## Utilizando o GLPI

Ao concluir toda a parte de configuração, podemos então utilizarmos o sistema. Será apresentada uma tela de login, onde informaremos o usuário e senha.

![17 login no sistema.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/17%20login%20no%20sistema.png?raw=true)

> Aqui utilizamos o usuário e senha padrão de Glpi: "glpi" em ambos os campos.

Ao conluirmos nosso acesso, temos o sistema disponível para o inicio das operações

![18 tela inicial glpo.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/18%20tela%20inicial%20glpo.png?raw=true)

### Sessões do Sistema

Ao acessar o sistema nos deparamos com a tela inicial 

![](https://glpi-user-documentation.readthedocs.io/fr/latest/_images/main-ui.png)
	
1.  O menu do usuário permite que você gerencie suas preferências, acesse a ajuda, altere o idioma atual, altere seu perfil e entidade atuais e desconecte-se.
2.  O menu principal permite que você navegue pelos diferentes módulos.
3.  A trilha de navegação permite que você localize o contexto de uso da área de trabalho principal.
4.  A área de trabalho principal é o espaço privilegiado para interação com o aplicativo. 
5.  A caixa de pesquisa permite que você faça uma pesquisa global a qualquer momento.

#### Ativos

O módulo de Ativos é usado para gerenciar todos os ativos que fazem parte da sua infraestrutura de TI. Para gerenciar hardwares e softwares de uma infraestrutura de TI, o GLPI permite listar nativamente todos os ativos que são utilizados dentro da organização gerenciada.

![27 ativos.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/27%20ativos.png?raw=true)

#### Assitência

O módulo de assistência permite que os usuários criem, acompanhem e processem tickets. Planejamentos, estatísticas e tickets recorrentes também estão disponíveis.
Dependendo das permissões do perfil, também é possível criar, acompanhar e processar problemas e alterações.

![28 ASSITENCIA.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/28%20ASSITENCIA.png?raw=true)

#### Gerência

O módulo de Gerêncai permite adentra em uma gestão financeira:  astreie suas despesas, contratos e fornecedores, crie novos objetos de estoque, gerencie banco de dados de usuários e faça relatórios.

![29 GENRENCIA.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/29%20GENRENCIA.png?raw=true)

#### Ferramentas

Através da sessão Ferramentas é possível Gerenciar projetos com GLPI: atribuir tarefas, adicionar colaboradores, definir prazos. Crie relatórios e explore os quadros Kanban para organizar sua equipe! Crie relatórios e explore quadros Kanban para organizar sua equipe! 

Uma das funcionalidade qeu encontramos aqui que se torna bastante poderosa e últil a funcionalidade da criação de um sistema de FAQ (Frequently Asked Questions Em português seria algo como "Perguntas frequentes"), através da opção Base de conhecimento.

![30 FERRAMENTEAS.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/30%20FERRAMENTEAS.png?raw=true)

#### Administração

Aqui você pode gereniciar  o controle dos usuários: defina entidades, crie perfis e restrinja o acesso às informações. Com as regras do GLPI, você pode definir as funções de cada membro do diretório e configurar o fluxo de trabalho para Helpdesk e Inventário. 

![31 ADMINISTRAÇÃO.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/31%20ADMINISTRA%C3%87%C3%83O.png?raw=true)

#### Configurar

Personalize o GLPI: explore os recursos de configuração para adicionar o logotipo de seus farelos, selecione a paleta de cores e configure os plug-ins. Nesta seção, você também pode gerenciar SLAs e notificações. 

![32 CONFIGURAR.png](https://github.com/Romaildo-sn/GLPI-MKDOCS/blob/main/Glpi/imagens/32%20CONFIGURAR.png?raw=true)

[Getting Started]: ../glpi.md
