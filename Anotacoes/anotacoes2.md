## Navegação básica no terminal & instalação

**GUI X CLI**

A maioria dos software tem uma interface gráfica ou GUI(graphic user interface) para sua utilização. A forma que vamos interagir com o Git e consequentemente a forma como o seu design foi feito, será por meio de uma CLI(command line interface). Hoje em dia temos softwares que pegam o Git e acrescentam a ele uma GUI.

O que vamos aprender?
• Mudar de pastas
• Listar as pastas
• Criar pastas/arquivos
• Deletar pastas/arquivos

| Windows   | Unix   |
| --------- | ------ |
| cd        | cd     |
| dir       | ls     |
| mkdir     | mkdir  |
| del/rmdir | rm -rf |

O terminal do windows é derivado do shell e o terminal do linux é derivado do bash. O conceito de "silence on success" significa que se o comando der certo, nada será mostrado.

• **dir / ls** -  Traś a lista de diretórios e arquivos contidos em uma pasta.
• **cd** - É o comando "change directory". Ele possibilita que navegamos entre as pastas. É o mesmo comando para ambos os SOs. No linux "cd /" vai para o diretório raiz do usuário.
• **cd ..** - Em ambos os SOs esse comando retrocede de diretório, ou seja, sai da pasta e vai para o diretório acima.
• cd / - Vai para o diretório raiz a partir de qualquer lugar que você estiver.
• **cls / clear** - Limpa o terminal. A título de curiosidade, cls significa "clear screen". No linux o comando "ctrl + L" também limpa a tela.
• **Tecla tab** - Autocompleta um nome de arquivo, evitando erros.
• **mkdir** - Cria uma pasta. Para ambos os SOs.
• **echo** -  O comando "echo hello" simplismente mostra na tela "hello", entretanto "echo hello > hello.txt" redireciona o fluxo, ou seja, pega o output e joga em um arquivo. Funciona em ambos os SOs. Também funciona: echo “isso é um teste” > hello.txt.
• **del** - Deleta tudo que esta dentro da pasta. Ex: "del workspace" irá deletar tudo que esta dentro da pasta workspace, mas deixará a pasta workspace existir. Esse comando no windows se restringe a deletar apenas arquivos.
• **rmdir / rm -rf** - Esse comando remove a pasta com tudo que tem dentro. Para windows podemos utilizar "rmdir workspace /S /Q", onde utilizamos duas flags. No linux utilizaremos "rm -rf workspace"(r de *recursive* para deletar todas as pastas contidas la dentro e f é de *force* para não parecer nenhum tipo de pergunta).
• **seta para cima** - Navega pelos comando que você deu ateriormente. 

OBS: Todos esses comandos possuem varianças, ou seja, eles possuem “flags” que são complementos que passamos para esses comandos e que acrescentam, modificam ou formatam a forma como esses comandos são devolvidos para nós.