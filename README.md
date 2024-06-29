# IBM Data Engineering

## Projeto final avaliado por pares: Shell Scripting

### Cenário
Imagine que você é um desenvolvedor Linux líder na empresa de tecnologia de ponta ABC International Inc. 
A ABC atualmente sofre de um enorme gargalo: todos os dias, os estagiários devem acessar meticulosamente 
arquivos de senha criptografados em servidores principais e fazer backup de todos os arquivos que foram 
atualizados nas últimas 24 horas. 
Esse processo introduz erro humano, diminui a segurança e exige uma quantidade irracional de trabalho.

Como um dos desenvolvedores Linux mais confiáveis da ABC Inc. 

você foi encarregado de criar um script chamado backup.sh que é executado todos os dias e faz backup automático 
de todos os arquivos de senha criptografados que foram atualizados nas últimas 24 horas.

### Critérios de classificação
Há um total de 20 pontos a serem ganhos para 17 tarefas neste projeto final.

Sua nota será baseada nas seguintes tarefas dentro do laboratório prático:

* `[Tarefas 1-13]`: Carregar captura de tela de seções do script backup.sh exibindo o código correto ( 13 pontos : 1 ponto para cada uma das 13 tarefas)
* `[Tarefa 14]`: Envie seu backup.sharquivo concluído ( 1 pt )
* `[Tarefa 15]`: Carregar captura de tela mostrando permissões executáveis ( 2 pontos )
* `[Tarefa 16]`: Carregar captura de tela mostrando o arquivo chamado backup-[TIMESTAMP].tar.gz( 2 pts )
* `[Tarefa 17]`: Carregar captura de tela mostrando a programação do crontab uma vez por dia ( 2 pontos )

_________________________________________________________________________________________
### Task 1
#### Navegue até a `Task[1]` no código.

Defina duas variáveis com os valores dos dois primeiros argumentos da linha de comando, da seguinte forma:

- Defina `targetDirectory` como o primeiro argumento da linha de comando.
- Defina `destinationDirectory` como o segundo argumento da linha de comando.

(Essa tarefa tem como objetivo melhorar a legibilidade do código.)

``Os argumentos da linha de comando interpretados pelo script podem ser acessados via $1 (primeiro argumento) e $2 (segundo argumento)``

_________________________________________________________________________________________
### Task 2
#### Navegue até a `Task[2]` no código.
Exiba os valores dos dois argumentos da linha de comando no terminal.

Lembre-se de que você pode usar o comando `echo` para imprimir os valores, como no exemplo a seguir:

```bash
echo "O ano é $year"
```

_________________________________________________________________________________________
### Task 3
#### Navegue até a `Task[3]` no código.
Defina uma variável chamada `currentTS` como o timestamp atual, expresso em segundos.

Lembre-se de que você pode personalizar o formato de saída do comando `date`.

Para atribuir o valor de saída de um comando a uma variável, você pode usar substituição de comando: `$()` ou ``.

Por exemplo:
```bash
currentYear=$(date +%Y)
```

_________________________________________________________________________________________
### Task 4
#### Navegue até a `Task[4]` no código.
Defina uma variável chamada `backupFileName` para armazenar o nome do arquivo de backup arquivado e compactado que o script criará.

A variável `backupFileName` deve ter o valor "backup-[$currentTS].tar.gz".

Por exemplo, se `currentTS` tiver o valor 1634571345, então `backupFileName` deve ter o valor `backup-1634571345.tar.gz`.

_________________________________________________________________________________________
### Task 5
#### Navegue até a `Task[5]` no código.
Defina uma variável chamada `origAbsPath` com o caminho absoluto do diretório atual como valor da variável.

Você pode obter o caminho absoluto do diretório atual usando o comando `pwd`.

_________________________________________________________________________________________
### Task 6
#### Navegue até a `Task[6]` no código.
Defina uma variável chamada `destAbsPath` com o valor igual ao caminho absoluto do diretório de destino.

Primeiro, use o comando `cd` para navegar até o diretório de destino (`destinationDirectory`), e depois utilize o mesmo método que você usou na Tarefa 5.

_________________________________________________________________________________________
### Task 7
#### Navegue até a `Task[7]` no código.
Navegue do diretório de trabalho atual para o diretório de destino `targetDirectory`.

Para fazer isso, primeiro utilize o comando `cd` para voltar ao diretório original (`origAbsPath`), e depois navegue para o diretório de destino `targetDirectory`.

_________________________________________________________________________________________
### Task 8
#### Navegue até a `Task[8]` no código.
Encontre arquivos que foram atualizados nas últimas 24 horas.

