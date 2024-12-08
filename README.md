# Comandos do Docker

 - docker ps: lista os containes.

 - docker ps -a: todos os containes mesmo os que não estão rodando.

 - docker run hello-world: executa uma imagem, imagem de teste do docker.

 - docker login: faz a autenticação no docker hub.

 - docker info: informação da instalação.

 - docker --version: informa.

 - docker run ubuntu: executa o ubundo mas é desativado porque não tem processo.

 - docker run -it ubuntu bash: executa o umbundo com um processo de bash, o -it siginifica que vai poder interagir.

 - docker stop 'id do container': para o container que tem aquele id.

 - id container do exemplo: e1567db3632d.

 - docker start 'id do container': retorna a ser executado.

 - docker exec -iti e1567db3632d bash: 
  - exec: executa
  - -iti: interagir
  - e1567db3632d: 'id container'
  - bash: programa que é para ser executado.

 - mkdir pasta_lincoln: comando linux para criar pasta pelo bash.

 - docker build -t spring-boot:1.0 .: gera imagem apartir de dockerfile, o -t é para definir um nome para a imagem, no final tem um ponto indicando o caminho do dockerfile.

 - docker run -P spring-boot:1.0: esse -P, siginifica que ele faz o mapeamento usando uma porta aleatoria da minha maquina principal.

 -

 -

# Docker Hub

 - https://app.docker.com

# Comandos do Dockerfile

 - FROM: busca/pega o que é pedido, depois do ":" informe a versao.

 - AS build: chama ele de build. 

<blockquete>

      FROM maven:3.8.4-jdk-8 AS build

</blockquete>

 - faz uma copia tudo que está em src, para a pasta src que está dentro da pasta app.
 
 - copia o arquivo pom.xml para a pasta app.

<blockquete>

      COPY src /app/src
      COPY pom.xml /app

</blockquete>

 - Muda o diretorio.
 
<blockquete>

      WORKDIR /app

</blockquete>

 - Executa comandos de qualquer aplicação, nesse exemplo é um comando do mave, sistema que gerencia pacotes de aplicação JAVA.
 
<blockquete>

      RUN mvn clean install

</blockquete>

 - Pega o jdk e escolhe a versão dele.

<blockquete>

      FROM openjdk:8-jre-alpine

</blockquete>

 - Copia o build que foi gerado, indica o nome do arquivo gerado,
 e informa o novo local que vai ser colado e o novo nome do arquivo.

<blockquete>

      COPY --from=build /app/target/spring-boot-2-hello-word-1.0.2-SNAPSHOT.jar /app/app.jar 


</blockquete>

 - Declara que vai expor a porta 8080
 
<blockquete>

      EXPOSE 8080

</blockquete>

 - Comandos finais
 
<blockquete>

      CMD ["java", "-jar", "app.jar"]

</blockquete>


# Conceito de mapeamento de portas

 - Quando define a porta 8080 para uma aplicação usando docker, ele vai rodar na porta 8080 do conteiner da aplicação, não vai aparecer na maquina principal, mas para exibir e funcionar na maquina principal, deve ser feito um mapeamento de portas!

 - docker run -P spring-boot:1.0: esse -P, siginifica que ele faz o mapeamento usando uma porta aleatoria da minha maquina principal.

 - docker run -p 8080:8080 spring-boot:1.0: esse -p 8080:8080, siginifica que ele faz o mapeamento usando a porta 8080 da minha maquina principal.

# Instalando o Docker no Ubunto(configurando a maquina pro deploy)

 - tutorial: https://www.hostinger.com.br/tutoriais/instalar-docker-ubuntu?utm_campaign=Generic-Tutorials-DSA|NT:Se|LO:BR-t1&utm_medium=ppc&gad_source=1&gclid=Cj0KCQiApNW6BhD5ARIsACmEbkX3-99Y3Avx0DpdESfNc0R5nbbtQXOZZ6Mb9NmjVxKcxcM6H2B7jMAaAhCFEALw_wcB

 - Precisa ter uma noção de VPS, porque vai precisar se conectar ao
  servidor VPS Linux usando SSH. 

 - Depois de logar na sua VPS, começa executando o comando que
  atualiza o sistema.

<blockquete>

      sudo apt update
      sudo apt upgrade

</blockquete>

- Instala o pacote de pré-registro.

<blockquete>

      sudo apt-get install  curl apt-transport-https ca-certificates software-properties-common

</blockquete>

- Adicione os Repositórios do Docker, comandos no link do tutorial.

<blockquete>

      https://www.hostinger.com.br/tutoriais/instalar-docker-ubuntu?utm_campaign=Generic-Tutorials-DSA|NT:Se|LO:BR-t1&utm_medium=ppc&gad_source=1&gclid=Cj0KCQiApNW6BhD5ARIsACmEbkX3-99Y3Avx0DpdESfNc0R5nbbtQXOZZ6Mb9NmjVxKcxcM6H2B7jMAaAhCFEALw_wcB

</blockquete>

- Instalar Docker Ubuntu

<blockquete>

      sudo apt install docker-ce

</blockquete>

- Outros detalhes de uso vai ter no tutorial.

# Botando a imagem do projeto no DockerHub.

- Cria conta e loga no dockerHub.

- Tem que ir no Security e criar um new access Token.

- Na sua maquina faz o login do DOCKERHUB usando o novo token.

- Cria um repositorio no dockerhub, só da um nome.

- Cria uma nova imagem fazendo o docker build -t, com o mesmo
 nome do repositorio!

- Faz um docker push, docker push e o nome do repositorio.

# Gerando uma imagem com build, informando uma arquitetura especifica.

 - Pode ser que o processo de cima de erro de plataforma/arquitetura.
 
 - Na hora que for executar o comando docker build, 
 usa o "--platform linux/amd64" por exemplo.

 - Com isso é informado a arquitetura especifica.

 - Tem que executar um comando chamado Docker Tag, caso já tenha uma
 imagem gerada com uma outra arquitetura.

 - Com o docker tag , vc apenas está criando uma imagem que existe
 só que com outra tag.

<blockquete>

      docker tag 'nome da imagem' 'novo nome da imagem'

</blockquete>

# Deploy da imagem.

- Baixa a imagem docker do projeto.

- Faz o mapeamento das portas usando docker run.

- Com isso seu sistema está no ar.
