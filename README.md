# Urlaubsverwaltung

## Setup

### Voraussetzungen

- Docker und Docker Compose installiert
- Git installiert

### Vorgehensweise

1. Repository klonen:

```bash
git clone https://github.com/maxptg/urlaubsverwaltung-docker-wiwi.git
```

2. In das Verzeichnis wechseln:

```bash
cd urlaubsverwaltung-docker-wiwi
```

3. `docker-compose.yml` anpassen:

   - Setzen der korrekten IP-Adressen
   - Ändern des Mailservers zu HTWD Mailserver
   - `redirectUris` korrekt mit der internen IP-Adresse setzen

4. Passwörter der Benutzer im Keycloak-Admin-Interface setzen:

   - Gehe zu `http://<IP-Adresse>:8080/auth/admin/`
   - Melde dich mit den Standard-Admin-Zugangsdaten an (siehe `docker-compose.yml`):
   - Navigiere in das Realm `urlaubsverwaltung`
   - Wähle alle Benutzer aus und setze ein Passwort (siehe Anwenderdokumentation)

5. Zuerst mit dem Admin-Benutzer anmelden und dann mit allen anderen Benutzern
6. Setzen der Rollen aller Benutzer in der Urlaubsverwaltung
7. Testweise Durchspielen der Use-Cases aus der Anwenderdokumentation

### Betrieb

- Anlegen der korrekten Benutzer
    - Persistente Speicherung der Benutzer ist gewährleistet
    - Änderungen an Standardbenutzern werden **überschrieben**!

## Änderungen zur Doku

- Die Benutzer sind nun in der `keycloak/import/urlaubsverwaltung-realm.json` Datei definiert.
    - Diese haben auch **keine** Passwörter mehr und müssen über die Keycloak Admin Console gesetzt werden.
- Der erste Benutzer, der sich in der Urlaubsverwaltung anmeldet, wird automatisch zum Admin (Office-Rolle).
- Die Benutzer werden nun auch persistent gespeichert -> Neustart der Compose setzt **keine** Benutzer mehr zurück.
- Die Abteilung muss noch erstellt werden (bspw. "Fakutät Wirtschaftswissenschaften")
    - Zuweisung aller Benutzer zu dieser Abteilung ("gehört zur Abteilung")
    - Sekretär (Abteilungsleiter --> "ist Abteilungsleiter") sowie Dekan (Freigabe-Verantwortlicher --> "ist verantwortlich für die Freigabe vorläufig genehmigter Anträge") müssen noch ihre konkreten Berechtigungen für die Abteilung erhalten
    - Dies kann bei Navigaitonsleiste -> "Abteilungen" -> "Fakultät Wirtschaftswissenschaften" -> "Bearbeitet" getan werden
