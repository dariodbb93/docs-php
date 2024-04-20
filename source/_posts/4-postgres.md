---
title: Postgres on linux
subtitle: postgres
categories:
    - database relazionali
---

![image.png](/assets/img/postgres.png)

In questa guida vedremo come installare un'istanza di postgresql in un server linux. <br>

1. aggiornare i pacchetti di sistema
```bash
sudo apt && sudo apt upgrade
```

2. installare il pacchetto di postgres 
```bash
sudo apt install postgresql postgresql-contrib
```

3. accedere alla CLI di postgres
```bash
sudo -i -u postgres
```
4. creare un nuovo database
```bash
createdb nome_database
```
5. configurazione delle connessioni da client esterno
```bash
sudo nano /etc/postgresql/<versione>/main/pg_hba.conf
```
Cambia l'indirizzo IP da host all all 127.0.0.1/32 md5 a host all all 0.0.0.0/0 md5 per consentire le connessioni da qualsiasi indirizzo IP. <br>

6. riavviare l'istanza del motore database postgres

```bash
sudo service postgresql restart
```



