## SGBD
Instalar e configurar o SGBD PostgreSQL.

Comando para instalar o SGBD: 

```bash
sudo apt install -y postgresql
``` 
>Obs: O comando sudo, no nosso caso, pode ser omitido pois já somos root.
---
Realizando verificação do SGBD:
```bash
pg_lsclusters
``` 

Para realizar o acesso ao SGBD **sem senha**, utilizar o comando: 

```bash
sudo -u postgres psql
``` 
>Com esse comando o acesso é feito sem senha, pois o Linux já provou quem você é (root). Autenticação PEER.

Para primeiro acesso, alterei a senha:

```sql 
ALTER USER postgres PASSWORD '1234';   
``` 

>O retorno correto, é `ALTER ROLE`.

Para sair do postgres , comando é `\q` (igual o `\quit` de varios jogos).

```mermaid
graph LR
A[sudo -U postgres psql -h 127.0.0.1]--<b>Autenticação</b>--> B[Só funciona entrando dentro do proprio Linux - Ubuntu, Debian.]
```
```mermaid
graph LR
A[sudo psql -h 127.0.0.1 -U postgres] --<b>Autenticação</b--> B[Funciona vindo de qualquer maquina, porque é necessario inserir a senha.]
```
---
## Configurações de Serviço
>Caminho para as configurações

![
](<Captura de tela 2026-08-05 095316.png>)

Primeira configuração:
```bash
sudo nano postgresql.conf
```
CTRL + W para buscar a linha do listen_addresses e decomentamos, alterando para `*`.

Se ficar localhost, somente meu pc acessa.

**Passo 2:**
```bash
sudo nano pg_hba.conf
```
Nas ultimas linhas (CTRL + fn + end), adicionei: `host - all - all - 10.87.38.0/24 - scram-sha-256`

**Para criar um banco de dados, usamos o comando:**
```sql
CREATE DATABASE lojamax;
```
Para visualizar os bancos, usamos:
```bash
\l
```