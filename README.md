**Manual de Instalação ChatWoot**

*OBS UBUNTU 22.04 RECOMENDADO!*

sudo apt update && apt upgrade -y

wget https://get.chatwoot.app/linux/install.sh

chmod +x install.sh

./install.sh --install

Use as opções abaixo

yes # Para Configurar Automaticamente Dominio!

chatwoot.dominio.com.br # seu dominio com o subdominio do chatwoot

contato@dominio.com.br # seu email para gerar certificado SSL 

yes para todos

#CASO DER ERRO OU DEMORAR MUITO REFAZER QUE A INSTALAÇÃO VAI SUBIR NORMANTE 
_______________________________________________________________________________________

Alterando Idioma e ativando sua tela de cadastro

cd /home/chatwoot/chatwoot
nano .env
Altere a linha
DEFAULT_LOCALE=pt_BR
ENABLE_ACCOUNT_SIGNUP=true
sudo systemctl restart chatwoot.target
Acesse: seudominio.com.br
Faça seu cadastro

_________________________________________________________________________________________

NOMES CHATWOOT TERMOS E POLITICA DE PRIVACIDADE

Acesse super Admin

https://seudominio.com.br/super_admin
Opção>installation_configs
LOGO
LOGO_THUMBNAIL
NOMES CHATWOOT:
Alterando nomes na plataforma
INSTALLATION_NAME
BRAND_NAME
TERMOS E POLITICA DE PRIVACIDADE
TERMS_URL
PRIVACY_URL
BRAND_URL
WIDGET_BRAND_URL


**PARA FAZER ATUALIZAÇÃO DO CHATWOOT**

sudo -i -u chatwoot

cd chatwoot

git fetch origin tag v2.17.0 --no-tags

rvm install "ruby-3.1.3"

rvm use 3.1.3 --default

bundle

yarn

rake assets:precompile RAILS_ENV=production

RAILS_ENV=production bundle exec rake db:migrate

exit 

**Habilitando configurações ocultas do Chatwoot**

*No banco de dados PostgreSQL*

sudo -u postgres psql

\c chatwoot_production

update installation_configs set locked = false;

\q

##Desistalar Chatwoot##

rm -rf /home/chatwoot
rm -rf /etc/nginx/sites-available/nginx_chatwoot.conf
rm -rf /etc/nginx/sites-enabled/nginx_chatwoot.conf

nginx -t

kill -9 $(lsof -i tcp:3000 -t)

# Uninstall ruby-sidekiq
sudo apt-get remove --auto-remove ruby-sidekiq
sudo apt-get purge ruby-sidekiq

# Uninstall ruby
aptitude purge ruby

#Elimiar user chatwoot
userdel -r chatwoot

service nginx restart
