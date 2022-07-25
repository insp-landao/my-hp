---
title: "Segundo Post"
date: 2022-07-24T23:49:48-03:00
draft: false
---
# Segundo Post.

Criando sites com Hugo e Netlify

Com o objetivo de incentivar mulheres a criar seu próprio site, obter um novo conhecimento para aplicar em seus trabalhos ou poderem fazer disso uma nova forma de obter renda, no dia 15 de fevereiro de 2020, a comunidade Women Who Go de Curitiba, em parceria com Women Techmakers de Curitiba, ofereceu um workshop para criação de sites estáticos utilizando o framework Hugo.

Hugo é um framework open source desenvolvido em Go, simples de usar e muito rápido para gerar páginas estáticas. Em seu site oficial é possível encontrar centenas de temas prontos para todos os gostos e necessidades.

Hugo Logo, nas cores rosa, azul, verde, amarelo, uma cor para cada letra
O que são sites estáticos?
Quando acessamos um site, é feita uma requisição a um servidor que devolve para o navegador a informação em formato HTML (HyperText Markup Language) que renderiza este texto formatado.

Porém, a grande maioria dos sites são gerados dinamicamente, o que exige processamento do servidor, por vezes um banco de dados e uma linguagem de programação que faz a conversão para HTML.

Os sites estáticos não exigem este processamento pois eles já estão armazenados no servidor no formato HTML, e com isso tem um custo de hospedagem menor (para alguns casos até gratuito) e melhor performance. Além de não ter brechas de segurança.

Estas vantagens fizeram com que grandes blogs e empresas adotassem a ferramenta, como Tableless, 1Password, Let’s Encrypt e outros.

Sites estáticos são muito indicados para blogs, sites pessoais e institucionais.

Bora ver como é fácil?
Vamos utilizar neste tutorial:

Terminal (para quem usa Windows, sugerimos usar o Git Bash);
Git para versionar o projeto;
Github como repositório remoto;
Netlify para publicar o site.
Instalação
O Hugo é disponibilizado como um executável pronto para uso via terminal. É possível utiliza-lo nos principais sistemas operacionais. A instalação consiste em baixar o executável em qualquer local do seu sistema, e fazer uma configuração nas variáveis de ambiente para que o terminal reconheça seu comando.

Para facilitar esta instalação / configuração é possível usar gerenciadores de pacotes como:

Brew no MacOs

$ brew install hugo

Apt-get no Linux (Debian e Ubuntu)

$ sudo apt-get install hugo

Chocolatey no Windows

$ choco install hugo -confirm

O Chocolatey não vem instalado no windows, portanto deve ser instalado antes de usar este comando.
Se preferir pode seguir a instalação manual (sem o chocolatey) que descrevo aqui.


Instalando Hugo via terminal do MacOS
Para outros sistemas operacionais veja na documentação do Hugo.

Ao final da instalação verifique a versão do Hugo, se tudo ocorreu corretamente a versão é apresentada:

$ hugo version

Criando um site
São poucos comados que você precisa conhecer no Hugo. O primeiro é criar um novo site, no terminal navegue até a pasta onde o site deve ser criado (fique a vontade para escolher) então utilize o comando:

$ hugo new site nome-do-meu-site

Será criada uma pasta com o nome do site e dentro dela a estrutura de um site Hugo.


Criando novo site com Hugo via terminal do MacOS
Atenção: TUDO o que for feito a partir daqui deve ser feito dentro da pasta do site. Entre na pasta antes de continuar!!!

$ cd nome-do-meu-site

Definir um tema
Antes de baixar um tema vamos iniciar um novo repositório Git localmente:

$ git init

Atenção: só faça isso dentro da pasta do site!!!

Repositório criado, já podemos escolher um tema para o site em: themes.gohugo.io

Para este tutorial vamos utilizar o tema Noteworthy, para outro procure o repositório github do respectivo tema.


Github do tema Noteworthy
Para publicar o site no Netlify é necessário que o tema seja baixado como um submodulo no repositório. Neste caso o comando fica assim:

$ git submodule add <url> <path>

Onde <url> é o link de clone HTTPS do tema e <path> é o caminho onde o tema será instalado e deve seguir o padrão themes/<nome-do-tema>

Fica assim:

$ git submodule add https://github.com/kimcc/hugo-theme-noteworthy themes/noteworthy


Download do tema feito, agora precisa informar na configuração do site que deve ser utilizado este tema.

Abra o arquivo config.toml em sua IDE ou editor de texto favorito incluindo a linha:

tema = <nome-do-tema>

Os temas geralmente vem com um site de exemplo dentro deles, é preferível que se copie o conteúdo deste exampleSite pois com isso várias outras configurações disponibilizadas pelo tema já serão aplicados ao seu site.

Copie o conteúdo de exempleSite para a raiz do seu site:

$ cp -r themes/noteworthy/exampleSite .

Se não quiser copiar o conteúdo de exemplo, mas só a configuração do tema:

$ cp themes/noteworthy/exampleSite/config.toml .

Já notou que este arquivo config.toml carrega as configurações o seu site?
Então vamos editar e colocar um pouco de personalidade nele!

