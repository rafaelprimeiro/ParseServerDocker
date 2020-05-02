
Required 

.env file in api/
create with this keys APPID, MASTERKEY and PORT
eg.:
APPID=MyAppId
MASTERKEY=MyMasterKey
PORT=3000


Dockerfile
FROM é a imagem já existe que vamos usar, no caso do banco de dados será o mongo
ENV são as variáveis de ambiente do container que iremos passar para a imagem


Buildar imagem do Dockerfile

docker build -t mongo-image -f db/Dockerfile .

Criando o container
docker run -d -v $(pwd)/db/data:/data/db --rm --name mongo-parse-server-rg mongo-image

run = é para criar o container
-d = é para executar em backgoud o container
--rm = é para rmover o container caso ele já exista
--name = é o nome do container


Rodando comandos dentro do Dockerfile
docker exec -i mongo-parse-server-rg COMANDO

-i = é interativo, é usado quando precisamos ter acesso a um projeto interativo como por exemplo o shell, precisamos rodar com -i, isso faz com q o processo não seja finalizado até que seja concluido.

Use docker exec -it some-mongo bash para acessar o bash do container


-- nodemon 
 instalar no node para manter ele rodando

 API 
 build imagem
 docker build -t node-image -f api/Dockerfile .

 subir imagem
 docker run -d -v $(pwd)/api:/home/node/app -p 443:3000 --link mongo-parse-server-rg --rm --name node-parse-server-rg node-image

 subir tudo com docker compose
 na raiz do projeto execute docker-compose up -d