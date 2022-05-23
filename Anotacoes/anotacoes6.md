# Primeiros comandos com o GIT

• Iniciar o GIT (git init)
• Iniciar o versionamento (git add)
• Criar um commit (git commit)

Quando estamos mexendo com terminal, sempre o nome do programa vai na frente, pois estamos chamando pelo terminal o git, estamos chamando pelo terminal comandos específicos do git, como no exemplo: git (nome do software) init (comando específico do git).

## Criando um repositório

**git init** - Inicializa o repositório na pasta onde o comando foi dado. É criado o arquivo oculto .git que tem informações do versionamento dos arquivos nesta pasta. É a pasta gerencial do git. Atente que existe dentro dessa pasta a pasta "objects".

**ls -a** - Lista arquivos ocultos do tipo “.git” por exemplo.

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Repositório vazio Git inicializado em  /home/daniel/Área de Trabalho/workspace/livro-receitas/.git/
```

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ ls -a
.  ..  .git  README.md  receitas
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ cd .git/
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas/.git$ ls
branches  description  hooks  info  objects      refs
config    HEAD         index  logs  packed-refs
```

Se é a primeira vez que você esta usando o Git, ele requer algumas configurações. São muito poucas na verdade. Ele requer um “name” e um “email”. Isso porque os objetos commit são criados com um autor, é exatamente o que vamos fornecer para que lá na frente quando gerarmos o commit ele tenha um autor atrelado a ele.

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ git config --global user.name Daniel
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ git config --global user.email "seu@email.com"
```

OBS: Podemos setar essa configuração de forma global ou apenas para esse repositório. Aqui no caso setamos de forma global.

## Adicionando um arquivo

Vamos utilizar um tipo de arquivo chamado markdown, que é uma forma mais humana de se escrever um arquivo html sem precisar entender como o html funciona de fato. Os arquivos markdown são ".md". Vamos utilizar o editor de arquivos markdown "typora". Vide [www.typora.io](http://www.typora.io).

Com o Markdown, podemos fazer desde coisas simples até coisas bem charmosas, de forma que o texto fique organizado.

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/6_1.png)

A hashtag "#" formata em níveis de cabeçalho. Para nível 1 basta uma #.  Para o texto ficar em negrito basta iniciar e terminar com "**" como em "**negrito**". Para ficar em itálico basca colocar o texto entre "_" como em "_Itálico_".

Você pode utilizar emoticons também, para tal, basta colocar ":" e escrever o tipo de emoticon. Como em chicken com um ":" no início e outro no fim. Ele autocompleta após você começar a digitar.

Para criar uma lista não ordenada basta dar "-" e espaço. Basta dar "enter" que irá ser completado com novos itens.

Para saber mais formatações markdown basta ir em "ajuda" e "markdown reference". Você irá visualizar todos os tipos de formatações possíveis.

Vamos agora comitar o arquivo, após concluída a receita:

**git add \***  - adiciona todos os arquivos e pastas para serem commitado (na área staged).
**git commit -m "mensagem"** - Lembre-se que os commits são os objetos do git que dão significado as alterações. Esse objetos carregam uma mensagem de texto juntamente como outros metadados como autor, a hora que o commit foi criado etc. Perceba que a mensagem dizendo do sucesso do commit possue uma sequência de números. Essa sequência são os primeiros caracteres do SHA1.