Isso significa que você precisa encontrar todos os arquivos cuja data de modificação foi há 24 horas ou menos.

Para facilitar, defina uma variável numérica chamada `yesterdayTS` como o timestamp (em segundos) 24 horas antes do timestamp atual, `currentTS`.

Você pode fazer isso usando a seguinte fórmula:
```bash
yesterdayTS=$(($currentTS - 24 * 60 * 60))
```

_________________________________________________________________________________________
### Task 9
#### Navegue até a `Task[9]` no código.
Dentro da expressão `$()` dentro do loop `for`, escreva um comando que retornará todos os arquivos e diretórios na pasta atual.

Clique [aqui](https://www.howtogeek.com/448446/how-to-use-the-ls-command-on-linux/) para obter uma dica sobre uma maneira eficiente de fazer isso usando o comando `ls`.

_________________________________________________________________________________________
### Task 10
#### Navegue até a `Task[10]` no código.
Dentro do loop `for`, você deseja verificar se o arquivo `$file` foi modificado nas últimas 24 horas.

Para obter a data da última modificação do arquivo em segundos, use o comando `date -r $file +%s`.

Em seguida, compare o valor com `yesterdayTS`.

Idea: se `[[ $file_last_modified_date > $yesterdayTS ]]` então o arquivo foi atualizado nas últimas 24 horas!

Como grande parte disso não foi abordado no curso, para esta tarefa você pode copiar o código abaixo e colá-lo entre os parênteses duplos `(())`:

```bash
`date -r $file +%s` > $yesterdayTS
```

_________________________________________________________________________________________
### Task 11
#### Navegue até a `Task[11]` no código.
No comando if-then, adicione o arquivo `$file` que foi atualizado nas últimas 24 horas ao array `toBackup`.

Como grande parte disso não foi abordado no curso, você pode copiar o código abaixo e colocá-lo após o comando `then` para esta tarefa:

```bash
toBackup+=($file)
```

_________________________________________________________________________________________
### Task 12
#### Navegue até a `Task[12]` no código.
Após o loop `for`, compacte e arquive os arquivos, usando o array `$toBackup` com os nomes dos arquivos, em um arquivo com o nome `backupFileName`.

Use o comando abaixo:
```bash
tar -czvf $backupFileName ${toBackup[@]}
```

_________________________________________________________________________________________
### Task 13
#### Navegue até a `Task[13]` no código.
Agora o arquivo `$backupFileName` foi criado no diretório de trabalho atual.

Mova o arquivo `backupFileName` para o diretório de destino localizado em `destAbsPath`.

_________________________________________________________________________________________
### Task 15
#### Navegue até a `Task[14]` no código.
Salve o arquivo em que você está trabalhando (`backup.sh`) e torne-o executável.
Clique aqui para obter uma dica:

Use o comando `chmod` com as opções corretas.

Verifique se o arquivo é executável usando o comando `ls` com a opção `-l`:

```bash
ls -l backup.sh
```

_________________________________________________________________________________________
### Task 16
#### Navegue até a `Task[16]` no código.
1 - Baixe o arquivo zip a seguir usando o comando wget:
```bash
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-LX0117EN-SkillsNetwork/labs/Final%20Project/important-documents.zip
```
2 - Descompacte o arquivo:
```bash
unzip -DDo important-documents.zip
```
(Use -DDo para sobrescrever e não restaurar a data de modificação original)

3 - Atualize a data de modificação do arquivo para o momento atual:
```bash
touch important-documents/*
```
4 - Teste seu script usando o seguinte comando:
```bash
./backup.sh important-documents .
```

_________________________________________________________________________________________
### Task 17
#### Navegue até a `Task[17]` no código.
Copie (não mv) o script `backup.sh` para o diretório `/usr/local/bin/`.

**Nota:** Você pode precisar usar `sudo cp` para criar um arquivo em `/usr/local/bin/`.

1 - Teste o cronjob para ver se o script de backup está sendo acionado, agendando-o para cada 1 minuto.

```bash
*/1 * * * * /usr/local/bin/backup.sh /home/project/important-documents /home/project
```

2 - Utilize o comando abaixo:
```bash
sudo service cron start
```
3 - Uma vez que o serviço cron seja iniciado, verifique no diretório (/home/project) se os arquivos tar estão sendo criados.

Se sim, então pare o serviço cron usando o comando abaixo, caso contrário, ele continuará criando arquivos tar a cada minuto.
```bash
sudo service cron stop
```





