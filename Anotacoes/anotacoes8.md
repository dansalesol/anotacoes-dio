Vamos apontar o nosso código na nossa máquina, no nosso repositório local para um repositório remoto.

**git config --list** - Traz a lista de todas as configurações que estão no seu git.

**git config --global --unset user.name** - Reseta ou desassocia a configuração de nome.

**git config --global --unset user.nickname** - Reseta ou desassocia a configuração de nickname. 

**git config --global --unset user.email** - Reseta ou desassocia a configuração de email.   

**git config --global user.name** **"SeuNome"** - Configura seu nome.

**git config --global user.nickname "SeuNickName"** - Configura seu nickname.

**git config --global user.email "seu@email.com"** - Configura seu email. Seria interessante que seja o mesmo email usado no GitHub. Isso por que o Git atrela aquele commit específico ao user name e email que você setou na configuração (com esse comando).

Vamos setar o name e o email:

```sh
git config --global user.name "SeuNome"
git config --global user.email "seu@email.com"
```

OBS: Os commits que foram feitos posteriormente com outro email antes de vc alterar com "git config" não há como mudar pois já foram feitos com aquele email.

Como já temos uma conta, basta logar. O GitHub além de ser um repositório remoto onde vamos guardar nosso código e trabalhar em equipe e dar acesso a esse código também, além de possuir outras funcionalidades e uma loja d e aplicações que você pode integrar ao seu fluxo, ele também é uma rede social.

Vamos clicar na sua foto e ir em “Your repositories” e clicar no botão verde “New”.

Vocẽ vai dar um nome ao seu repositório, adicionar uma descrição, deixar public ou private e marcar ou não o checkbox “Intialize this repository with a README”.

OBS: No GitHub você pode setar a opção “Intialize this repository with a README” para criar um README primeiro. Sempre que ele encontra um arquivo Markdown ele irá expó-lo para quem acessar aquela pasta. Os arquivos que contam a funcionalidade ou história daquele repositório são chamados “READMEs”.

Após clicar em “create repository” teremos que apontar nosso repositório local para o GitHub. você vai copiar o endereço do repositório no GitHub na tela.

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_1.png)

Vamos agora abrir o bash e dar o comando para empurar o nosso repositório (que tem todos os commits) local para o repositório remoto. Vamos primeiro adicionar a origem:

![2](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_2.png)

![3](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_3.png)

**git remote add origin "https://github.com/SeuRepositorio/algumacoisa.git"** - Para empurarmos a versão do nosso repositório local para um repositório remoto vamos adicionar a origem remota. O "origin" é apenas um alias ou apilido para que você não tenha que ficar toda hora digitando uma url (basta só se referir a url como "origin" nos comandos daqui para frente, por convensão usamos "origin", entretanto, poderia ser qualquer nome).

**git remote -v** - Mostra a lista de repositórios remotos que você tem cadastrado.

**git status** -  Mostra se há alguma pendência no repositório.

**git push origin master** -  Comando usado para levar o nosso código do repositório local para o nosso repositório remoto, ou seja, "empurar" para o GitHub nosso código. Master é a branch que estamos enviando. Ele irá pedir as credenciais. Podemos ter autenticação de dois passos ou chave SSH, que é mais uma camada de segurança.

![4](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_4.png)

No GitHub, observe que quando vc clica no número (ao lado de yesterday) que é o inicio do sha, você vai para o histórico e mais detalhes sobre esse commit.

![5](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_5.png)

![6](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_6.png)

Observe o número identificador do commit (sha) e ele tem 1 parent (já aponta para o commit parente).

![7](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_7.png)

​          Conforme você for clicando no parent, você vai retornando o código para trás. Podemos navegar entre o histórico.

Voltando para o diretório base do nosso repositório, se você clicar em 3 commits, você pode ver o historico de commits. Você pode ver quando você fez esses commits e a mensagem de cada um. 

![8](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_8.png)

![9](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_9.png)

Você vc clicar no sha do commit você verá o conteúdo contido naquele commit. Ou seja o conteúdo trackeado pelas bordas, o conteúdo no qual está realmente os arquivos que estão sendo alterados.

![10](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/8_10.png)