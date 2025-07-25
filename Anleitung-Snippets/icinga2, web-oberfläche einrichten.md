1. im browser web-oberfläche unter addresse öffnen:
```url
http://[ip-adresse vom icinga-host]/icingaweb2/setup
```
2. auf icinga-host-maschine token (wie in anleitung) erstellen:
```bash
sudo su www-data -s /bin/sh -c "mkdir -m 2770 /etc/icingaweb; chgrp icingaweb2 /etc/icingaweb2; head -c 12 /dev/urandom | base64 | tee /etc/icingaweb2/setup.token; chmod 0660 /etc/icingaweb2/setup.token;";
```
3. "Icingadb"- und "Monitoring"-features aktivieren
4. authentication type: Database
5. daten für "Database Resource" (für icingaweb):
	1. Resource name: icinga2web_db
	2. Database type: PostgresSQL
	3. Host: localhost
	4. Port: 5432
	5. Database Name: icinga2web_db
	6. Username: icinga2web_db
	7. Password: (passwort vom icinga2web_db-benutzer in pgsql)
6. "Administration": Hier Daten für Weboberflächen-User eingeben (wird neu angelegt)
7. "Application Configuration" so lassen
8. "Icinga DB Resource":
	1. Database type: PostgresSQL
	2. Host: localhost
	3. Port: 5432
	4. Database Name: icinga2_db
	5. Username: icinga2_db
	6. Password: (passwort vom icinga2_db-benutzer in pgsql)
9. "Redis": Nur bei "Redis Host" ``localhost`` setzen
10. "Icinga 2 API":
	1. Host: localhost
	2. Port: 5665
	3. API Username: icinga2-api
	4. API Password: (passwort von icinga2-api, wie in datei (``/etc/icinga2/conf.d/api-users.conf``) gesetzt)
11. "Monitoring IDO Resource":
	1. Resource name: icinga2ido_db
	2. Database type: PostgresSQL
	3. Host: localhost
	4. Port: 5432
	5. Database Name: icinga2ido_db
	6. Username: icinga2ido_db
	7. Password: (passwort vom icinga2ido_db-benutzer in pgsql)
	8. INFO: evtl Validation skippen
12. "Command Transport":
	1. Transport Name: icinga2
	2. Transport Type: icinga 2 API
	3. Host: localhost
	4. Port: 5665
	5. API Username: icinga2-api
	6. API Password: (passwort von icinga2-api, wie in datei (``/etc/icinga2/conf.d/api-users.conf``) gesetzt)
13. "Monitoring Security": so lassen