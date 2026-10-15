# Einrichten: einmal am eigenen Rechner

Diese Anleitung brauchst du einmal, bevor du zum ersten Mal mit Claude in einem mokebo-Repo arbeitest. Sie ist für Mac geschrieben. Du brauchst dafür etwa 30 Minuten und an zwei Stellen dein Mac-Passwort.

Wörter wie Repo, Branch oder Pull Request sind neu für dich? Dann lies vorher [GitHub einfach erklärt](GITHUB-EINFACH-ERKLAERT.md).

## 1. GitHub-Konto

1. Leg auf github.com ein eigenes Konto an, mit deiner Firmen-Mailadresse. Ein Konto pro Person, kein gemeinsames.
2. Schalte die Zwei-Faktor-Anmeldung ein: oben rechts auf dein Bild, dann „Settings“, „Password and authentication“, „Enable two-factor authentication“. Eine Authenticator-App auf dem Handy reicht.
3. Schick deinen GitHub-Namen an die Org-Admins. Sie nehmen dich in die Org und in das Team „Alle“ auf. Erst danach darfst du in den Repos Änderungen hochladen.

## 2. Programme installieren

Du brauchst vier Programme. Die ersten drei installierst du über Homebrew, ein Werkzeug, das Programme auf dem Mac installiert.

1. Homebrew: Öffne https://brew.sh, kopiere den Befehl von der Startseite, öffne das Programm „Terminal“, füge den Befehl ein und drücke Enter. Er fragt nach deinem Mac-Passwort.
2. Im selben Terminal danach diese Zeile eingeben und Enter drücken:

   ```bash
   brew install git gh gitleaks
   ```

   Das sind Git (speichert Änderungen), die GitHub-Anmeldung `gh` und gitleaks (findet versehentlich gespeicherte Passwörter).
3. Die Claude-App: Lade sie von https://claude.ai/download herunter und melde dich mit deinem Firmenkonto an. Gearbeitet wird im Bereich „Code“ der App.

## 3. Bei GitHub anmelden

Im Terminal:

```bash
gh auth login
```

Wähle „GitHub.com“, dann „HTTPS“, dann „Login with a web browser“. Es öffnet sich der Browser, dort bestätigst du mit deinem eigenen GitHub-Konto. Danach kann Claude in deinem Namen Branches und Pull Requests anlegen.

## 4. Das Repo holen

Leg im Finder einen Ordner `mokebo` in deinem Benutzerordner an. Öffne dann die Claude-App, Bereich „Code“, wähle diesen Ordner und schreib zum Beispiel:

> Hol mir das Repo mokebo/mokebo-ops-automations in diesen Ordner.

Claude lädt es herunter. Wechsle danach in der App in den neuen Ordner `mokebo-ops-automations`. Ab jetzt liest Claude dort die Regeln des Repos (`CLAUDE.md` und `AGENTS.md`) von selbst.

## 5. Erster Auftrag zum Üben

Schreib Claude im Repo-Ordner:

> Ich möchte üben. Leg ein Issue „Test von [dein Name]“ an, mach dazu einen Branch, trag im CHANGELOG eine Zeile „Test von [dein Name]“ ein und öffne einen Pull Request. Nicht mergen.

Claude erklärt dir jeden Schritt und gibt dir am Ende den Link zum Pull Request. Schau ihn dir auf GitHub an: Steht unten bei den Checks ein grüner Haken, hat alles geklappt. Danach sag Claude: „Schließ den Pull Request und das Issue wieder, das war nur ein Test.“

## Wenn etwas rot wird

Rot heißt: Die automatische Prüfung hat etwas gefunden. Das ist kein Unglück, sondern genau ihre Aufgabe.

- Sag Claude: „Die Prüfung im Pull Request ist rot, schau nach warum und behebe es.“ Claude liest die Meldung und repariert, was es reparieren kann.
- Steht in der Meldung etwas von Zugangsdaten oder einem Passwort: nicht weiterarbeiten, sofort den Org-Admins Bescheid geben.
- Kommt Claude nicht weiter, schreib den Org-Admins den Link zum Pull Request.

## Wenn etwas nicht klappt

| Meldung | Bedeutung | Was tun |
|---|---|---|
| `Permission denied` oder `403` beim Hochladen | Du bist noch nicht im Team „Alle“, oder das Repo gehört nicht zum Team | Org-Admins fragen |
| `gh: command not found` | Schritt 2 hat nicht geklappt | `brew install gh` noch einmal ausführen |
| `gitleaks: command not found` | gitleaks fehlt | `brew install gitleaks` |
| Claude kennt die Regeln des Repos nicht | Die App ist nicht im Repo-Ordner geöffnet | In der App den Ordner des Repos wählen |
