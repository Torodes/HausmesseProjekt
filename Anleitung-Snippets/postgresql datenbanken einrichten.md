1. pfad von datei ``pg_hba.conf`` suchen:
```bash
su postgres -c "psql -c 'show hba_file;'"
```

2. in der datei ``pg_hba.conf`` den abschnitt an 2.-obersten stelle hinzufügen:
```txt
local all icinga2_db           scram-sha-256
host  all icinga2_db 0.0.0.0/0 scram-sha-256
host  all icinga2_db      ::/0 scram-sha-256

local all icinga2web_db           scram-sha-256
host  all icinga2web_db 0.0.0.0/0 scram-sha-256
host  all icinga2web_db      ::/0 scram-sha-256

local all icinga2ido_db           scram-sha-256
host  all icinga2ido_db 0.0.0.0/0 scram-sha-256
host  all icinga2ido_db      ::/0 scram-sha-256
```
3. pgsql-service neustarten
```bash
sudo systemctl restart postgresql
```
4. auf os ebene auf user postgres wechseln
```bash
sudo su -l postgres
```
5. neuen nutzer und neue datenbank ``icinga2_db`` hinzufügen:
```bash
createuser -P icinga2_db
createdb -E UTF8 --locale en_US.UTF-8 -T template0 -O icinga2_db icinga2_db
psql -c 'CREATE EXTENSION IF NOT EXISTS citext;' icinga2_db
```
6. schema zu neuer datenbank ``icinga2_db`` hinzufügen
```bash
psql -U icinga2_db icinga2_db < /usr/share/icingadb/schema/pgsql/schema.sql
```
7. neuen nutzer und neue datenbank ``icinga2web_db`` hinzufügen:
```bash
createuser -P icinga2web_db
createdb -E UTF8 --locale en_US.UTF-8 -T template0 -O icinga2web_db icinga2web_db
psql -c 'CREATE EXTENSION IF NOT EXISTS citext;' icinga2web_db
```
8. schema zu neuer datenbank ``icinga2web_db`` hinzufügen
```bash
psql -U icinga2web_db icinga2web_db < /usr/share/icingaweb2/schema/pgsql.schema.sql
```
9. neuen nutzer und neue datenbank ``icinga2ido_db`` hinzufügen:
```bash
createuser -P icinga2ido_db
createdb -E UTF8 --locale en_US.UTF-8 -T template0 -O icinga2ido_db icinga2ido_db
psql -c 'CREATE EXTENSION IF NOT EXISTS citext;' icinga2ido_db
```
10. schema zu neuer datenbank ``icinga2ido_db`` hinzufügen
```bash
psql -U icinga2ido_db icinga2ido_db < /usr/share/icinga2-ido-pgsql/schema/pgsql.sql
```
10. von benutzer postgres abmelden:
```bash
exit
```

