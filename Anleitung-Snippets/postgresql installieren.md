1. postgresql installieren:
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```

2. Passwort vom psql-postgres-user ändern:
```bash
sudo -u postgres psql
```
```psql
\password postgres
```
