#!/bin/bash

# Atualiza os pacotes do sistema
echo "Atualizando pacotes do sistema..."
sudo apt update -y
sudo apt upgrade -y

# Instala o Apache
echo "Instalando o Apache..."
sudo apt install apache2 -y

# Configura o firewall para permitir tráfego HTTP e HTTPS
echo "Configurando o firewall para permitir tráfego HTTP e HTTPS..."
sudo ufw allow in "Apache Full"

# Cria uma página de teste simples para verificar se o Apache está funcionando
echo "Criando uma página de teste..."
echo "<!DOCTYPE html>
<html lang='pt-br'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <title>Servidor Web Apache - Teste</title>
</head>
<body>
    <h1>Servidor Web Apache está funcionando!</h1>
    <p>Esta página foi criada automaticamente pelo script de provisionamento.</p>
</body>
</html>" | sudo tee /var/www/html/index.html > /dev/null

# Reinicia o Apache para aplicar as configurações
echo "Reiniciando o Apache..."
sudo systemctl restart apache2

# Verifica o status do Apache para garantir que está rodando corretamente
echo "Verificando status do Apache..."
sudo systemctl status apache2 | grep "Active"

# Mensagem de conclusão
echo "Servidor web Apache provisionado com sucesso!"
echo "Acesse o servidor em http://<seu_ip_servidor> para verificar a página de teste."
