# Estudando Docker 🐳
Este repositório foi criado com o objetivo de fornecer um guia prático e direto ao ponto sobre os comandos mais utilizados no terminal para trabalhar com o Docker. Seja você iniciante ou já com alguma experiência, este material ajudará a entender e aplicar os principais conceitos de forma eficiente. <br> 

O Docker é uma plataforma poderosa para criação, gerenciamento e execução de contêineres, permitindo o desenvolvimento e a implantação de aplicações de maneira rápida, segura e escalável. <br> 

Neste guia, você encontrará: <br>

- Comandos básicos para iniciar com o Docker.
- Gerenciamento de contêineres, imagens e volumes.
- Exemplos práticos e explicações claras para facilitar o aprendizado.

## Listar Contêineres
O comando `docker container ls` é usado para listar todos os contêineres em execução no momento. Ele fornece detalhes como o ID do contêiner, a imagem utilizada, status, portas expostas e o nome atribuído ao contêiner.
```bash
docker container ls
```

Se você quiser listar todos os contêineres (incluindo os que não estão em execução), use a opção `-a`:
```bash
docker container ls -a
```

## Criar um Contêiner

O comando `docker container create` é usado para criar um contêiner baseado em uma imagem especificada, mas sem iniciá-lo automaticamente.  

No exemplo abaixo:  
- `--name teste`: Define o nome do contêiner como "teste".  
- `-it`: Configura o contêiner para rodar de forma interativa com um terminal anexado.  
- `alpine`: Especifica a imagem Alpine Linux para o contêiner.  
- `sh`: Define o shell `sh` como o comando padrão a ser executado.  

```bash
docker container create --name nome-do-container -it alpine sh
```

## Conectar-se a um Contêiner em Execução

O comando `docker container attach` é usado para conectar seu terminal ao **STDIN**, **STDOUT** e **STDERR** de um contêiner em execução. Isso permite que você interaja com o processo principal do contêiner.

No exemplo abaixo:  
- `teste`: Refere-se ao nome do contêiner que foi criado anteriormente.

```bash
docker container attach nome-ou-id-do-conteiner
```

Esse comando é útil para visualizar logs ou interagir diretamente com o processo principal do contêiner.

## Parar a Execução de um Contêiner

O comando `docker container stop` é usado para parar a execução de um contêiner. Ele envia um sinal **SIGTERM** ao processo principal do contêiner, dando a ele a oportunidade de finalizar de forma controlada. Caso o processo não termine no tempo padrão (10 segundos), o Docker força o encerramento com um sinal **SIGKILL**.

```bash
docker container stop nome-ou-id-do-conteiner
```

Para forçar o encerramento imediatamente, você pode usar o comando:

```bash
docker container kill nome-ou-id-do-conteiner
```

## Iniciar um Contêiner Parado

O comando abaixo é usado para iniciar um contêiner que foi previamente criado ou parado. Você pode utilizar o nome ou o ID do contêiner para identificá-lo.

```bash
docker container start nome-ou-id-do-conteiner
```

- `start` Inicia um contêiner que está parado.
- `nome-ou-id-do-conteiner` Substitua pelo nome ou ID do contêiner que deseja iniciar.

Esse comando é útil quando você precisa reiniciar rapidamente um contêiner sem criar um novo.

## Remover um Contêiner

O comando `docker container rm` é usado para remover um contêiner que já foi parado. É útil para manter o ambiente limpo, excluindo contêineres que não são mais necessários.

```bash
docker container rm nome-ou-id-do-conteiner
```

**OBS:** Para poder remover o container é necessário primeiro para-lo.

## Renomear um Contêiner

O comando `docker container rename` é usado para alterar o nome de um contêiner existente. Isso pode ser útil quando você deseja dar um nome mais descritivo ou organizado ao seu contêiner.

```bash
docker container rename id-do-container novo-nome-para-o-container
```

## Executar Comandos em um Contêiner em Execução

O comando `docker container exec` permite executar comandos diretamente dentro de um contêiner que já está em execução. Ele é útil para inspecionar o estado do contêiner, realizar manutenção ou executar tarefas específicas. 

No exemplo abaixo, usamos o comando `top` dentro do contêiner chamado `teste` para listar os processos em execução:

```bash
docker container exec teste top
```

O comando `docker container cp` é utilizado para copiar arquivos ou pastas entre o sistema host e um contêiner. Ele é muito útil para transferir dados ou atualizar arquivos dentro do contêiner sem precisar recriá-lo.

No exemplo abaixo, copiamos uma pasta do host para o contêiner especificado:

```bash
docker container cp pasta-host nome-do-container:/
```

## Desconectar de um Contêiner Sem Parar sua Execução

No Docker, ao pressionar `Ctrl + P` seguido de `Ctrl + Q` enquanto está dentro de um contêiner interativo (por exemplo, após usar `docker exec -it` ou `docker run -it`), você é desconectado do terminal interativo **sem interromper a execução do contêiner**. 

