## Entendendo como o Git funciona "por baixo dos panos"

• SHA1
• Objetos fundamentais
• Sistema distribuído
• Segurança

A sigla SHA significa Secure Hash Algorithm (Algoritmo de Hash Seguro), é um conjunto de funções hash criptográficas projetadas pela NSA (Agência de Segurança Nacional dos EUA).

SHA1 é um algoritmo de encriptação falando a grosso modo, ele vai pegar o seu arquivo (foto, imagem etc) e vai embaralhar ele de uma forma muito específica.

A encriptação gera conjunto de caracteres identificador de 40 dígitos. Esse conjuto é único e serve como identificação. Ex: Você aplica o algoritmo SHA em um arquivo de texto, ele gerará um identificador único. Se você for nesse arquivo de texto e alterar apenas uma vírgula, ele irá gerar outro conjunto de caracteres diferente. E se você voltar no arquivo e tirar a vírgula novamente e rodar o algoritmo, ele irá gerar a chave que tinha gerado antes de colocar a vírgula.

É uma forma curta de representar um arquivo.

```sh
echo "ola mundo" | openssl sha1
> (stdin) = f9fc856e559b950175f2b7cd7dad61facbe58e7b
```

O comando "openssl sha1 texto.txt" gera o código de identificação para o arquivo "texto.txt". Essa é uma forma inteligente do git garantir e identificar que algum arquivo sofreu modificação ou não. Também de garantir que aquele arquivo tem exatamente aquele conteúdo. O git roda o sha1 não somente para arquivos, mas também para objetos internos.

Fazendo um teste:

```sh
openssl sha1 jogos\ mega\ sena\ da\ virada 
SHA1(jogos mega sena da virada) = fd0bba98c4841b061ffd300aa3a9c12c75a213e6
```

Se alterarmos um traço apenas no arquivo o resultado seria:

```sh
openssl sha1 jogos\ mega\ sena\ da\ virada 
SHA1(jogos mega sena da virada)= 7df01ee05894c0343b221a1a3f0da92039e9b30e
```

Se voltarmos o traço como estava:

```sh
openssl sha1 jogos\ mega\ sena\ da\ virada 
SHA1(jogos mega sena da virada)= fd0bba98c4841b061ffd300aa3a9c12c75a213e6
```

Perceba que quando se voltou exatamente o traço no lugar a sequência de 40 caracteres voltou a ser a mesma de antes.