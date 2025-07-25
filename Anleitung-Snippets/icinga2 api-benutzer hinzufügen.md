1. folgendes zur conf-datei hinzufügen (und passwort ändern):
```txt
object ApiUser "icinga2-api" {
	password = "CHANGEME"
	permissions = [ "actions/*", "objects/modify/*", "objects/query/*", "status/query" ]
}
```
2. icinga2-service neustarten:
```bash
sudo systemctl restart icinga2
```
