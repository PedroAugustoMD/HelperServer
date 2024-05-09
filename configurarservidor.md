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

### Instalação do Docker

No Windows:

1. Acesse a url https://www.docker.com/
2. Faça download do Docker Desktop
3. Abra o instalador de siga as instruções
4. **Na instalação esteja certo de que tem um WSL(Subsistema do Windows para Linux) instalado, configurado e aberto**

---

No Linux

1. Abra o terminal
2. Atualize o sistema

```console
sudo apt update
```

3. Instale o Docker

- Ubuntu:

```console
sudo apt install docker.io
```

- Sistemas baseados em RPM:

```console
sudo yum install docker
```

4. Inicie o Docker

- systemd:

```console
sudo systemctl start docker
```

- init.d:

```console
sudo service docker start
```

5. Habilite o Docker para iniciar automaticamente no boot

- systemd:

```console
sudo systemctl enable docker
```

- init.d:

```console
sudo chkconfig docker on
```

### Configuração do Banco de Dados

1. Faça o pull da imagem:

```console
docker pull postgres
```

2. Crie um volume do Docker

```console
docker volume create postgres_data
```

3. Execute o contêiner do Docker PostgreSQL

```console
$ docker run -itd -e POSTGRES_USER=MYUSER -e POSTGRES_PASSWORD=MYPASSWORD -p 5432:5432 -v postgres_data:/var/lib/postgresql/data --name postgresql postgres:latest
```

Modifique o nome de usuário e senha

4. Para criar uma tabela no banco de dados, use o seguinte comando:

```console
$ docker exec -it postgresql psql -U baeldung -d baeldung -c "CREATE TABLE baeldungauthor (AUTHOR_ID SERIAL PRIMARY KEY NOT NULL, AUTHOR_NAME TEXT NOT NULL, AUTHOR_AGE INT NOT NULL, AUTHOR_LEVEL INT NOT NULL);"
```

## Modifique as informações da tabela

### Configuração do Cloudfare

1. Crie um conta no https://www.cloudflare.com/pt-br/ e abra o painel de controle.
2. Selecione a opção "Add Site" e digite o seu domínio
3. Clique na guia "DNS" e selecione a opção "Add Record".
4. Registre o subdomínio com um registro adequado: "A" para endereços IPv4 e "CNAME" para outros domínios ou subdomínios.
5. Ative o proxy ao lado do registro DNS correspondente.
6. Salve as alterações.
