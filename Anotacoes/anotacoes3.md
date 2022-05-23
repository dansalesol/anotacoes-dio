| Windows   | Unix   |
| --------- | ------ |
| cd        | cd     |
| dir       | ls     |
| mkdir     | mkdir  |
| del/rmdir | rm -rf |

**Instalando o Git**

• **Windows:** Basta acessar o site [git-scm.com](http://www.git-scm.com) e baixar o arquivo de instalação apropriado. O próprio site reconhece se você esta utilizando windows ou linux. Na opção "Windows Explorer integration" é importante atentar para as duas opções que temos que ter sempre as duas opções marcadas "Git Bash Here" e "Git GUI Here", para facilitar para que o agent lan abra o bash do git direto de qualquer pasta que estivermos no explorer. Em seguida daremos "next". Outra parte interessante de se observar é em "Configuring the line ending conversions". Os SOs tem diferentes símbolos que simbolizam quebra de linha. Nessa opção temos que tomar essa decisão. Se caso tivermos um time que utiliza unix e nos utilizamos windows, vale a pena marcar a opção para "unix-style line endings".  
•  **Linux:** Basta no terminal dar o comando "apt-get install git". Temos dois comandos para verificar se esta instalado corretamente: "git --status" e "git --version". 