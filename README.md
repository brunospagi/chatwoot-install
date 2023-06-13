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
**PARA FAZER ATUALIZAÇÃO DO CHATWOOT**

sudo -i -u chatwoot
cd chatwoot
git fetch origin tag v2.16.0 --no-tags
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
