---
title: Design Decisions
nav_order: 3
---

{: .no_toc }
# Design Decisions

<details open markdown="block">
{: .text-delta }
<summary>Table of contents</summary>
+ ToC
{: toc }
</details>

## 01: [CSS Stil]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Für das Projekt *Nachbarsharing* benötigen wir CSS, HTML und wahrscheinlich JavaScript, um die Webanwendung zu gestalten. Da das Ziel der Plattform darin besteht, dass Nachbarn Werkzeuge und Alltagsgegenstände miteinander teilen können, muss das Design benutzerfreundlich und einfach zugänglich sein. Es gibt jedoch wenig Zeit, um die gesamte Seite individuell zu gestalten.

### Entscheidung

Wir haben beschlossen, Bootstrap als Framework zu verwenden, um das Frontend der Anwendung zu erstellen. Bootstrap ermöglicht eine schnellere Entwicklung, insbesondere für responsive Layouts, und bietet ein vorgefertigtes Gittersystem, das uns bei der Anpassung an verschiedene Bildschirmgrößen hilft. Darüber hinaus haben wir einige individuelle CSS-Stile hinzugefügt, um spezifische Designakzente zu setzen, die zu unserer Benutzeroberfläche passen.

### Betrachtete Optionen

|  | Pro | Contra |
| --- | --- | --- |
| **Eigenes CSS** | ✔️ Volle Kontrolle über das Styling <br> ✔️ Einzigartiges, individuelles Design | ❌ Zeitaufwändig |
| **Bootstrap** | ✔️ Schnelle Entwicklung <br> ✔️ Weniger Aufwand <br> ✔️ Geeignet für CSS-Anfänger | ❌ Weniger Flexibilität <br> ❌ Zusätzliche Bibliotheken können die Ladezeit erhöhen |

---

## 02: [Datenbank]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Für die Verwaltung von Nutzern, geteilten Gegenständen und Transaktionen benötigen wir eine Datenbank. Da es sich um eine Plattform handelt, bei der viele Daten gespeichert und verarbeitet werden müssen, ist es wichtig, eine zuverlässige und einfach zu verwaltende Datenbanklösung zu finden.

### Entscheidung

Wir haben uns entschieden, SQLite in Kombination mit Flask-SQLAlchemy zu verwenden. Diese Wahl bietet uns eine einfache Integration in unser Flask-Projekt, ermöglicht ORM-Funktionalitäten, und ist eine robuste und leicht zu handhabende Lösung für kleine bis mittelgroße Projekte.

### Betrachtete Optionen

|  | Pro | Contra |
| --- | --- | --- |
| **SQLite** | ✔️ Einfach zu verwenden <br> ✔️ Lokale Speicherung <br> ✔️ Gute Integration mit Flask | ❌ Weniger geeignet für große, skalierbare Anwendungen |
| **MySQL/PostgreSQL** | ✔️ Skalierbar <br> ✔️ Besser geeignet für große Datenmengen | ❌ Komplexere Einrichtung und Wartung für kleine Projekte |

---

## 03: [Benutzerverwaltung]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Da es sich bei Nachbarsharing um eine Plattform mit mehreren Benutzern handelt, benötigen wir eine sichere und einfache Methode, um Anmeldungen, Authentifizierungen und Zugriffsberechtigungen zu verwalten. Außerdem müssen wir sicherstellen, dass nur authentifizierte Benutzer Zugriff auf die Plattform und deren Funktionen haben.

### Entscheidung

Wir haben Flask-Login für die Benutzerverwaltung ausgewählt. Diese Erweiterung bietet eine einfache und sichere Möglichkeit, Nutzeranmeldungen und Sitzungen zu verwalten. Es ist leicht in Flask integrierbar und bietet alle grundlegenden Funktionen für Authentifizierung, Sitzungsverwaltung und Schutz von Routen.

### Betrachtete Optionen

|  | Pro | Contra |
| --- | --- | --- |
| **Flask-Login** | ✔️ Einfache Integration <br> ✔️ Geeignet für kleine bis mittelgroße Anwendungen <br> ✔️ Bietet alle nötigen Authentifizierungsfunktionen | ❌ Für größere und komplexere Anwendungen könnte ein eigenständiges Authentifizierungsservice sinnvoller sein |
| **OAuth** | ✔️ Weit verbreitet <br> ✔️ Geeignet für große Anwendungen | ❌ Überkompliziert für kleine Projekte |

---

## 04: [Formularverwaltung mit Flask-WTF]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Für die Plattform sind viele Formulare notwendig, beispielsweise zur Registrierung, Anmeldung oder zum Hinzufügen neuer Gegenstände. Um den Entwicklungsaufwand zu reduzieren und die Validierung der Benutzereingaben zu erleichtern, benötigen wir eine Lösung, die die Formularerstellung und -verwaltung in Flask vereinfacht.

