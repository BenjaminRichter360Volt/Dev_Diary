
Dieses Dokument definiert technische Standards und Best Practices für die Softwareentwicklung im Team.

Ziel ist es, Codequalität, Wartbarkeit, Skalierbarkeit und Wissensaustausch sicherzustellen.

---
## 1. Git & Versionskontrolle

### Was ist Git und warum nutzen wir es?

Git ist ein Versionskontrollsystem – stellt euch vor wie Google Docs mit "Versionsgeschichte", nur für Code. Es hilft uns:

- Zusammenzuarbeiten, ohne uns gegenseitig den Code zu überschreiben

- Änderungen nachzuvollziehen (wer hat was wann geändert?)

- Fehler rückgängig zu machen, ohne alles neu zu schreiben

- Parallel an Features zu arbeiten, ohne Konflikte

### Branching Strategie

**Was sind Branches?** Branches sind wie verschiedene "Versionen" eures Projekts, die parallel existieren.

- **main**: Produktionsbranch – nur funktionierender, getesteter Code!

- **dev**: Entwicklungsbranch – hier wird integriert und getestet, bevor es live geht

- **Feature Branches**: z.B. `feature/login-system` – Ein Branch = Ein Feature

  
**Regeln:**

- Niemals direkt auf main arbeiten

- Feature Branches immer von dev abzweigen

- Branch-Namen sollten beschreibend sein

### Pull Requests (PRs)

Ein PR ist eine "Bitte", euren Code in einen anderen Branch zu übernehmen. Es ist auch eine Diskussion über euren Code!

- Jede Änderung erfolgt über einen PR

- PR Beschreibung: Was wurde geändert? Warum? Wie testen?

- Maximal 300–500 Zeilen pro PR

- Keine Selbst-Merges

- Mindestens einen Reviewer taggen

### Commit Konvention

Gute Commit-Messages sind wie ein Tagebuch eures Projekts.

- `feat:` – neues Feature

- `fix:` – Bugfix

- `refactor:` – Code-Umstrukturierung

- `test:` – Tests

- `docs:` – Dokumentation

- `chore:` – Build/Config

## 2. Codequalität & Standards

### Linting & Formatting

Linting prüft euren Code auf Fehler und Formatierung sorgt für einheitlichen Stil.

- Frontend: ESLint, Prettier

- Backend: StyleCop, Roslyn Analyzer, dotnet format

### Pre-Commit Hooks

Automatische Checks vor jedem Commit, z.B. mit Husky. Blockiert Commits bei Fehlern oder fehlgeschlagenen Tests.

## 3. Frontend Standards

### Framework

- React oder Next.js

- **Next.js, wenn Backend-Logik benötigt wird**


**Warum ist Next.js oft besser als React + Express?**

- Alles in einem Projekt: Frontend und Backend sind integriert, weniger Setup und weniger Fehlerquellen

- Automatisches Routing: Seiten und APIs werden automatisch erkannt, kein manuelles Routing nötig

- Server Side Rendering (SSR): Schnellere Ladezeiten und bessere SEO

- Einfaches Deployment: Ein Build, eine App – kein Zusammenschustern von zwei Projekten

- Gemeinsame Codebasis: Typen und Logik können zwischen Frontend und Backend geteilt werden

- Weniger DevOps-Aufwand: Weniger Konfiguration, weniger Infrastruktur

- Große Community, viele Beispiele und Plugins


**Gerade für Einsteiger** ist Next.js einfacher, weil man sich nicht um die Integration von Frontend und Backend kümmern muss und viele Best Practices schon "out of the box" bekommt.

### Sprache

- TypeScript verpflichtend (besser als JavaScript für Anfänger, da Fehler früh erkannt werden)

### Projektstruktur

- components/, hooks/, services/, api/, types/, interfaces/

### Namensgebung

- Pages: PascalCase + Page

- Komponenten: PascalCase

### Styling

- CSS Modules

- Struktur: css/Home/Home.module.css

### Logging

- TS: Winston

### Tests

- Unit: Jest

- E2E: Playwright oder Cypress

## 4. Backend Standards

### Frameworks

- C# ASP.NET Web API

- TypeScript Express / Encore

### Architektur

Clean / Onion Architecture:

- API Layer: Controller, Middleware

- Application Layer: Services, Business Logik, Interfaces

- Contract Layer: DTOs, Requests, Responses

### Namensgebung

- TS:

    - Wie im Frontend

- C#

    - PascalCase

    - Interfaces beginnen mit I

### Datenbank

- DbContext unter Data/

### Tests

- C#: XUnit

- TS: Jest

## 5. Testing Strategie

### Testpyramide

- Viele Unit Tests

- Integration Tests

- E2E Tests

### Coverage

- Mindestziel: 70–80%

- Neue Features immer getestet

## 6. Architektur Prinzipien

- SOLID: Schreibe Code, der leicht erweiterbar und testbar ist

- DRY: "Don't Repeat Yourself" – vermeide doppelten Code

- KISS: "Keep It Simple, Stupid" – halte es einfach

- YAGNI: "You Aren't Gonna Need It" – baue nur, was wirklich gebraucht wird

### Regeln

- Keine Business Logik in Controllern

- Keine API Calls direkt in der UI

- Dependency Injection überall

## 7. Dokumentation

### Projekt README

