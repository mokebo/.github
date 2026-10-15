# So arbeiten wir mit GitHub

Diese Regeln gelten für jedes Repo der Org mokebo, das keine eigene `CONTRIBUTING.md` hat.

## Asana und GitHub

Wünsche kommen wie bisher als Aufgabe in Asana an. Sobald etwas gebaut wird, läuft die Arbeit in GitHub weiter. Die Asana-Aufgabe und das GitHub-Issue verlinken aufeinander. Wer nur etwas braucht und nicht selbst baut, bleibt in Asana.

Jeder Bereich hat ein eigenes Repo, zum Beispiel eins für alle Ops-Checks. Neue Repos entstehen aus `mokebo-repo-vorlage` über „Use this template“.

## Ablauf einer Aufgabe

1. Den Wunsch als Aufgabe in Asana anlegen.
2. Wer baut, legt im passenden Repo ein Issue mit der Vorlage an und trägt den Asana-Link ein. In die Asana-Aufgabe kommt der Issue-Link als Kommentar.
3. Einen Branch anlegen, Name `<issue-nummer>-<kurzname>`, zum Beispiel `12-lieferzeit-check`.
4. Auf diesem Branch bauen. Claude pflegt dabei README-Status, Changelog und, wenn nötig, eine Entscheidung im Ordner `decisions/`.
5. Einen Pull Request mit der Vorlage öffnen und `Closes #12` hineinschreiben.
6. Die automatische Prüfung läuft von selbst. Die Checkliste im Pull Request wird ausgefüllt.
7. Wer gebaut hat, mergt. Das Issue schließt sich dadurch.
8. Merge heißt noch nicht live. Erst danach wird gezielt aktiviert. Im Pull Request steht, welche Version läuft, wer sie aktiviert hat und wie man sie stoppt. Die Asana-Aufgabe wird erst erledigt, wenn das vereinbarte Ziel erreicht ist.

Ist die Arbeit noch nicht fertig, steht im Issue ein Kommentar mit dem Stand, dem nächsten Schritt und den offenen Fragen. Wer weitermacht, liest dort nach.

## Regeln

- Nie direkt auf `main` arbeiten und nie `git push --force`.
- Ist eine Prüfung rot oder läuft sie noch, wird nicht gemergt. Eine Prüfung, die gar nicht gelaufen ist, gilt nicht als bestanden.
- Keine Zugangsdaten in Dateien. Im Code steht nur der Name des Credentials.
- Ändert ein Pull Request Daten bei Kunden, in Plenty, in Shopify oder bei Geldflüssen, bekommt er das Label `live-wirkung`. Vor dem Merge ist dann ein Gegencheck Pflicht: Dubletten, Summen und 3 Stichproben. Das Ergebnis steht im Pull Request. Eine zweite Person muss nicht zustimmen.
- Neue Repos haben keinen Auto-Sync auf `main`. Notizen gehen in den Pull Request oder als Kommentar ins Issue.

## Labels

| Label | Bedeutung |
|---|---|
| `typ:check` | neue Prüfaufgabe automatisieren |
| `typ:fehler` | etwas Bestehendes läuft falsch |
| `typ:idee` | noch nicht entschieden, ob gebaut wird |
| `laufzeit:n8n`, `laufzeit:apps-script`, `laufzeit:code` | wo es läuft, sobald das entschieden ist |
| `live-wirkung` | ändert Daten bei Kunden, in Plenty, Shopify oder Geldflüssen |

## Die automatische Prüfung

Jedes Repo ruft bei jedem Pull Request und bei jedem Push auf `main` die Prüfung `basis-pruefung.yml` aus diesem Repo auf. Sie sucht mit gitleaks nach Zugangsdaten im Code und in der ganzen Git-Historie. Außerdem prüft sie, ob in den ersten 10 Zeilen der `README.md` die Zeilen `**Zweck:**`, `**Verantwortlich:**` und `**Status:**` mit einem echten Wert stehen. Leere Werte und Platzhalter wie `<Name>` zählen nicht.

Die Prüfung sagt nur, dass keine Zugangsdaten gefunden wurden und die README einen Kopf hat. Ob eine Automation fachlich richtig rechnet, prüft sie nicht. Dafür braucht jeder Check eigene Tests.

Wird die Prüfung rot, steht der Grund im Pull Request unter „Checks“. Fehlt eine README-Zeile, reicht es, sie nachzutragen.

Findet gitleaks Zugangsdaten, genügt Löschen nicht, weil der Wert in der Git-Historie bleibt. Zuerst den Zugang beim jeweiligen Dienst sperren und neu anlegen und den Org-Admins Bescheid geben. Danach entweder den gesperrten Fund einzeln in der `.gitleaks.toml` als Ausnahme eintragen, mit Begründung, oder die Historie bereinigen. Eine Bereinigung braucht einen Force-Push und wird deshalb als eigener Vorfall mit den Org-Admins abgesprochen. Ganze Ordner werden nie ausgenommen.

Eine eigene `.gitleaks.toml` muss mit `[extend]` und `useDefault = true` beginnen. Ohne diese Zeilen ersetzt sie die eingebauten Regeln, und gitleaks findet fast nichts mehr.

Die Prüfung läuft auf GitHub und verbraucht Actions-Minuten des aufrufenden Repos. Im kostenlosen Tarif hat die Org 2.000 Minuten im Monat für private Repos.
