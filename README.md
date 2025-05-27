# Debian-DHCP
# Instalação e Configuração do Servidor DHCP no Debian

Este repositório fornece instruções técnicas detalhadas para a instalação e configuração do serviço **ISC DHCP Server** em sistemas baseados em Debian Linux.

---

## Requisitos

- Sistema operacional Debian (mínimo Debian 10)
- Acesso root ou sudo
- Interface de rede configurada e ativa
- Conectividade com os clientes na rede local

---

# 1. Instalar o Servidor DHCP

## Atualize os pacotes do sistema:
sudo apt update && sudo apt upgrade -y

## Instale o pacote do servidor DHCP:
sudo apt install isc-dhcp-server -y

# 2. Configurar Interface de Rede para o DHCP

## Edite o arquivo /etc/default/isc-dhcp-server:
sudo nano /etc/default/isc-dhcp-server

## Localize a linha:
INTERFACESv4=""

## E adicione a interface que vai fornecer os IPs (ex: eth0 ou enp0s3):
INTERFACESv4="eth0"

# 3. Configurar o Escopo de IPs

## Edite o arquivo principal de configuração do DHCP:
sudo nano /etc/dhcp/dhcpd.conf

## Exemplo de configuração básica:
## Configurações Globais
 option domain-name "empresa.local";
 
 option domain-name-servers 8.8.8.8, 8.8.4.4;
 
 authoritative;

## Escopo para rede 192.168.1.0/24

 subnet 192.168.1.0 netmask 255.255.255.0 {
 
 range 192.168.1.100 192.168.1.200;
 
 option routers 192.168.1.1;
 
 option broadcast-address 192.168.1.255;
 
 default-lease-time 600;
 
 max-lease-time 7200;
 
 }

Altere os valores de IP conforme a sua rede local.

# 4. Iniciar e Habilitar o Serviço

sudo systemctl restart isc-dhcp-server

sudo systemctl enable isc-dhcp-server

## Verifique o status do serviço:

sudo systemctl status isc-dhcp-server







