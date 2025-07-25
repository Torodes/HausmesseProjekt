1. icingadb- und icingadb-web-packages installieren:
```bash
sudo apt install icingadb icingadb-web
```
2. icinga2-ido-pgsql (für verwendung mit postgresql) installieren (bei einer der Abfragen auf manuelles einrichten bestehen!):
```bash
sudo apt install icinga2-ido-pgsql
```
3. icingadb-service aktivieren und starten
```bash
sudo systemctl enable --now icingadb
```
4. ido-pgsql feature in icinga2 aktivieren + icinga2 neustarten:
```bash
sudo icinga2 feature enable ido-pgsql
```
```bash
sudo systemctl restart icinga2
```
5. datei ``/etc/icinga2/features-enabled/ido-pgsql.conf`` anpassen, damit folgender eintrag für datenbankverbindung drin steht:
```txt
library "db_ido_pgsql"

object IdoPgsqlConnection "ido-pgsql" {
	user = "icinga2ido_db"
	password = [passwort von pgsql-benutzer "icinga2ido_db"]
	host = "localhost"
	database = "icinga2ido_db"
}
```