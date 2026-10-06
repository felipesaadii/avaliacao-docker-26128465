# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Felipe Saadi Nesso
Matrícula: 26128465
Usuário do GitHub: felipesaadii
Usuário do Docker Hub: felipesaadii

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

Usei a imagem base nginx:1.27-alpine. O tamanho final da imagem do portal foi 73.6 MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.

   O Nginx procura os arquivos do site em /usr/share/nginx/html. Usei o comando docker exec teste-portal ls /usr/share/nginx/html para conferir se o index.html estava dentro do container.

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

felipesaadii/agrovale-portal:1.0-26128465
Repositório: https://hub.docker.com/r/felipesaadii/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

Porque o token de acesso é usado para autenticação do Docker Hub de forma mais segura, sem precisar utilizar diretamente a senha da conta.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |

| 1 | O conteúdo de site não era copiado para a pasta servida pelo Nginx |O container iniciou normalmente, mas ao acessar localhost:7065 apareceu a página padrão “Welcome to nginx!”, em vez da página “Voltamos em breve”. | COPY site/ /usr/share/nginx/html/|

| 2 | A porta 80 não estava documentada no Dockerfile| Depois de corrigir o primeiro problema, a página “Voltamos em breve” passou a aparecer e o container continuou em execução. Porém, percebi que o Dockerfile não tinha a porta 80 documentada.|Adicionei EXPOSE 80. |

| 3 | O WORKDIR estava apontando para /usr/share/nginx, e não para a pasta de conteúdo do Nginx|O WORKDIR /usr/share/nginx não era necessário para o funcionamento da página e não correspondia diretamente à pasta onde o Nginx serve o site. |Remover o WORKDIR ou usar /usr/share/nginx/html|

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

-p 7042:80 significa que a porta 7042 do computador (host) será ligada à porta 80 do container.
 Já -p 80:7042 liga a porta 80 do computador à porta 7042 do container. A porta do container é sempre o número que vem depois dos dois-pontos (

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

Porque db é o nome do serviço do MariaDB no Docker Compose. Os containers conseguem se comunicar pela rede do Compose usando o nome do serviço. localhost apontaria para o próprio container do WordPress, e não para o MariaDB.Porque db é o nome do serviço do MariaDB no Docker Compose. Os containers conseguem se comunicar pela rede do Compose usando o nome do serviço. localhost apontaria para o próprio container do WordPress, e não para o MariaDB.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

   Porque o WordPress acessa o banco diretamente pela rede interna do Docker, usando o serviço db. Não é necessário expor o banco para o computador ou para a internet.
   Para consultar o banco sem publicar a porta, podemos usar:
   docker compose exec db mariadb -u root -p

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

sei docker compose down para derrubar a stack e docker compose up -d para subi-la novamente. O comando que poderia apagar o post seria docker compose down -v, pois ele remove os volumes.

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