- Setup, Start, Tests, Architektur

### Code Dokumentation

- Öffentliche Methoden kommentieren

- Warum erklären, nicht was

## 8. DevOps & CI/CD

### CI Pipeline

- Lint

- Build

- Tests

### Environments

- Local, Dev, Staging, Prod

### Secrets

- Keine Secrets im Code

- Nutzung von GitHub Secrets, Key Vault

### Versioning

Semantic Versioning: MAJOR.MINOR.PATCH

## 9. Sicherheit

### Backend

- Input Validation

- JWT Auth

- Refresh Tokens

- Rate Limiting

- Keine sensiblen Logs

### Frontend

- Keine Secrets

- Keine sensiblen Daten im LocalStorage

## 10. Team Prozesse

### Definition of Done

Was bedeutet "fertig"? Ein Feature ist erst dann wirklich fertig, wenn:

- Der PR gemerged ist (also im Hauptcode gelandet)

- Es automatisierte Tests gibt, die das Feature prüfen

- Die Dokumentation (README, Kommentare) aktualisiert ist

- Das Feature auf der Entwicklungsumgebung (Dev) läuft

**Warum ist das wichtig?**

So stellen wir sicher, dass nichts vergessen wird und alle wissen, was "fertig" bedeutet.

### Wissensverteilung

Im Team lernen alle voneinander. Das geht am besten so:

- **Pair Programming:** Zwei Leute arbeiten gemeinsam am Code, einer tippt, der andere denkt mit

- **Tech Talks:** Kurze Präsentationen zu neuen Tools, Methoden oder Erfahrungen

- **Brown Bag Sessions:** Gemeinsames Mittagessen mit lockeren Technik-Themen

**Tipp:** Niemand muss alles wissen! Fragen ist ausdrücklich erwünscht.

### Tech Debt

"Technische Schulden" sind Dinge, die wir später verbessern müssen (z.B. unsauberer Code, fehlende Tests).

- Immer im Board (z.B. Jira, Trello) als eigene Tickets tracken

- Keine TODO-Kommentare im Code lassen – sonst gehen sie verloren

**Warum?** So behalten wir den Überblick und können gezielt aufräumen.

## 11. Anti Patterns (No-Gos)

Hier sind typische Fehler, die wir vermeiden wollen:

- **God Components:** Riesen-Komponenten, die alles machen – schwer zu verstehen und zu testen

- **1000+ Zeilen Klassen:** Zu viel Verantwortung, lieber aufteilen

- **Business Logik in UI:** Logik gehört in Services, nicht direkt in die Oberfläche

- **Copy-Paste Code:** Lieber wiederverwenden als kopieren

- **Hardcodierte URLs:** URLs und Konfiguration gehören in Settings/Env-Files

- **console.log in Prod:** Debug-Ausgaben dürfen nicht in die Produktion

**Warum?** Diese Fehler machen den Code schwer wartbar und fehleranfällig.

## 12. Reifegrad Modell

Das Reifegrad-Modell zeigt, wie "professionell" unser Team arbeitet:

### Level 1 – Chaos

- Jeder macht, was er will

- Keine Standards, keine Reviews

- Viele Fehler, wenig Übersicht

### Level 2 – Basic

- Git Flow wird genutzt

- Linting und Unit Tests sind Standard

- Erste Regeln und Prozesse entstehen

### Level 3 – Professional

- Architektur ist klar (z.B. Clean Architecture)

- CI/CD Pipelines automatisieren Build und Tests

- Code Reviews sind Pflicht

### Level 4 – High Performance

- Monitoring und Tracing für Fehler und Performance

- Feature Flags für kontrollierte Releases

- Zero Downtime Deployments: Updates ohne Ausfall

**Ziel:** Schritt für Schritt von Chaos zu High Performance – jeder kann dazu beitragen!

## Zusätzliche Tipps fürs Team:

- Fragt immer nach, wenn ihr etwas nicht versteht – niemand weiß alles!

- Nutzt Online-Ressourcen (z.B. Stack Overflow, Dokumentationen)

- Macht kleine, häufige Commits statt seltener, großer

- Schreibt Tests für euren eigenen Code – das hilft euch, Fehler zu finden

- Dokumentiert nicht nur den Code, sondern auch Entscheidungen (z.B. im README)

- Nutzt Pair Programming, um voneinander zu lernen

- Habt keine Angst vor Fehlern – sie sind normal und helfen beim Lernen

- Reflektiert regelmäßig: Was lief gut? Was kann besser werden?

## Projektstart mit Templates

Wenn ein neues Projekt begonnen wird, MUSS eines der bereitgestellten GitHub-Projekt-Templates verwendet werden (z.B. für React, Next.js, Express, ASP.NET API).


**Warum?**

- Einheitliche Struktur und Best Practices von Anfang an

- Alle wichtigen Tools (Linting, Testing, CI, Beispiel-Code) sind schon integriert

- Weniger Fehlerquellen und schnelleres Onboarding

**Wie?**

- Im GitHub-Repository-Bereich das gewünschte Template auswählen („Use this template“)

- Neues Repository daraus erstellen

- Erst dann mit der eigentlichen Entwicklung starten

**Hinweis:**

Die Nutzung der Templates ist Pflicht, damit alle Projekte im Team auf dem gleichen Qualitätsstandard starten.