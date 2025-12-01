# Docker – Microsserviços com Load Balancer (Baseado na Aula da DIO)

Este repositório é uma versão reorganizada e aprimorada do projeto apresentado na aula  
**"Docker: Utilização Prática no Cenário de Microsserviços"**, do instrutor **Denilson Bonatti**.

O objetivo é demonstrar:

- Microsserviços em containers
- Balanceamento de carga com NGINX
- Múltiplas instâncias PHP
- Banco de dados MySQL em container
- Arquitetura organizada via Docker Compose

---

## 🧱 Arquitetura

```

```
            ┌───────────────────────────┐
            │        NGINX (LB)          │
            │      porta: 4500           │
            └────────────┬──────────────┘
                         │
  ┌──────────────────────┼──────────────────────┐
  │                      │                      │
```

┌────────────┐        ┌────────────┐        ┌────────────┐
│   app1     │        │   app2     │        │   app3     │
│  PHP-FPM   │        │  PHP-FPM   │        │  PHP-FPM   │
└────────────┘        └────────────┘        └────────────┘
└────────────────┬────────────────┘
│
┌──────────────┐
│    MySQL     │
└──────────────┘

```

---

## 🚀 Como executar

### 1️⃣ Crie o arquivo `.env`
O projeto já fornece um `.env`:

```

DB_HOST=db
DB_USER=root
DB_PASS=Senha123
DB_NAME=meubanco
NGINX_PORT=4500

````

---

### 2️⃣ Suba todos os serviços

```sh
docker-compose up -d --build
````

---

### 3️⃣ Acesse no navegador

```
http://localhost:4500
```

A cada acesso, o load balancer envia a requisição para um dos 3 containers PHP e insere um registro no MySQL.

---

## ⚙️ Escalar os serviços

Por exemplo, para 10 containers PHP:

```sh
docker-compose up --scale app1=10 -d
```

*(ou duplique serviços no compose)*

---

## 📂 Estrutura do projeto

```
app/
nginx/
db/
.env
docker-compose.yml
README.md
```

---

## 📝 Créditos

Projeto baseado na aula da Digital Innovation One (DIO)
Instrutor: **Denilson Bonatti**
