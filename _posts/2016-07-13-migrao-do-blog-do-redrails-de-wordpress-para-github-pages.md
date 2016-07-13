---
layout: post
title: "Migração do blog do RedRails de Wordpress para Github Pages"
description: ""
category:
tags: []
author:
  email: contato@luizcarvalho.com
  display_name: Luiz Carvalho
  first_name: Luiz
  last_name: Carvalho
---

### TL;DR
**Exportação:**

`https://YOUR-USER-NAME.wordpress.com/wp-admin/export.php`

**Importação:**

{% highlight ruby %}
    $ ruby -rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::WordpressDotCom.run({
      "source" => "wordpress.xml",
      "no_fetch_images" => false,
      "assets_folder" => "assets"
    })'
{% endhighlight %}

## Introdução

Eu vinha tendo muitos problemas com **Wordpress** nos últimos tempos, ataques e mais ataques. Não lembro de todos pois o blog existe a mais de 8 anos, o último ataque, de alguma forma (um plugin talvez), começou a redirecionar todo e qualquer acesso ao site para uma página de [scam](http://canaltech.com.br/o-que-e/hacker/O-que-e-Phishing-Scam/) desabilitei todos os plugins e voltei para o tema padrão do *Wordpress* e não resolveu.

Há algum tempo eu vinha buscando uma alternativa mais flexível para migrar o blog do **RedRails** e como já tinha criado o [luizcarvalho.com](http://luizcarvalho.com) no [Github Pages](https://pages.github.com/) achei que poderia ser uma boa solução, mesmo imaginando que daria muito trabalho fazer toda essa importação, estava completamente enganado.

Ambas plataformas fornecem recursos muito interessantes para a migração (tanto o Wordpress para exportação, quando o **Jekyll** para importação de blogs como o **Wordpress**). Bastou uma pesquisa rápida e já encontramos a [documentação](http://import.jekyllrb.com/docs/wordpressdotcom/) do próprio **Jekyll** mostrando como realizar o procedimento.

## Exportação
Entre em seu `Admin do Wordpress -> Configurações -> Exportar` ou diretamente em `https://YOUR-USER-NAME.wordpress.com/wp-admin/export.php`. A documentação é aplicada a blogs hospedados no *Wordpress.com*, mas pode ser aplicado também aos *Wordpress.org*.

## Importação
Depois de exportar seus posts em formato `XML`, vamos transformar isso em algo que o **Jekyll** possa utilizar. Para isso precisaremos de uma gem chamada `jekyll-import`.

    gem install jekyll-import

Então basta rodar o seguinte comando ou criar um `script` com ele (lembrando de colocar o `require "jekyll-import"` dentro do arquivo)

{% highlight ruby %}
  $ ruby -rubygems -e 'require "jekyll-import";
      JekyllImport::Importers::WordpressDotCom.run({
        "source" => "wordpress.xml",
        "no_fetch_images" => false,
        "assets_folder" => "assets"
      })'
{% endhighlight %}

> **Atenção com o nome do arquivo XML**: Verifique o nome que foi exportado pelo seu **Wordpress** e altere seu script, caso seja necessário.



## Resultado

![Markdown generated]({{ site.baseurl }}/assets/posts/2016-07-13-wordpress-html-to-jekyll-markdown.png)

Bom o processo de conversão dos posts, identifica as imagens dentro de cada post e faz o download do arquivo dentro da pasta `assets_folder` que você definir em seu script e o endereço é alterado para a nova localização. Uma coisa que pode dar um pouco de trabalho pra você é que o texto dos posts continuam em `HTML` para tentar manter o máximo da formatação antiga, mas como muita coisa de seus estilos pode ter ficado do Wordpress é uma boa você dar uma olhada post a post para dar um tapa na formatação dos textos.


Para o layout utilizamos o template do [exflow](http://exflow.io) que também foi feito com **Jekyll** e está hospedado no **Github  Pages**. Ainda estamos nesse processo de corrigir alguns posts que não ficaram bem formatados ou trouxeram muitas formatações desnecessárias.



