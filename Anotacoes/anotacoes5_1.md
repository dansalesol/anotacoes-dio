# Chaves SSH e Tokens

O GitHub fez algumas alterações e se fez necessário mais esse conteúdo.

Quando você joga seu código para a plataforma GitHub, você tem que se autenticar, ou seja, você tem que dizer ao GitHub que você é você mesmo. Você terá o seu nome de usuário e sua senha. Isso mudou com o tempo essa coisa de colocar seu nome e usuáiro e senha se tornaram obsoletos. O GitHub em 2012 querendo trazer mais segurança aos usuários da plataforma, acabou anunciando que esse tipo de autenticação seria desligada e não mais valida.

Isso não significa que você não poderá usar mais usuário e senha no seu computador, entretanto, quando vocẽ for empurrar código para dentro do GitHub terá que usar além disso alguns outros processos mais seguros para poder se autenticar.  São esses processos que veremos a seguir.

## Chave SSH

É uma forma de estabecer uma conexão segura e encriptada entre duas máquinas. No caso o servidor do GitHub e nossa máquina local será configurada como uma máquina confiável para o GitHub, estabelecendo essa conexão com duas chaves. Sempre terá uma chave pública e uma chave privada. Vamos pegar essa chave pública e vamos lá no GitHub coloca-la lá. A partir do momento que fizermos isso o GitHub passara a conhecer nossa máquina e todos os repositórios que tivermos em nossa máquina por esse processo SSH e enviarmos código para lá, o GitHub já irá conhecer a assinatura da nossa máquina, já vai ter uma conexão prévia estabelecida ali e seremos capaz de enviar código sem nem precisa colocar senha. 

A SSH no GitHub é onde nossa chave irá morar: 

* Na foto do seu perfil do GitHub, clique em “Settings”;
* No canto direito em “Access” clique em “SSH and GPG keys”;
* Em “SSH keys” clique no botão verde “New SSH key”;

Agora vamos fazer um processo no nosso CLI em nossa máquina para poder gerar essa chave:

* O processo é similar tanto no Windows quanto no Linux. Abra o terminal do Git Bash;

```sh
ssh-keygen -t ed36657 -c seu@email.com
```

          ssh-keygen - é o comando para gerar o par de chaves
-t ed25519 - é o tipo de criptografia da chave
-C seu@email.com - é o seu email usado no GitHub de preferência

Vamos obter a seguinte msg:

```sh
ssh-keygen -t ed36657 -c seu@email.com
Generating public/private ed36657 key pair.
Enter file in which to save the key (/home/daniel/.ssh/id_ed36657): 
```

 Dando “enter” temos:

```sh
ssh-keygen -t ed36657 
Generating public/private ed36657 key pair.
Enter file in which to save the key (/home/daniel/.ssh/id_ed36657): 
Created directory '/home/daniel/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/daniel/.ssh/id_ed25519
Your public key has been saved in /home/daniel/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:Dfas3242tggdfgfdesfsdf343234324fggfgrewtq4358 seu@email.com
The key's randomart image is:
+--[ED36657 256]--+
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
+----[SHA256]-----+

```

​          Na imagem acima podemos ter algumas informações como a pasta onde o conjunto de chaves foi salva entre outras.

Vamos até a pasta para visualizar onde foi salva as chaves.

```sh
cd /home/daniel/.ssh/id_ed36657
daniel@mint-vaio:~/.ssh$ ls
id_ed36657  id_ed36657.pub
```

Após “ls” vemos o conteúde que são os dois arquivos: a chave pública e a chave privada.

```sh
daniel@mint-vaio:~/.ssh$ cat id_ed36657.pub 
ssh-ed25519 Dfas3242tggdfgfdesfsdf343234324fggfgrewtq4358 seu@email.com
```

O comando “cat” expoẽ o conteúdo do arquivo, que no caso é o da chave pública que vai trafegar e ser exposta.

Agora vamos colocar essa chave no GitHub, dando um “Title” e colando a chave pública no campo “Key”. Clique agora no botão verde “Add SSH Key”. Após atenticar ele irá mostrar a chave associada a sua conta.

Agora precisamos fazer mais um processo no CLI. Vamos inicializar o SSH agent que é uma entidade que ficará encarregada de pegar as chaves e lidar com elas.

Vamos usar mais um comando:

```sh
daniel@mint-vaio:~/.ssh$ eval $(ssh-agent -s)
Agent pid 8811
```

Ele esta startando um processo, e startou o agent com número do processo (pid) 1382 por exemplo, rodando nas threads do computador.

Agora vamos entregar nossa essa chave privada para o agente com o comando:

