# Ciclo de vida dos arquivos

**GIT INIT** - Além de criar a pasta .git ele inicializa o repositório. Quando usamos esse comando, de fato estamos criando um repositório no git dentro da pasta.

## Tracked ou Untracked

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_1.png)

**Tracked** são os arquivos que o git tem ciência deles.

**Untracked** são os arquivos que o git ainda não tem ciência sobre, não sabe que eles existem. 
 
**Unmodified** são os arquivvos que ainda não foram modificados. 
 
**Modified** são os arquivos Unmodified que sofreram modificação. 
 
**Staged** é um conceito chave para se entender, imagine um palco que vai ocorrer uma peça e a parte de trás do palco é o backstage onde tem pessoas trabalhando, cuidando de maquiagem, figurino etc. Temos também as pessoas que estão preparadas para entrar no palco, seja para atuar, cantar etc. O Staged é onde ficam os arquivos que estão se preparando para fazer parte de outro tipo de agrupamento (veremos adiante).

No exemplo prático criando um repositório, o comando "git add" o seguinte processo foi feito. Tinhamos um arquivo (strogonoff.md) que estava *Untracked* (git não sabia da existência dele)  que havia acabado de ser criado. Rodamos o segundo comando "git add", que moveu o arquivo *Untracked* diretamente para o *Staged* (área a qual ele esta aguardando para entrar no palco). 

![2](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_2.png)

Os arquivos no *Unmodified*, temos um arquivo dentro do repositório do git que ainda não sofreu alteração. Abrindo o arquivo e modificando-o, ele muda de *Unmodified* para *Modified*. O git faz isso comparando o SHA1 dos arquivos e descobrirá que o arquivo tem modificação.

![3](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_3.png)

Se rodarmos o "git add" novamente ele irá para *Staged*, a área especial que esta aguardando entrar em ação, para executar uma outra ação ou fazer parte de outro grupo.

![4](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_4.png)

Se tivermos um arquivo *Unmodified* (não sofreu alteração alguma) e removemos esse arquivo, ele vai para *Untracked* novamente.

![5](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_5.png)

Em *Unmodified* e *Modified*. Quando movemos este arquivo para *Staged* (um estado de arquivos que é importante), ele esta se preparando para fazer parte de um commit. Quando a gente coloca atrás do palco esses arquivos para entrar em ação e a gente da um commit neles, ou seja, a gente envelopa todas esses modificações com significância, escreve uma mensagem para nosso commit que carrega um autor e uma data e interega de fato o objeto commit, eles deixam de ser *Staged* e vão para commit, pois passam para o estado diferente. O commit retorna todos esses arquivos para *Modified* para começar o ciclo novamente. Por que ele retorna para *Modified*? Ele pega todos aqueles arquivos e diz "acabei a alteração desses arquivos e vou salvar eles, vou criar um *snapshot* (uma foto)". O *snapshot* do código naquele momento esta salvo dentro do commit, dentro desse objeto especial. Todos os arquivos voltam para *Unmodified* para aguardar novas modificações. Se for aberto e editado volta para *Modified* novamente, e rodando "git add", ele vai para *Staged* novamente. Assim por diante. O ciclo fica rolando entre esses três estágios: *Unmodified*, *Modified* e *Staged*.

![6](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_6.png)

Quando você roda o "git init" ele inicia um repositório. Vamos entender o que os repositórios significam:

![7](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_7.png)

Os arquivos vão ficar alternando entre o "REPOSITÓRIO DE TRABALHO" e o "STAGING AREA" a medida que você vai adicionando e modificando novos arquivos. Quando você faz um commit, ele passa a integrar o seu "REPOSITÓRIO LOCAL". O seu "REPOSITÓRIO LOCAL", por sua vez, pode ser emputado para um "REPOSITÓRIO REMOTO".

![8](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_8.png)

Quando você  adiciona um arquivo qe era *Untracked* e você da um "git add", ele é movido para *Staged*. Quando você tem um arquivo modificado e dá um "git add", ele também é movido para a área de *Staged*. Justamente o que fora dito anteriormente: Os arquivos vão ficar transitando entre a área de "WORKING DIRECTORY" e "STAGING AREA".

![9](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_9.png)

O arquivo também se move da "STAGING AREA" (área de trás do palco, que ele esta se preparando para entrar no palco) e faz com que esses arquivos entrem em cena quando você dá commit neles. Quando você da commit, você faz duas coisas:

* Move os arquivos que estavam na área "STAGING AREA" e colocá-os em *Unmodified*, ou seja, você criou um snapshot do estado dos seus arquivos.
*  Você popula o seu repositório local "LOCAL REPOSITORY". Ao qual será composto por commits (tudo comitado), caso contrário, você não consegue enviar esses arquivos para um repositório remoto "REMOTE REPOSITORY". 

**git status** - Nos ajuda a monitorar os status dos arquivos. Nos diz se o arquivo esta *Untracked*, *Modified* ou *Staged* por exemplo. Usaremos esse comando com muita frequência.

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace/livro-receitas$ git status
No ramo master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

**mkdir receitas** - Criou a pasta receitas.

**mv strogonoff.md ./receitas/** -  Move o arquivo "strogonoff.md" para a partir do diretório que estamos, no subdiretório "receitas".

A partir desse momento ela irá mostrar com "git status" que houve uma alteração e trouxe muito mais informações:

![10](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_10.png)

Ele diz que deletamos “strogonoff.md” e que essas mudanças então “atrás do palco” (not staged), ou seja, não fazem parte do commit ainda.

Ele diz que deletou, pq o Git não conhece a pasta que foi criada (untracked). Ele sujere que vc de um “git add” para mover esse arquivo para a área “staged”. Se comitarmos “git commit” vamos criar um snapshot do nosso repositório (e das alterações que fizemos). Vamos fazer exatamente isso:

**git add strogonoff.md receitas/**

**git status**

![11](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_11.png)

**git commit -m “cria pasta receitas, move arquivo para receitas”**

![12](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_12.png)

**git status**

![13](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_13.png)

**echo > README.md** - Cria um arquivo com o nome README.md.

**git status**

![14](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_14.png)

Vemos que temos arquivos do tipo "untracked" (não rastreados). Acabamos de adicionar o arquivo em nosso repositório e ele é diferente da última versão do nosso commit (snapshot), então ele não esta sendo "trackeado" ou “versionado”.

**git add \*** - Pega tudo que esta no diretório de trabalho e adiciona para *Staged* para poder comitar.

![15](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_15.png)

**git commit -m “adiciona index”**

![16](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_16.png)

Vimos:

![17](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_17.png)

![18](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_18.png)

![19](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_19.png)

No próximo tópico veremos:

![20](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/7_20.png)