# Instalasi Odoo 13
# Install Pip, Git dan Note js

sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less

# Adduser odoo13
sudo useradd -m -d /opt/odoo13 -U -r -s /bin/bash odoo13

# Install Database PostgresSQL
sudo apt install postgresql

# Add User Db Odoo13
sudo su - postgres -c "createuser -s odoo13"

# Install wkhtmltopdf
# aplikasi convert html to pdf

wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb

sudo apt install ./wkhtmltox_0.12.5-1.bionic_amd64.deb

