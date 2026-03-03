# 🏢 Organizações Garyana - Site de Produção

Bem-vindo ao repositório do site da **Organizações Garyana Comércio Geral**!

## 📋 Conteúdo do Repositório

- **`index.html`** - Site completo com design responsivo
- **`nginx.conf`** - Configuração Nginx para Ubuntu 20.04/22.04
- **`deploy.sh`** - Script automatizado para deploy
- **`README.md`** - Este arquivo

## 🚀 Como Fazer Deploy no VPS

### Pré-requisitos

- Ubuntu 20.04 ou 22.04
- Acesso SSH ao VPS (como root ou com sudo)
- Domínio configurado apontando para o IP do VPS: `192.168.1.1`
- Certbot e Let's Encrypt serão instalados automaticamente

### Instalação Rápida (Recomendado)

1. **SSH no seu VPS:**
```bash
ssh root@192.168.1.1
```

2. **Clone o repositório:**
```bash
git clone https://github.com/valentediego26-commits/site.ORG-GARYANA.git
cd site.ORG-GARYANA
```

3. **Execute o script de deploy:**
```bash
chmod +x deploy.sh
sudo ./deploy.sh
```

O script irá:
- ✅ Instalar Nginx
- ✅ Instalar Certbot (Let's Encrypt)
- ✅ Clonar/atualizar o repositório
- ✅ Configurar SSL/HTTPS
- ✅ Ativar renovação automática de certificado
- ✅ Iniciar o servidor

### Instalação Manual

Se preferir fazer passo a passo:

1. **Atualizar sistema:**
```bash
sudo apt-get update
sudo apt-get upgrade -y
```

2. **Instalar Nginx:**
```bash
sudo apt-get install -y nginx
```

3. **Clonar repositório:**
```bash
sudo git clone https://github.com/valentediego26-commits/site.ORG-GARYANA.git /var/www/site.ORG-GARYANA
```

4. **Configurar Nginx:**
```bash
sudo cp /var/www/site.ORG-GARYANA/nginx.conf /etc/nginx/sites-available/organizacoesgaryana.com
sudo ln -s /etc/nginx/sites-available/organizacoesgaryana.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl start nginx
sudo systemctl enable nginx
```

5. **Instalar certificado SSL:**
```bash
sudo apt-get install -y certbot python3-certbot-nginx
sudo certbot certonly --nginx \
    --non-interactive \
    --agree-tos \
    --email valentediego26@gmail.com \
    -d organizacoesgaryana.com \
    -d www.organizacoesgaryana.com
```

6. **Recarregar Nginx:**
```bash
sudo systemctl reload nginx
```

## 📝 Configurações Incluídas

### Nginx (`nginx.conf`)
- ✅ HTTPS/SSL com Let's Encrypt
- ✅ Redirecionamento HTTP → HTTPS
- ✅ Compressão Gzip
- ✅ Cache de assets (30 dias)
- ✅ Headers de segurança
- ✅ Proteção contra acesso a arquivos sensíveis

### SSL/HTTPS
- Certificado: Let's Encrypt (gratuito)
- Renovação automática: Cron job configurado
- Protocolos: TLSv1.2 e TLSv1.3

## 🔧 Comandos Úteis

### Ver logs do site
```bash
sudo tail -f /var/log/nginx/organizacoesgaryana_access.log
```

### Verificar status do Nginx
```bash
sudo systemctl status nginx
```

### Recarregar configuração (sem parar o servidor)
```bash
sudo systemctl reload nginx
```

### Atualizar site (após fazer git push)
```bash
cd /var/www/site.ORG-GARYANA
git pull origin main
sudo systemctl reload nginx
```

### Verificar renovação SSL
```bash
sudo certbot certificates
```

### Renovar manualmente (se necessário)
```bash
sudo certbot renew --force-renewal
```

## 🌐 Acessar o Site

Após o deploy:
- **HTTP:** http://organizacoesgaryana.com (redireciona para HTTPS)
- **HTTPS:** https://organizacoesgaryana.com ✅ (recomendado)

## 📧 Contato e Suporte

- **Email:** comercial.org.garyana@gmail.com
- **Telefone:** 923361154 / 928940161
- **NIF:** 5405160270

## 🔐 Segurança

O site inclui:
- ✅ HTTPS obrigatório
- ✅ Headers de segurança (HSTS, X-Frame-Options, etc.)
- ✅ Bloqueio de acesso a arquivos sensíveis
- ✅ Compressão e otimização

## 📱 Responsividade

O site é totalmente responsivo e funciona perfeitamente em:
- ✅ Desktop
- ✅ Tablet
- ✅ Mobile

## 🆘 Troubleshooting

### Certificado SSL não funciona
```bash
sudo certbot certonly --nginx -d organizacoesgaryana.com -d www.organizacoesgaryana.com
```

### Nginx não inicia
```bash
sudo nginx -t  # Verificar erros de configuração
sudo systemctl start nginx
```

### Permissões de arquivo
```bash
sudo chown -R www-data:www-data /var/www/site.ORG-GARYANA
sudo chmod -R 755 /var/www/site.ORG-GARYANA
```

## 📚 Mais Informações

- [Documentação Nginx](https://nginx.org/en/docs/)
- [Let's Encrypt](https://letsencrypt.org/)
- [Certbot](https://certbot.eff.org/)

---

**Desenvolvido com ❤️ para Organizações Garyana Comércio Geral**

*Última atualização: 03/03/2026*