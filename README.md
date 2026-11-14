# .github

**Zweck:** Gemeinsame Vorlagen und Regeln für alle Repos der Org mokebo
**Verantwortlich:** Org-Admins von mokebo
**Status:** aktiv, Stand 14.11.2026
**Läuft live:** die Prüfung `basis-pruefung.yml`. Andere Repos rufen sie bei jedem Pull Request und jedem Push auf `main` auf, dieses Repo ruft sie über `ci.yml` bei sich selbst auf

Dieses Repo ist öffentlich. Hier liegen nur Vorlagen und die Prüfung, keine internen Daten.

| Datei | Wofür |
|---|---|
| `EINRICHTEN.md` | Was man einmal am eigenen Rechner einrichtet, bevor es losgeht |
| `GITHUB-EINFACH-ERKLAERT.md` | Branch, Pull Request, Merge und Co. für Nicht-Entwickler |
| `CONTRIBUTING.md` | So arbeiten wir mit GitHub |
| `CHANGELOG.md` | Was sich in diesem Repo geändert hat |
| `.github/ISSUE_TEMPLATE/` | drei Issue-Formulare: Neue Automation, Läuft falsch, Idee |
| `.github/pull_request_template.md` | Vorlage für jeden Pull Request |
| `.github/workflows/basis-pruefung.yml` | Prüfung, die jedes Repo aufruft |
| `.github/workflows/ci.yml` | Ruft die Prüfung für dieses Repo selbst auf |

GitHub nimmt die Vorlagen automatisch für jedes Repo der Org, das keine eigenen hat.

## Wenn die Prüfung kaputt ist

Jedes Repo ruft die Prüfung mit einer festen Version auf. Das ist die lange Kennung hinter dem `@` in der Datei `.github/workflows/ci.yml` des Repos, zum Beispiel `basis-pruefung.yml@52c7ef48…`. Eine Änderung hier wirkt deshalb erst, wenn ein Repo die neue Kennung einträgt. Wer die neue Kennung in den einzelnen Repos nachträgt, ist noch nicht festgelegt.

Wird ein Repo rot, obwohl nichts falsch ist, und der Grund liegt in der Prüfung selbst, stellt man dieses Repo auf die vorige Version zurück. Zuerst in der roten Prüfung auf „Details“ klicken und lesen, ob wirklich ein Fehler der Prüfung vorliegt. Meldet gitleaks Zugangsdaten oder fehlt eine README-Zeile, ist die Prüfung in Ordnung und es wird nicht zurückgestellt.

1. Die vorige Kennung finden: in diesem Repo die Datei `.github/workflows/basis-pruefung.yml` öffnen, oben rechts „History“ wählen. Gesucht ist die Änderung direkt vor der aktuellen. Ihre vollständige Kennung hat 40 Zeichen, die Kurzform reicht nicht.
2. Im betroffenen Repo `.github/workflows/ci.yml` öffnen und die Kennung nach dem `@` durch die vorige ersetzen. Sonst nichts ändern.
3. Als Pull Request einreichen. Wird die Prüfung dort wieder grün, ist die Ursache bestätigt.
4. Ein Issue in diesem Repo anlegen: welches Repo, welche Meldung, welche Kennung zurückgestellt wurde.

Ältere Versionen kennen neuere Regeln nicht. Die Version vom 04.11.2026 zum Beispiel überspringt die Changelog-Prüfung bei Entwurfs-Pull-Requests, die davor nicht.
