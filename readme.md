# Como dar deploy de uma aplicação React no Github-pages 

\* criado usando `create-react-app`

# Introdução
Nesse tutorial, vou mostrar como criar uma aplicação React e fazer o deploy dele no GitHub Pages.

Para criar a aplicação React, estarei usando [`create-react-app`](https://create-react-app.dev/), que é uma ferramenta para a criação de um projeto react do zero. Para fazer o deploy, estarei usando [`gh-pages`](https://github.com/tschaub/gh-pages), um pacote npm usado para fazer deploy no [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages), uma hospedagem gratúita do GitHub.

Ao seguir esse tutorial, você terminará com um app React hospedado no GitHub Pages no qual você também poderá customisar.

    Em breve: siga o tutorial no youtube.

# Tutorial

## Pré-requisitos

1. [Node e npm](https://nodejs.org/en/download/) instalados. Essas são as versões que estarei usando neste tutorial:

    ```
    $ node --version
    v16.13.2
    $ npm --version
    8.1.2
    ```
    
2. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) instalado. Essa é a versão que estarei utilizando:

    ```
    $ git --version
    git version 2.29.1.windows.1
    ```

3. Uma conta [GitHub](https://github.com/signup);

## Procedimento

### 1. criar um repositório **vazio** no GitHub

1. Entrar na sua conta GitHub.
2. [Criar um novo repositorio](https://github.com/new).


### 2. Criar um React app

1. Criar um app React :

  
    ```shell
    $ npx create-react-app my-app
    ```

    Esse comando irá criar uma nova pasta chamada: `my-app`, que vai conter o código da aplicação React.

2. Entrar na nova pasta:
  
    ```shell
    $ cd my-app
    ```


### 3. Instale o `gh-pages` pacote npm.

1. Instale o [`gh-pages`](https://github.com/tschaub/gh-pages) :
 
    ```shell
    $ npm install gh-pages --save-dev
    ```


### 4. Adicione uma propriedade `homepage` no `package.json`.

1. Abra o `package.json` no vs-code.
   

2. Adicine uma propriedade `homepage` nesse fomato \*: `https://{username}.github.io/{nome-do-repositorio}`

    
    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://gitname.github.io/react-gh-pages",
      "private": true,
    ```

### 5. Adicione um script de deploy no arquivo `package.json`.

1. Abra  o `package.json` (se não estiver aberto).
   

2. Adicione uma propriedade de `predeploy`e uma propriedade de  `deploy` nos `scripts`:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```


### 6. Adicionar um "remote" que aponte para o repositório Github

1. adicione um "[remote](https://git-scm.com/docs/git-remote)" para o respositório git local.

    Você pode fazer isso usando o comando com o formato abaixo: 
    
    ```shell
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    
    Para customizar o código, substitua `{username}` com o seu username do GitHub e substitua `{repo-name}`  com o nome do repositório GitHub que você criou no passo 1.


    > That command tells Git where I want it to push things whenever I—or the `gh-pages` npm package acting on my behalf—issue the `$ git push` command from within this local Git repository.
At this point, the local repository has a "remote" whose URL points to the GitHub repository you created in Step 1.

### 7. Faça o deploy do app React no GitHub Pages

1. Faça deploy no github pages:

    ```shell
    $ npm run deploy
    ```

    > Isso vai fazer os scripts `predeploy` e  `deploy` definidos no `package.json` rodarem.
    >
    > Por baixo dos panos, o script `predeploy` vai construir uma versão distribuível da aplicação React e guardar-la numa pasta chamada  `build`. Depois, o script `deploy`vai empurrar o conteúdo e arquivos para um novo commit na branch `gh-pages` do repositório GitHub, criando a branch caso não exista.
    > por padrão os commits da branch `gh-pages` terão a mensagem de "Updates". voc~e pode especificar a mensagem por meio do comando `-m`, como está abaixo:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```
    GitHub Pages vai detectar automáticamente os commits publicados pela branch `gh-pages` do repositor. Assim que for detectado, irá acontecer a distribuição do projeto React para qualquer um visitar, seguindo a URL `homepage` que voc~e especificou no passo 4.

**Tudo pronto!** O prejeto React foi publicado no GitHub Pages! 
  
# Referências

1. [ Repositório Original (em inglês) ](https://github.com/gitname/react-gh-pages)
2. [ `create-react-app` guia oficial de Deploy](https://create-react-app.dev/docs/deployment/#github-pages)
