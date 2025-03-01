# Comandos e dicas do docker

## Curso

[Curso de Docker Alura](https://cursos.alura.com.br/course/docker-e-docker-compose)

## Aplicações

- Instalar docker

  https://docs.docker.com/engine/install/ubuntu/
  
  https://docs.docker.com/engine/install/linux-postinstall/ (evitar docker pedir sudo)
  
  https://docs.docker.com/compose/install/

- Dive (Analisar imagem docker)

  https://github.com/wagoodman/dive
  
- Dock Station (Ferramenta visual para docker)

  https://dockstation.io/

## Comandos

- Rodando o Hello Word:

```docker run hello-word```

- Listar containers ativos:

```docker ps```

- Listar todos containers:

```docker ps -a```

- Listar imagens:
 
```docker images```

- Parar container (wait default de 10 segundos):

```docker stop CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Parar container diminuindo tempo de wait:

```docker stop -t 0 CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Parar todos os caontainers:

```docker stop $(docker ps -q)```

- Remover container um a um:

```docker rm CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Remover todos containers inativos:

```$ docker rm $(docker ps -aq)```

- Remover imagem:

```docker rmi REPOSITORY```

- Remover todas as imagem:

```docker rmi -f $(docker images -q)```

- Remover todos os volumes:

```docker volume prune -f```

- Remover todas as networks:

```docker network prune -f```

- Remover todo cache de build:

```docker builder prune -f```

- Rodando imagem de static site (-d detached sem travar terminal, sem atribuir porta):

```docker run -d dockersamples/static-site```

- Rodando imagem de static site (-d detached sem travar terminal, utilizando porta aleatoria):

```docker run -d -P dockersamples/static-site```

- Rodando imagem de static site adicionado alias para o container:

```docker run -d -P --name meu-site dockersamples/static-site```

- Para ver qual porta esta sendo utilizada pelo container:

```docker port CONTAINER_ID```

- Mapear uma porta a sua escolha(-p PORTA_LOCAL:PORTA_INTERNA_CONTAINER);

```docker run -d -p 12345:80 dockersamples/static-site```

- Adicionar variavel de ambiente(-e NOME_VAR="VALOR"):

```docker run -d -P -e AUTHOR="Douglas Adams" dockersamples/static-site```

- Listar apenas id dos containers ativos:

```docker ps -q```

- Concatenar comandos (para todos os containers da lista de ativos):

```docker stop -t 0 $(docker ps -q)```

- Inspecionar container:

```docker inspect CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Criação de VOLUMES:

```
ex: docker run -v "/var/www" ubuntu
Inspecionar o container
Verá em mount "Destination" (caminho do volume dentro do container) e "Source" (caminho no docker host/maquina local)
Obs: mesmo matando o container, o volume no docker host/maquina local se mantem
```

- Criando volume definindo caminho na maquina local (-it terminal interativo, quando rodar o comando ja loga na maquina do container):

```docker run -it -v "/home/teste_ubuntu:/var/www" ubuntu```

- Ver processos do container:

```docker container top CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Ver todo o log:

```docker container logs --tail -n CONTAINER_ID_OU_PARTE_DELE_OU_NAME_DO_CONTAINER```

- Ver todos os logs:
  
```docker container ls```

- Mudar porta de uso do docker:

```
$ route -n (para ver as portas)
$ systemctl stop docker
$ sudo vim /etc/docker/daemon.json
inserir :
{
  "bip": "192.168.1.5/24", 
  "fixed-cidr": "192.168.1.5/25", 
  "default-address-pools":[{ "base":"192.168.2.5/24", "size":28 }]
} 
$ systemctl start docker
```

