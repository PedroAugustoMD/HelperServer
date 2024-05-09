# Configuração do Servidor

Esta documentação detalha o passo a passo para a configuração do servidor, em um ambiente que contempla Cloudfare, subdomínios, docker e banco de dados.

### Configuração inicial do servidor

1. Realize a instalação do Ubuntu server

---

2. Realize as atualizações de segurança:

```console
sudo apt update
```

```console
sudo apt upgrade
```

---

3. Configure o Firewall

```console
sudo ufw allow OpenSSH
```

```console
sudo ufw enable
```