Isso permite que o contêiner continue rodando em segundo plano, enquanto você retorna ao terminal do sistema host para executar outros comandos.

### Como reconectar ao contêiner:

Se desejar voltar ao terminal interativo do mesmo contêiner, utilize o comando:

```bash
docker attach nome-ou-id-do-container
```

## Obter Informações Detalhadas de um Contêiner

O comando `docker container inspect` exibe informações detalhadas sobre um contêiner específico. Ele retorna os dados em formato JSON, incluindo configurações, status, rede, volumes e outras propriedades importantes.

No exemplo abaixo, inspecionamos um contêiner pelo seu nome ou ID:

```bash
docker container inspect nome-ou-id-do-container
```

Esse comando é útil para diagnosticar problemas, verificar configurações ou obter informações detalhadas sobre o contêiner em execução.

## Executar um Contêiner com Volume Montado

O comando abaixo cria e executa um contêiner chamado `teste-volume` utilizando a imagem `alpine`. Ele monta um volume local na pasta `/home/user/bkp/` do host dentro do contêiner, no caminho `/bkp`. 

```bash
docker container run -v /home/user/bkp/:/bkp/ --name teste-volume -it alpine sh
```

- `-v /home/user/bkp/:/bkp/` Monta o diretório local /home/user/bkp/ no caminho /bkp dentro do contêiner, permitindo acesso e manipulação dos arquivos no host.

## Executar um Contêiner com Nginx e Mapeando Rotas

O comando abaixo cria e executa um contêiner chamado `nginx` utilizando a imagem oficial `nginx`. O contêiner será executado em segundo plano e a porta 80 do host será mapeada para a porta 80 do contêiner.

```bash
docker container run -d -p 80:80 --name nginx nginx
```

- `-d` Faz o contêiner ser executado em segundo plano (modo detached).
- `-p 80:80` Mapeia a porta 80 do host para a porta 80 do contêiner, permitindo acessar o servidor web Nginx pelo endereço do host.
- `--name nginx` Define o nome do contêiner como nginx para facilitar sua identificação.
- `nginx` Especifica a imagem utilizada para criar o contêiner, que neste caso é a imagem oficial do Nginx.

## Visualizar Logs de um Contêiner

O comando abaixo exibe os logs do contêiner chamado `nginx`. Isso é útil para verificar mensagens de erro, saídas padrão ou qualquer registro gerado pelo contêiner.

```bash
docker container logs nginx
```

- `logs` Mostra os logs do contêiner especificado.
- `nginx` Nome do contêiner cujos logs serão exibidos.

Você pode usar esse comando para monitorar o comportamento do contêiner e depurar possíveis problemas.

## Criar uma Nova Imagem a Partir de um Contêiner

O comando abaixo cria uma nova imagem a partir de um contêiner existente chamado `nginx-name`. A imagem gerada será nomeada como `nginx-name-img`.

```bash
docker container commit nginx-name nginx-name-img
```

- `commit` Cria uma nova imagem com base no estado atual de um contêiner.
- `nginx-name` Nome ou ID do contêiner que será usado como base para criar a nova imagem.
- `nginx-name-img` Nome atribuído à nova imagem gerada.

Esse comando é útil quando você deseja salvar as alterações feitas em um contêiner como uma nova imagem reutilizável.

## Exportar uma Imagem Docker para um Arquivo

O comando abaixo salva a imagem `nginx-name-img` em um arquivo chamado `nginx-name.tar`. Esse arquivo pode ser usado para transferir ou armazenar a imagem.

```bash
docker image save -o nginx-name.tar nginx-name-img
```

- `save` Exporta uma imagem Docker para um arquivo no formato TAR.
- `-o nginx-name.tar` Especifica o nome do arquivo de saída onde a imagem será salva.
- `nginx-name-img` Nome da imagem Docker que será exportada.

Esse comando é útil para compartilhar imagens Docker entre sistemas ou para backup.

## Importar uma Imagem Docker de um Arquivo

O comando abaixo importa uma imagem Docker a partir de um arquivo chamado `nginx-name.tar`. Isso recria a imagem no ambiente Docker local.

```bash
docker image load -i nginx-name.tar
```

- `load` Importa uma imagem Docker de um arquivo no formato TAR.
- `-i nginx-name.tar` Especifica o arquivo de entrada contendo a imagem exportada.

Esse comando é útil para restaurar imagens salvas ou transferidas de outro sistema.

## Executar um Contêiner Interativo e Removível

O comando abaixo executa um contêiner chamado `nginx-name` utilizando a imagem `nginx-name-img`. O contêiner é iniciado em modo interativo, e será automaticamente removido ao ser parado.

```bash
docker container run -it --rm --name nginx-name nginx-name-img sh
```

