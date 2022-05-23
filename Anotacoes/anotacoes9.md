# Resolvendo conflitos

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/9_1.png)

Quando temos nosso código no GitHub e baixamos ele para nossa máquina ou acabamos de envia-lo para lá, significa que o código que temos no GitHub é exatamente o código que temos na nossa máquina. Suponhamos que uma segunda pessoa vá até o GitHub e baixe o código, fazendo um clone do repositório para a máquina dele, para realizar contribuições. Até esse momento nenhum dos dois mexeram no código, ou seja, os dois código são iguais. Ambos começam então a editar seus código, sendo assim, eles não serão mais iguais. Suponhamos que ambos mexam na mesma linha de código fazendo alterações diferentes para a mesma linha. Suponhamos agora que essa segunda pessoa, empurre o código dela para o GitHub, antes de você, você continuou editando e trabalhando em outros arquivos e ainda não empurrou seu código para o GitHub.

Então temos o seguinte cenário agora, o código que está no GitHub é o mesmo código que esta na máquina da segunda pessoa, e o seu código esta desatualizado. Quando você submeter seu código ao GitHub, ele irá lhe informar que antes de você empurrar seu código para lá, é necessário que você puxe a versão que está no GitHub (que outra pessoa fez a alteração e enviiou) e faça as suas alterações (juntar o que você trabalhou com o que a outra pessoa trabalhou) para poder empurrar, ai sim a versão que estiver na sua máquina será a versão mais recente. 

Esse momento que o GitHub tenta juntar dois código que foram alterados na mesma linha, se chama conflito de marge. Ele não irá fazer alteração alguma, você terá que fazer a alteração manualmente e resolver aquele conflito. Somente depois poderá empurrar o código para o GitHub que irá representar a versão mais atualizada daquele arquivo.

```sh
git status
git add *
git status
git commit -m "Adiciona receita pave"
git push origin master
```

Nesse momento ocorre a seguinte mensagem:

![2](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/9_2.png)

Nesse momento temos que puxar para nossa máquina o que tem no GitHub, através do comando "pull" (puxar), para podermos comparar as versões do código:

```sh
git pull origin master
```

A seguinte mensagem é mostrada, para nos informar que o arquivo foi baixado do GitHub. Ele alterou para que possamos escolher entre as alterações que desejamos:

![3](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/9_3.png)

Abrindo o arquivo, veremos algumas marcações que indicam qual é a nossa parte do código e qual é a parte baixada do GitHub:

```sh
# Livro de receitas :man_cook:

Olá! Bem vindo ao meu livro de receitas :wave:

- Strogonoff de frango
  <<<<<<< HEAD
- Filé a parmegiana

=======

- Abacaxi Frito

>>>>>>> bf8f026b2d12e74f9a2e3f92ab0b9e239bf418c5
```

A partir de  "<<<<<<< HEAD" é a parte do código que é a alteração mais recente que temos, e que estava em nosso repositório local. A partir de "======", é a parte que foi baixada do GitHub. No fim temos um SHA1.

Agora podemos salvar o arquivos com a escolha e alterações. É assim que resolvemos conflitos, abrindo o arquivos, alterando e comitando novamente o arquivos, removendo as marcações “<<<HEAD” e “====” com o SHA1. Por fim empuramos o arquivo para o GitHub:

```sh
git status
git add *      //adicionar a area de staged
git commit -m "resolve conflitos"
git push origin master
```

## Como baixar código do GitHub?

No botão verde "code" que tem a descrição "Clone with HTTPS", copiaremos o link para fazermos a clonagem pelo terminal.

```sh
git clone https://github.com/urlquevocesalvou.git
ls
git remote -v
```

Quando você listar os diretórios, irá visualizar o repositório que você baixou em seu repositório local. Clonando dessa forma, vem como um repositório de verdade, com a pasta ".git" e todo o histórico de modificações. Dando um "git remote -v", iremos visualizar os repositórios remotos aos quais esse repositório local que baixamos esta apontado.