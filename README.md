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

# Install and Configure Odoo 
# pindah ke user odoo13 yg telah dibuat
sudo su - odoo13

# Git pull source odoo ke /opt
git clone https://www.github.com/odoo/odoo --depth 1 --branch 13.0 /opt/odoo13/odoo

# Buat virtual env odoo biar terisolate
cd /opt/odoo13
python3 -m venv odoo-venv
source odoo-venv/bin/activate

# Install pip3 dan paket yg dibutuhkan
pip3 install wheel
pip3 install -r odoo/requirements.txt

# Meng nonaktifkan 
deactivate

# Buat folder u oddo custom addons
mkdir /opt/odoo13/odoo-custom-addons

# Konfigurasi settingan db dll
sudo nano /etc/odoo13.conf

## isinya
[options] ; This is the password that allows database operations:
admin_passwd = my_admin_passwd
db_host = False
db_port = False
db_user = odoo13
db_password = False
addons_path = /opt/odoo13/odoo/addons,/opt/odoo13/odoo-custom-addons

# setting odoo13.service
sudo nano /etc/systemd/system/odoo13.service
# isi
[Unit]
Description=Odoo13
Requires=postgresql.service
After=network.target postgresql.service

[Service]
Type=simple
SyslogIdentifier=odoo13
PermissionsStartOnly=true
User=odoo13
Group=odoo13
ExecStart=/opt/odoo13/odoo-venv/bin/python3 /opt/odoo13/odoo/odoo-bin -c /etc/odoo13.conf
StandardOutput=journal+console

[Install]
WantedBy=multi-user.target

# setting systemctl -> u reload service
sudo systemctl daemon-reload

# Aktifkan service
sudo systemctl enable --now odoo13

# verifikasi service
sudo systemctl status odoo13

# liat log
sudo journalctl -u odoo13

# akses user -> http://<your_domain_or_IP_address>:8069












