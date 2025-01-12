---
title: Utilizando fontes customizadas
description: Está procurando como adicionar typefaces customizadas a um website Astro? Utilize Google Fonts com Fontsource ou adicione uma fonte de sua escolha.
i18nReady: true
layout: ~/layouts/MainLayout.astro
setup: |
    import PackageManagerTabs from '~/components/tabs/PackageManagerTabs.astro';
---


Astro suporta todas as estratégias comuns de adicionar typefaces customizadas ao design do seu site. Este guia irá te mostrar duas diferentes opções para incluir fontes web no seu projeto.

## Utilizando um arquivo de fonte local

Se você quer adicionar arquivos de fonte ao seu projeto, nós recomendamos adicioná-las ao seu [diretório `public/`](/pt-br/core-concepts/project-structure/#public). No seu CSS você pode então registrar fontes com uma [declaração `@font-face`](https://developer.mozilla.org/pt-BR/docs/Web/CSS/@font-face) e utilizar a propriedade `font-family` para estilizar seu site.

### Exemplo

Vamos imaginar que você tem o arquivo de fonte `DistantGalaxy.woff`.

1. Adicione seu arquivo de fonte a `public/fonts/`.

2. Adicione uma declaração `@font-face` ao seu CSS. Isso pode ser num arquivo `.css` global que você importa ou em um bloco `<style>` do layout ou componente em que você quer utilizar esta fonte.

    ```css
    /* Registra nossa família de fontes customizada e diz ao navegador aonde encontrá-la. */
    @font-face {
      font-family: 'DistantGalaxy';
      src: url('/fonts/DistantGalaxy.woff') format('woff');
      font-weight: normal;
      font-style: normal;
      font-display: swap;
    }
    ```

    :::note
    Nós não precisamos incluir `public` na URL de origem da fonte pois todos os arquivos em `public` são adicionados ao diretório raiz do seu site.
    :::

3. Utilize a `font-family` da declaração `@font-face` para estilizar elementos em seu componente ou layout. Neste exemplo, o título `<h1>` terá a fonte customizada aplicada, enquanto o parágrafo `<p>` não terá.

    ```astro {10-12}
    ---
    // src/pages/exemplo.astro
    ---

    <h1>Em uma galáxia muito, muito distante...</h1>

    <p>Fontes customizadas fazem meus títulos tão mais legais!</p>

    <style>
    h1 {
      font-family: 'DistantGalaxy', sans-serif;
    }
    </style>
    ```

## Utilizando Fontsource

O projeto [Fontsource](https://fontsource.org/) simplifica utilizar Google Fonts e outras fontes open-source. Ele providencia módulos npm que você pode instalar para as fontes que você quer utilizar.

1. Encontre a fonte que você quer utilizar no [catálogo do Fontsource](https://fontsource.org/fonts). Para este exemplo, nós utilizaremos [Twinkle Star](https://fontsource.org/fonts/twinkle-star).

2. Instale o pacote da sua fonte escolhida.

    <PackageManagerTabs>
      <Fragment slot="npm">
      ```shell
      npm i @fontsource/twinkle-star
      ```
      </Fragment>
      <Fragment slot="pnpm">
      ```shell
      pnpm i @fontsource/twinkle-star
      ```
      </Fragment>
      <Fragment slot="yarn">
      ```shell
      yarn add @fontsource/twinkle-star
      ```
      </Fragment>
    </PackageManagerTabs>

    :::tip
    Você irá encontrar o nome correto do pacote na seção “Quick Installation” (Instalação Rápida, em Português) da página de cada fonte no website do Fontsource. O nome irá iniciar com `@fontsource/` seguido do nome da fonte.
    :::

3. Importe o pacote da fonte no layout ou componente que você quer utilizar a fonte. Geralmente, você vai querer fazer isso em um componente de layout comum para certificar-se de que a fonte está disponível em todo o seu site.

    A importação irá automaticamente adicionar as regras do `@font-face` necessárias para configurar a fonte.

    ```astro
    ---
    // src/layouts/BaseLayout.astro
    import '@fontsource/twinkle-star';
    ---
    ```

4. Utilize `font-family` como mostrado na página da fonte no Fontsource. Isso irá funcionar em qualquer lugar aonde você pode escrever CSS em seu projeto Astro.

    ```css
    h1 {
      font-family: "Twinkle Star", cursive;
    }
    ```

## Mais recursos

### Adicione fontes com Tailwind

Se você estiver utilizando a [integração para Tailwind](/pt-br/guides/integrations-guide/tailwind/), você pode ou adicionar uma declaração `@font-face` para uma fonte local ou utilizar a estratégia de `import` do Fontsource para registrar sua fonte. Após isso, siga [a documentação do Tailwind em como adicionar famílias de fontes customizadas](https://tailwindcss.com/docs/font-family#using-custom-values).

### Aprenda como fontes web funcionam

[O guia da MDN em fontes web](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts) introduz o tópico.

### Gere CSS para sua fonte

[O gerador de fontes web da Font Squirrel](https://www.fontsquirrel.com/tools/webfont-generator) pode ajudar a preparar seus arquivos de fonte para você.
