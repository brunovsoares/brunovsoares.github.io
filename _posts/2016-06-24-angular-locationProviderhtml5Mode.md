---
layout:     post
title:      AngularJS html5mode
date:       2016-06-24
summary:    Angular HTML5 Mode URLs Amigáveis Apache (usando htaccess)
categories: AngularJS
---

## html5mode return 404 ?!?!?
corrigindo o 404 quando usamos o Locationprovider.html5mode no Angular

## O código

Primeira coisa que você tem a fazer é ligar o modo HTML5 no bloco de configuração a sua principal do módulo angular. Isso é muito bonito um um forro:

{% highlight js %}
angular.module('main', []).config(['$locationProvider',
    function($locationProvider) {
        ... $locationProvider.html5Mode(true); ...
    });
{% endhighlight %}
Após fazer isso, você precisa criar um arquivo .htaccess na raiz do seu servidor:

RewriteEngine On
RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} -f [OR] RewriteCond %{DOCUMENT_ROOT}%{REQUEST_URI} -d RewriteRule ^ - [L]

RewriteRule ^ /index.html

## Como funciona?

O html5mode baseia-se na história HTML5 API, que essencialmente permite definir um URL no mesmo domínio com JavaScript. O arquivo .htaccess torna possível recarregar uma página (ou ir para uma página hashbang-less para que o assunto) sem obter uma resposta 404 do servidor. Além disso, se a API Histórico HTML5 não está disponível, o aplicativo Angular usará automaticamente o hashbang como um fallback. Leia mais sobre isso nesta página [Angular docs](https://docs.angularjs.org/guide/$location#html5-mode).
