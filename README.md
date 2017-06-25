# fz_mastodon

## Prerequisites

Para esss demostracao foi utilizado sistema operacional ubuntu 16.04.02
"Versao do docker Docker version 17.05.0-ce, build 89658be"
docker-compose version 1.14.0, build c7bdf9e

##Siga os passos abaixo

O comando abaixo ira gerar e/ou baixar as imagens necessarias para subir todos os componentes do ambiente
    docker-compose build

O comando abaixo a seguir eh utilizado para gerar os secrets que deverao ser inseridos no arquivo .env.production para as chaves PAPERCLIP_SECRET, SECRET_KEY_BASE, OTP_SECRET
(O arquivo ja contem um secret configurado para facilitar a demonstracao, mas caso deseja recriar todos os passos, digite o comando abaixo e substitua)
    docker-compose run --rm mastodon rake secret

O comando abaixo é necessário para a criacão das tabelas no banco de dados postgres

    docker-compose run --rm mastodon rake db:migrate

Também é necessário pre-compilar os assets

    docker-compose run --rm mastodon rake assets:precompile


Após isso certifique-se que todos os containers estao down para isso digite:

docker-compose down

E finalmente para subir todos os componentes digite

    docker-compose up ou docker-compose up -d


Para cadastro no mastodon é necessário uma confirmacao via e-mail e para tal foi configurado no arquivo .env.production uma configuracao de uma conta pessoal criada no sendgrid - https://sendgrid.com. Caso deseja utilizar outro servico de SMTP é necessário alterar as chaves SMTP_SERVER,SMTP_PORT,SMTP_LOGIN,SMTP_PASSWORD e SMTP_FROM_ADDRESS com os respectivos valores.


Umas vez que todos os containers estejam up voce devera acessar:

http://localhost:3000 para acessar o mastodon
http://localhost:5601 para acessar o painel do Kibana e acompanhar os logstash(No primeiro acesso é necessario no combobox Time-field name selecionar o valor "@Timestamp")

##TO DO
 Configurar nginx
 Configurar monitoria com https://www.influxdata.com/time-series-platform/

 