Pode alterar o title (título principal do site), baseURL (URL final do seu site, não esqueça do http:// ou https://) e outras variáveis próprias do tema.

baseURL = "https://<nome-escolhido>.netlify.com"

Para obter esta URL, deve ser criada conta e um site dentro do Netlify.

Criando conteúdo
Até aqui bem tranquilo, assim como criar um novo conteúdo para o site.

$ hugo new posts/primeiro-post.md

O Hugo cria o um arquivo Markdown dentro da pasta content com o nome que você definiu, e se quiser agrupar em uma pasta pode também.
Se você criar posts/meu-post.md no seu site o caminho será "https://dominio.com/posts/meu-post" então já pense no nome certinho para a URL ficar de acordo com o conteúdo.


Criando conteúdo via terminal do MacOS
Edite o arquivo criado utilizando a sintaxe Markdown, veja aqui.

Note que o arquivo já vem com um cabeçalho, que não vai aparecer no seu texto, porém são variáveis utilizadas na renderização do conteúdo. A principio você só precisa alterar o valor draft: true para draft: false , que informa que este conteúdo não é um rascunho.

Alguns temas podem conter outros valores neste cabeçalho. Sempre leia a documentação dos temas ;)

Publicando o site
Só uma espiadinha

Ok, fizemos muitas coisas e não vimos nada ainda. Podemos pelo menos dar uma espiada em como o site está ficando antes de publicar né?

Para visualizar localmente o site utilizaremos o comando:

$ hugo server -D

Onde, server cria um servidor http para acesso local, e -D (opcional) informa que você quer visualizar os conteúdos que estão ainda como rascunho. Abra o endereço http://localhost:1313 no seu navegador.

Caso queira encerrar o servidor http, use o comando ctrl + c no terminal.

Tudo certo pra publicar?

Preparativo para o Netlify

Quase! Antes de continuar vamos preparar o caminho para o Netlify. Precisamos criar um arquivo netlify.toml na raiz do site com o seguinte conteúdo:

[context.production.environment]
HUGO_VERSION = "x.xx.x"

Aqui você pode colocar a versão do Hugo que está usando para criá-lo. No meu caso foi o 0.65.3

Prontinho para subir para o servidor. Conforme já falamos vamos usar o Github com Netlify.

Criar repositório GitHub

Então vamos criar um repositório no Github (pode ser privado), e "linkar" com o nosso repositório local (lembra que fizemos o $ git init ?) usando o comando:

$ git remote add origin https://github.com/<USER>/<REPO>.git

Onde <USER> é o seu usuário no Github e <REPO> é o nome do repositório que você criou.

Feito isso, segue a receitinha de bolo (que você pode aprender mais aqui):

$ git status mostra todos os arquivos criados e/ou modificados.

$ git add . adiciona TODOS os arquivos na área de staging

$ git commit -m "<título do commit>" realiza o commit

$ git push origin master envia tudo para o Github

Quase lá!

Criar um site no Netlify

Caso não tenha uma conta, pode criar utilizando a autenticação do Github.

Após realizar seu login no Netlify com sucesso, clique em "New site from Git":


Tela inicial da conta no Netlify
Selecione GitHub:


Tela de criação de site do Netlify
Escolha o repositório no qual você trabalhou durante esse tutorial.

Caso não estejam preenchidos os campos "Build command" e "Publish directory", preencha respectivamente hugo e public
E clique "Deploy site", que vai buscar os arquivo no repositório indicado, rodar o comando hugo que gera os arquivos estáticos do site dentro de uma pasta public dentro do servidor da Netlify.

Edite o subdomínio para que fique igual ao que você configurou na baseURL

> Domain settings > Domain management > Options > Edit site name


Tela de gerenciamento de domínios do Netlify
Modifique o nome e salve.

Caso o nome escolhido não esteja disponível, você terá que escolher outro e voltar no config.toml do seu site ajustar a baseURL e fazer novo commit e push .

FEITO, seu site está na internet pra todo mundo ver!!!

Extra: Customização de tema
Caso seja necessário alteração de CSS, JS e ou Imagens do tema, utilize a pasta static reproduzindo a mesma estrutura de pastas do tema.

Exemplo:

Arquivo a ser modificado:
/themes/<THEME>/static/css/style.css

Arquivo recriado com as suas alterações em:
/static/css/style.css

Mas se você quer alterar a estrutura do HTML do tema, utilize a pasta layouts também reproduzindo a estrutura de pastas do tema.

Exemplo:

Arquivo a ser modificado:
/themes/<THEME>/layouts/partials/head.html

Arquivo recriado com as suas alterações em:
/layouts/partials/head.html

Finalizando
Se você utilizou para publicar seu site este tutorial ou passo-a-passo do repositório com o conteúdo da oficina, compartilha nas redes sociais e marca nossa parceira @womenwhogocwb tanto no twitter quanto no instagram com a hashtag #wwgcwb.

Conheça alguém que possa se beneficiar deste conteúdo?
Manda o link deste conteúdo pra ela 😉

E acompanhe as redes sociais 
Women Techmakers Curitiba
 para saber dos próximos eventos e oficinas.

Thanks to Erika Carvalho
