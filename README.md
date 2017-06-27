# fz_mastodon

## Pré Requisitos

- Para essa demostração foi utilizado sistema operacional ubuntu Xenial 16.04.02:

   Versao do docker Docker version 17.05.0-ce, build 89658be
   docker-compose version 1.14.0, build c7bdf9e

## Siga os passos abaixo

- O comando abaixo irá gerar e/ou baixar as imagens do dockerhub necessárias para subir todos os componentes do ambiente localmente
 
       docker-compose build

- O comando abaixo a seguir é utilizado para gerar os secrets que deverão ser inseridos no arquivo .env.production para as chaves PAPERCLIP_SECRET, SECRET_KEY_BASE, OTP_SECRET com o intuito de a aplicação funcionar corretamente.

      docker-compose run --rm mastodon rake secret

O comando abaixo é necessário para a criação das tabelas no banco de dados postgres: 

      docker-compose run --rm mastodon rake db:migrate

Também é necessário pré-compilar os assets basta executar o comando abaixo:

      docker-compose run --rm mastodon rake assets:precompile


Após isso certifique-se que todos os containers estão down para isso digite:

      docker-compose down

E finalmente para subir todos os componentes digite: 

      docker-compose up ou docker-compose up -d


- Para cadastro no mastodon é necessário uma confirmação via e-mail e para tal foi configurado no arquivo .env.production uma configuracao de uma conta pessoal criada no sendgrid - https://sendgrid.com. Enviarei o api token por e-mail e deverá ser substituído na variavel SMTP_LOGIN. 

 - Caso deseja utilizar outro servico de SMTP é necessário alterar as chaves SMTP_SERVER,SMTP_PORT,SMTP_LOGIN,SMTP_PASSWORD e SMTP_FROM_ADDRESS com os respectivos valores.
 
 Umas vez que todos os containers estejam up voce deverá acessar:

- http://localhost:3000 para acessar o mastodon
- http://localhost:5601 para acessar o painel do Kibana e acompanhar os logstash(No primeiro acesso é necessário no combobox Time-field name selecionar o valor "@Timestamp")
 
- Poderá também acessar
  http://localhost (mastodon)
 E configurando o arquivo /etc/hosts da maquina com a nos nomes Kibana e chronograf apotando para 127.0.0.1 podera acessar
 - http://kibana
 - http://chronograf
 
 - Monitoria Tick stack :
 
 Para acessar o painel do chronograf acesse: http://localhost:8888
 
 - Caso dejese utilizar o Influx cli execute :
 
         docker-compose run influxdb-cli
- Caso deseje acessar o Kapacitor cli execute:

         docker-compose run kapacitor-cli
         $ kapacitor list tasks


 