- `run` Inicia um novo contêiner.
- `-it` Permite interação com o terminal do contêiner (modo interativo).
- `--rm` Remove o contêiner automaticamente ao ser encerrado.
- `--name nginx-name` Define o nome do contêiner como nginx-name.
- `nginx-name-img` Nome da imagem utilizada para criar o contêiner.
- `sh` Executa o shell dentro do contêiner.

Esse comando é útil para testes rápidos, já que o contêiner será apagado automaticamente após o uso.

## Ver Histórico de Modificações de uma Imagem

O comando abaixo exibe o histórico de camadas e modificações realizadas na construção da imagem `image-name`.

```bash
docker image history image-name
```

- `image` Especifica que o comando é para manipulação de imagens.
- `history` Mostra as camadas de construção de uma imagem Docker.
- `image-name` Nome da imagem cuja história será exibida.

Esse comando é útil para verificar as etapas realizadas durante a criação da imagem, como comandos executados, alterações de arquivos e outras configurações.

## Exportar o Sistema de Arquivos de um Contêiner

O comando abaixo exporta o sistema de arquivos do contêiner `teste-export` e salva em um arquivo compactado no formato `.tar`.

```bash
docker container export teste-export -o teste-export.tar
```

- `container` Especifica que o comando está relacionado a contêineres.
- `export` Exporta o sistema de arquivos de um contêiner em execução ou parado.
- `teste-export` Nome ou ID do contêiner a ser exportado.
- `-o teste-export.tar` Define o nome do arquivo de saída, neste caso, teste-export.tar.

Este comando é útil para criar um backup do sistema de arquivos de um contêiner ou para transferir o sistema de arquivos para outra máquina.

## Importar uma Imagem a Partir de um Arquivo TAR

O comando abaixo importa o sistema de arquivos exportado (arquivo `.tar`) como uma nova imagem Docker.

```bash
docker image import teste-export.tar ubuntu-importado
```

- `image` Indica que o comando está relacionado a imagens Docker.
- `import` Importa o conteúdo de um arquivo .tar como uma imagem Docker.
- `teste-export.tar` Nome do arquivo que contém o sistema de arquivos exportado.
- `ubuntu-importado` Nome da nova imagem Docker criada a partir do arquivo.

Este comando é útil quando você exporta o sistema de arquivos de um contêiner e deseja utilizá-lo para criar uma nova imagem Docker. Você pode, por exemplo, reutilizar a imagem em outro ambiente.

## Remover Imagens Não Utilizadas

O comando abaixo remove todas as imagens de contêineres que não estão mais sendo utilizadas no Docker, ajudando a liberar espaço em disco.

```bash
docker image prune
```

- `image` Indica que o comando é relacionado a imagens Docker.
- `prune` Remove recursos que não estão mais em uso, neste caso, imagens órfãs (dangling images), que não possuem tag ou associação com contêineres.

Este comando é útil para manter o ambiente de Docker limpo, evitando o acúmulo de imagens desnecessárias. Caso deseje evitar a confirmação manual, você pode utilizar a flag -f

### Observação
Este comando não remove imagens em uso. Para limpar todas as imagens não utilizadas, incluindo as associadas a contêineres parados, use o comando:

```bash
docker system prune.
```

## Baixar uma Imagem do Docker Hub

O comando abaixo baixa a imagem oficial `alpine` do Docker Hub para o seu ambiente local.

```bash
docker image pull alpine
```

- `image` Indica que o comando é relacionado a imagens Docker.
- `pull` Faz o download de uma imagem do repositório oficial do Docker Hub.
- `alpine` Nome da imagem que será baixada. Neste caso, a imagem alpine, conhecida por ser leve e otimizada para contêineres.

Este comando é útil para garantir que a imagem necessária esteja disponível localmente antes de iniciar a criação de contêineres baseados nela. Caso você não especifique uma tag, a versão mais recente da imagem será baixada por padrão.

## Taggear e Enviar uma Imagem para um Registro

Os comandos abaixo são usados para adicionar uma nova tag a uma imagem local e enviá-la para um registro Docker (como o Docker Hub).

### Adicionar uma Tag à Imagem

```bash
docker image tag ubuntu repositório/meu-ubuntu:1
```

- `image tag` Adiciona uma nova tag a uma imagem existente.
- `ubuntu` Nome da imagem local que será taggeada.
- `repositório/meu-ubuntu:1` Novo nome e tag da imagem. O prefixo repositório/ geralmente indica o repositório do Docker Hub.

Este comando é útil para preparar uma imagem com um nome e tag específicos antes de enviá-la a um registro.

### Enviar a Imagem para um Registro

```bash
docker image push repositório/meu-ubuntu:1
```

- `image push` Envia a imagem especificada para o registro configurado (por exemplo, Docker Hub).
- `repositório/meu-ubuntu:1` Nome e tag da imagem que será enviada.

Certifique-se de estar autenticado no registro antes de executar este comando. Use docker login para fazer login no Docker Hub ou outro registro.