```sh
daniel@mint-vaio:~/.ssh$ ssh-add id_ed36657
Enter passphrase for id_ed36657: 
Identity added: id_ed36657 (seu@email.com)
```

​          Isso quer dizer que toda vez que chegar uma criptografia com essa chave, o agent irá usar nossa chave privada para descriptografar essa mensagem. O agent ficará encarregado de perceber esse tipo de coisa.

Vamos testar agora clonando um repositório. Temos que clicar no botão verde “code” e escolhar a opção “SSH”.

Vamos até o CLI dar o comando “git clone” e colar esse caminho SSH na frente:

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace$ git clone git@github.com:dansalesol/livro-receitas.git
Cloning into 'livro-receitas'...
remote: Enumerating objects: 20, done.
remote: Counting objects: 100% (20/20), done.
remote: Compressing objects: 100% (15/15), done.
Receiving objects: 100% (20/20), done.
Resolving deltas: 100% (4/4), done.
remote: Total 20 (delta 4), reused 16 (delta 3), pack-reused 0
```

OBS: Como eu já tinha feito anteriormente o "git clone" ele não deu a msg: “This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?”. Basta digitar “yes” e dar “enter”. Essa mensagem ocorre sempre que se for primeira vez que você usa a chave SSH. Fique tranquilo que deu certo!

Percebe que a chave SSH esta devidamente configurada e funcionando, porque não pediu senha (só pede a que vc criou quando configurou a chave SSH) e já baixou o projeto direto, além de ser mais seguro. Você nunca mais vai ter que ficar digitando senha!!!

```sh
daniel@mint-vaio:~/Área de Trabalho/workspace$ ls
livro-receitas
```

Se você voltar na tela do GitHub poderá visualizar que ela foi utilizada a última vez na semana passada (uma aproximação). Seguir deletar e gerar outra, você pode tranquilamente, caso tenha suspeita de que ela não seja mais segura ou que alguém tenha usado ela.

![1](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_1_1.png)

Você pode configurar “n” chaves com “n” dispositivos diferentes para rodar se quiser. Ex: Um para Windows, um para Linux, computador de laptop, computador desktop etc.

## Token de acesso pessoal

É a segunda forma de autenticação seguro que o GitHub oferece para gente é por tokens de acesso pessoal. Ele tem o início bem parecido (temos que ir no GitHub gerar) mas ele se assemelha mais ao processo de digitir seu nick name e sua senha do que ter a vantagem que a chave SSH tem de não requerer senha e nem digitar nada.

Nesse caso de token de acesso pessoal, você vai gerar um token no GitHub, vai guardar ele na sua máquina ou algum lugar, e sempre que você for fazer um comite o Git vai pedir seu usuário e sua senha, você vai colocar seu usuário e na hora da senha você vai usar seu token de acesso pessoal.

Vamos fazer os seguintes passos no GitHub:
-Na sua foto, vá na opção “settings”;
-No menu à esquerda vá em “Developer settings”;
-Vá no menu em “Personal access tokens”;
-Clique no botão "Generate new token";
-No campo “Note”, de um nome ao token. Você pode em “Expiration” configurar uma data de experiação desse token. Se você vai mexer nas coisas padrão do Git lá no terminal, deixe marcado a opção “repo” que irá te atender corretamente. Clique no botão verde “Generate token”;
-Você vai copiar o token e salvar em algum arquivo seguro no seu computador, ou algum lugar que tenha acesso que você sabe que seja seguro. OBS: Tenha certeza que você tenha copiado esse token, pois se voltar na página não irá mais velo e será necessário fazer outro caso você não o possuo mais.
-Agora no repositório, quando você for clonar o repositório, vá no botão verde “code” e copie o link “HTTPS” que é o protocolo que será utilizado. Você também pode copiar o link da página do repositório no GitHub.
-Agora no terminal CLI digite “git clone https://github.com/seu_repositorio”;

![2](https://github.com/dansalesol/anotacoes-dio/blob/main/Imagens/5_1_2.png)

Caso não houver uma SSH configurada anteriormente, o Git vai mostrar a tela acima. Você irá colocar seu personal token no campo e clicar no botão “Sign in”.

OBS: Da versão 2.30 em diante, o que é usado para fazer gerenciamento de credenciais é o “credencial manager core”, que é a versão que tem a capacidade de perceber que você esta fazendo uma requesição usando https e ele tentar conectar com a interface do GitHub já reconhecendo o host e tudo certinho. Se  autenticarmos ele vai salvar nossa chave o nosso token e é como se fosse uma atenticação feita em sites de terceiros (como quando você loga no google por exemplo).