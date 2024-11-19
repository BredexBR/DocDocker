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
