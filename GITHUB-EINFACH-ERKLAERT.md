# GitHub einfach erklärt

Für alle, die keine Entwickler sind und trotzdem mit GitHub arbeiten. Du musst nichts davon auswendig können. Meistens macht Claude die Handgriffe, und du entscheidest.

## Die Wörter

| Wort | Was es heißt |
|---|---|
| Repo (Repository) | ein gemeinsamer Ordner bei GitHub. Er merkt sich jede Änderung, wer sie gemacht hat und wann. Jeder Bereich hat ein eigenes Repo, zum Beispiel eins für alle Ops-Checks. |
| main | die gültige Fassung in einem Repo. Was auf `main` liegt, gilt. Darauf arbeitet niemand direkt. |
| Branch | eine Arbeitskopie neben `main`. Du kannst darin ändern, was du willst, ohne dass die gültige Fassung kaputtgeht. Vergleichbar mit „Kopie von Dokument“ in Google Docs. Jeder Branch hat einen Namen, bei uns `<issue-nummer>-<kurzname>`, zum Beispiel `12-lieferzeit-check`. |
| Commit | ein Speicherpunkt mit einer kurzen Notiz, was geändert wurde. Ein Branch sammelt meist mehrere Commits. |
| Push | die Speicherpunkte von deinem Rechner zu GitHub hochladen. Vorher liegen sie nur auf deinem Rechner und sind weg, wenn er kaputtgeht. |
| Pull Request (kurz PR) | die Bitte „Bitte übernimm meinen Branch in `main`“. Der Pull Request ist auch der Ort, an dem man die Änderungen ansieht, die Prüfung abwartet und notiert, wie getestet wurde. |
| Merge Request | dasselbe wie ein Pull Request. GitHub sagt Pull Request, das Konkurrenzprodukt GitLab sagt Merge Request. Bei uns heißt es immer Pull Request. |
| Merge | der Klick, mit dem die Änderungen aus dem Branch in `main` übernommen werden. Danach gilt die neue Fassung. |
| Issue | eine Aufgabe in GitHub, ähnlich wie eine Asana-Aufgabe. Jede Arbeit beginnt mit einem Issue, damit klar ist, worum es geht. |
| Prüfung (auch CI oder Check) | ein kleines Programm, das bei jedem Pull Request von selbst läuft. Es sucht nach Passwörtern und Schlüsseln im Code und schaut, ob die README vollständig ist. Grün heißt bestanden, rot heißt nicht bestanden. |

## Der Weg einer Änderung in einem Bild

```text
main  ──────────────────────────●──────►   gültige Fassung
        \                      /
         ●───●───●  Branch  ───   Pull Request, Prüfung grün, Merge
         Commits
```

Du zweigst von `main` ab, arbeitest auf deinem Branch und speicherst Commits. Danach lädst du alles hoch (Push), öffnest einen Pull Request, wartest auf Grün und mergst.

## So arbeitest du mit Claude

Das ist der normale Weg. Du sagst Claude in einfachen Worten, was passieren soll. Claude tippt die Befehle.

1. Lege das Issue an oder sag Claude: „Leg im Repo mokebo-ops-automations ein Issue mit dem Formular Neue Automation an, für den Lieferzeit-Check.“
2. Sag: „Leg einen Branch für Issue 12 an und arbeite darauf.“
3. Baut zusammen, was gebaut werden soll. Claude speichert zwischendurch Commits.
4. Sag: „Push den Branch und öffne einen Pull Request.“
5. Öffne den Link zum Pull Request, den Claude dir gibt. Lies „Was“ und „Wie getestet“.
6. Warte, bis unten bei den Checks ein grüner Haken steht.
7. Klick auf den grünen Knopf „Merge pull request“ (manchmal heißt er „Squash and merge“) und dann auf „Confirm merge“.
8. Klick danach auf „Delete branch“. Die Arbeitskopie wird nicht mehr gebraucht, alles steckt jetzt in `main`.

Ist die Arbeit nicht fertig, sag Claude: „Schreib den Stand als Kommentar ins Issue.“ Morgen kann dann jemand anderes dort weitermachen.

## So arbeitest du ohne Claude, nur im Browser

Für kleine Textänderungen, zum Beispiel in einer README.

1. Öffne die Datei bei GitHub und klick oben rechts auf den Stift („Edit this file“).
2. Ändere den Text.
3. Klick auf „Commit changes…“.
4. Wähle „Create a new branch for this commit and start a pull request“. GitHub schlägt einen Namen vor, den du ändern kannst.
5. Klick auf „Propose changes“ und dann auf „Create pull request“.
6. Weiter wie oben ab Schritt 6: auf Grün warten, mergen, Branch löschen.

## Wenn etwas schiefgeht

### Die Prüfung ist rot

Nicht mergen. Klick im Pull Request bei den Checks auf „Details“, dort steht der Grund. Oder sag Claude: „Die Prüfung im Pull Request ist rot, schau nach warum.“

### GitHub meldet einen Konflikt

GitHub zeigt „This branch has conflicts“. Das heißt: Jemand hat in der Zwischenzeit dieselbe Stelle in `main` geändert. Sag Claude: „Im Pull Request gibt es einen Konflikt, bitte lösen.“ Nicht selbst raten.

### Es wurde etwas Falsches gemergt

Öffne den gemergten Pull Request und klick auf „Revert“. GitHub legt dann einen neuen Pull Request an, der die Änderung rückgängig macht. Den mergst du wie jeden anderen.

### Du hast versehentlich ein Passwort oder einen Schlüssel hochgeladen

Sofort beim jeweiligen Dienst sperren und den Org-Admins Bescheid geben. Löschen allein reicht nicht, weil GitHub sich jede alte Fassung merkt. Mehr dazu in `CONTRIBUTING.md`.

## Wichtig

Merge heißt noch nicht live. Eine Automation läuft erst, wenn sie danach bewusst eingeschaltet wird. Wer sie einschaltet und wie man sie stoppt, steht im Pull Request.
