# Changelog

Ein Eintrag je Pull Request, neueste oben. Format:

`TT.MM.JJJJ: Was sich geändert hat. Warum. (#Issue-Nummer)`

19.11.2026: Die Formulare fragen jetzt die Spec ab. „Neue Automation“ hat neue Felder: Schreibt das irgendwohin, Endzustand je System, Abbruch mittendrin, zweiter Lauf direkt danach, Randfälle, Beispieldaten, Nachkontrolle. „Fachlich zuständig“ heißt jetzt „Fachperson und Vertretung“, mit dem Hinweis, dass die Fachperson die Spec vor dem Bau mit dem Kommentar „Spec frei“ freigibt. „Läuft falsch“ hat am Ende einen Abschnitt für den Fix mit denselben Fragen, nicht Pflicht für die meldende Person. Warum: Schritt 2 der Software-Fabrik (ADR 0007 in mokebo-ai, Entwurf in mokebo/mokebo-ai#32). Die Fragen kommen aus echten Pannen, etwa 42 doppelten Tickets nach einem Abbruch mittendrin. Gilt für alle Repos ohne eigene Vorlage. Pflichtfelder erzwingt GitHub in privaten Repos nicht. (#11)

14.11.2026: README aktualisiert (Stand, Hinweis auf `ci.yml`) und um den Abschnitt „Wenn die Prüfung kaputt ist“ ergänzt: Rückweg auf eine ältere feste Version. CONTRIBUTING verweist darauf. Die Prüfung selbst ist unverändert. Damit ein Repo, das wegen eines Prüfungsfehlers rot ist, ohne Rückfrage wieder grün wird. (#9)

04.11.2026: Bei Entwurfs-PRs prüft die Changelog-Prüfung nicht mehr, sie meldet nur einen Hinweis. Sobald der PR auf bereit steht, läuft sie neu und verlangt den Eintrag. Vorher war fast jeder neue Entwurf rot, weil der Eintrag laut Ablauf erst am Ende kommt. Repos brauchen dafür in ihrer ci.yml den Auslöser `ready_for_review`. (#7)

15.10.2026: EINRICHTEN.md nennt das Team „Alle“ statt „Team deines Bereichs“. Seit heute gibt es genau ein Team, alle Org-Mitglieder haben darüber Schreibrecht in den Bereichs-Repos. (#4)

15.10.2026: Neue Anleitung EINRICHTEN.md: Konto, Zwei-Faktor-Anmeldung, Installation, Anmeldung, erster Übungsauftrag und was bei Rot zu tun ist. Damit neue Leute ohne Entwickler-Erfahrung nicht an der Einrichtung hängen bleiben. (#4)

15.10.2026: Die Prüfung wird bei einem Pull Request rot, wenn `CHANGELOG.md` nicht geändert wurde. Ausweg für Kleinkram: ein Kästchen in der PR-Vorlage. Damit niemand selbst daran denken muss, festzuhalten, was gemacht wurde. (#2)

15.10.2026: Org-Vorlagen angelegt. Drei Issue-Formulare, PR-Vorlage, CONTRIBUTING, einfache Erklärung, zentrale Prüfung (gitleaks und README-Kopf). Einheitliche GitHub-Arbeitsweise für mokebo. (PR #1)