### Entscheidung

Wir verwenden Flask-WTF zur Verwaltung von Formularen. Diese Erweiterung ermöglicht uns eine einfache und übersichtliche Verwaltung von Formularen, inklusive der Validierung von Eingaben und des CSRF-Schutzes. Da wir bereits Erfahrung mit Flask-WTF haben, beschleunigt dies den Entwicklungsprozess.

### Betrachtete Optionen

| Kriterium | Flask-WTF | Reine WTForms | Manuell mit HTML |
|------------------|-------------------------------------------------|----------------------------------------|-------------------------------------------|
| Benutzerfreundlichkeit | ✔️ Hoch: Integriert mit Flask. Keine Einrichtung erforderlich | ❌ Mittel: Einrichtung erforderlich | ❌ Niedrig: Manuelle Einrichtung erforderlich |
| Validierung | ✔️ Eingebaute Validatoren, CSRF-Schutz | ✔️ Validatoren sind integriert | ❌ Manuelle Validierung erforderlich |
| Sicherheit | ✔️ CSRF-Schutz standardmäßig integriert | ❌ Kein CSRF-Schutz. Einrichtung erforderlich | ❌ Manueller CSRF-Schutz erforderlich |
| Flexibilität | ✔️ Hoch: Sehr flexibel und anpassbar | ✔️ Hoch: Anpassbar | ✔️ Hoch: Volle Kontrolle |
| Lernkurve | ✔️ Niedrig: Gute Dokumentation, Flask-Integration | ❌ Mittel: Einrichtung erforderlich | ❌ Hoch: Kenntnisse von HTML und Validierungslogik erforderlich |

---

## 05: [Zahlungsintegration mit PayPal]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Für einige Gegenstände auf der Plattform könnten zusätzliche Kosten für die Nutzung anfallen. Daher müssen wir eine Möglichkeit zur Integration einer Zahlungsmethode schaffen, die sowohl sicher als auch weit verbreitet ist.

### Entscheidung

Wir haben PayPal als Zahlungs-API ausgewählt, da es eine einfache Integration und große Akzeptanz bei Nutzern bietet. Zusätzlich bietet PayPal robuste Sicherheitsfunktionen und ist in Deutschland weit verbreitet, was es zur idealen Lösung für unser Projekt macht.

### Betrachtete Optionen

|  | PayPal | Kredit-/Debitkarten | Klarna |
| --- | --- | --- | --- |
| **Benutzerfreundlichkeit** | ✔️ Hoch: Weit verbreitet und einfach zu nutzen | ✔️ Hoch: Sehr verbreitet | ✔️ Bequem, besonders mit Rechnungskauf |
| **Sicherheit** | ✔️ Hoch: Robuste Sicherheitsmaßnahmen | ❌ Mittel: Risiko von Datenmissbrauch | ✔️ Hoch: Klarna übernimmt das Zahlungsausfallrisiko |
| **Integration** | ✔️ Einfach: Umfangreiche APIs und SDKs verfügbar | ✔️ Hoch: Direkte Abwicklung | ❌ Komplexere Integration erforderlich |

---

## 06: [Task-Scheduling mit Flask_apscheduler]

### Meta

Status: **Entschieden**

Aktualisiert: 04-Okt-2024

### Problemstellung

Um die Verfügbarkeit von Gegenständen zu aktualisieren oder Erinnerungen zu senden, müssen einige Aufgaben automatisch im Hintergrund ausgeführt werden. Diese Aufgaben sollten geplant und effizient ausgeführt werden, ohne die Performance der Anwendung zu beeinträchtigen.

### Entscheidung

Wir haben uns für die Nutzung von `flask_apscheduler` entschieden. Diese Erweiterung bietet die Möglichkeit, Aufgaben wie Cron-Jobs zu planen und nahtlos in Flask zu integrieren. Der ressourcenschonende Ansatz von Cron-Triggern macht es zur idealen Lösung für unsere geplanten Hintergrundaufgaben.

### Betrachtete Optionen

|  | flask_apscheduler | Cron-Jobs auf dem Server | Cloud-basierter Task-Scheduler |
| --- | --- | --- | --- |
| **Vorteile** | ✔️ Integration in Flask, einfache Konfiguration | ✔️ Stabil, systemintegriert | ✔️ Skalierbar, gute Integration |
| **Nachteile** | ❌ Abhängigkeit von der Anwendung | ❌ Keine direkte Integration in Flask | ❌ Kosten, erfordert zusätzliche Infrastruktur |

---
