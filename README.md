ANFO – Kontaktverwaltung (Backend)
1. Projektbeschreibung

Das Backend der ANFO-Kontaktverwaltung wurde mit Strapi 5 entwickelt.

Es stellt die zentrale Schnittstelle zwischen dem Frontend und der Datenbank bereit.

Über eine REST-API können Kontaktdaten abgerufen, erstellt, bearbeitet und gelöscht werden.

Zusätzlich übernimmt Strapi die Benutzerverwaltung und Authentifizierung für die Login- und Registrierungsfunktion.

Das Backend wird unabhängig vom Frontend in einem eigenen GitHub-Repository verwaltet.

Zugehöriges Frontend:

https://github.com/RaByteCell/anfo-frontend-master

2. Verwendete Technologien
Technologie	Version laut package.json	Verwendung
Strapi	5.57.0	Backend und API
React	^18.0.0	Strapi-Verwaltungsoberfläche
React DOM	^18.0.0	Darstellung der Verwaltungsoberfläche
TypeScript	^5	Typisierung
Axios	^1.20.0	HTTP-Kommunikation
TanStack React Query	^5.104.1	Datenverwaltung
React Hook Form	^7.89.0	Formularverwaltung
Zod	^4.6.5	Datenvalidierung
better-sqlite3	^12.8.0	SQLite-Datenbanktreiber
Styled Components	^6.0.0	Gestaltung der Strapi-Oberfläche

Zusätzlich werden Strapi-Erweiterungen verwendet:

@strapi/plugin-users-permissions: Benutzerverwaltung und Authentifizierung.
@strapi/plugin-documentation: API-Dokumentation.
@strapi/plugin-cloud: Integration mit Strapi Cloud.

Die Angaben entsprechen den Versionsvorgaben in der package.json.

3. Voraussetzungen

Für die Entwicklung werden folgende Programme benötigt:

Visual Studio Code
Node.js
npm
Git

Das Backend erlaubt laut package.json Node.js-Versionen von 20 bis einschließlich 26.

Empfohlen wird eine passende LTS-Version, beispielsweise Node.js 24.

Versionen überprüfen:

bash
node -v
npm -v
git --version


Node.js herunterladen:

https://nodejs.org/

4. Installation
4.1 Repository herunterladen
bash
git clone https://github.com/RaByteCell/anfo-backend-master.git


In den Projektordner wechseln:

bash
cd anfo-backend-master


Projekt in Visual Studio Code öffnen:

bash
code .

4.2 Abhängigkeiten installieren

Die benötigten Pakete werden anhand der vorhandenen package-lock.json installiert:

bash
npm ci


Alternativ:

bash
npm install

5. Umgebungsvariablen konfigurieren

Strapi benötigt verschiedene Einstellungen für den Betrieb, beispielsweise für die Sicherheit, Datenbank und Authentifizierung.

Im Repository befindet sich eine Datei namens .env.example.

Diese dient als Vorlage für die eigene Konfigurationsdatei .env.

Unter Windows PowerShell:

powershell
Copy-Item .env.example .env


Unter macOS oder Linux:

bash
cp .env.example .env


Anschließend müssen die erforderlichen Werte in .env eingetragen werden.

Wichtig:

Die Datei .env enthält vertrauliche Einstellungen.
Sie darf nicht auf GitHub hochgeladen werden.
Erforderliche Schlüssel und Passwörter müssen selbst eingerichtet werden.
Für eine produktive Umgebung müssen sichere und individuelle Zugangsdaten verwendet werden.
6. Backend starten
Entwicklungsmodus

Das Backend wird mit folgendem Befehl gestartet:

bash
npm run develop


Dieser Modus aktiviert die automatische Aktualisierung während der Entwicklung.

Das Strapi-Verwaltungsfenster ist standardmäßig erreichbar unter:

http://localhost:1337/admin

Dort kann das Administrator-Konto erstellt und die Verwaltung des Backends vorgenommen werden.

Produktionsmodus

Für den Produktionsbetrieb wird zunächst das Backend erstellt:

bash
npm run build


Anschließend kann es gestartet werden:

bash
npm run start


Im Produktionsmodus ist die automatische Aktualisierung deaktiviert.

7. Datenverwaltung und API

Strapi stellt die REST-API bereit, über die das Frontend auf die gespeicherten Daten zugreift.

Kontaktverwaltung

Die Kontaktverwaltung verwendet folgenden API-Endpunkt:

text
/api/anfo-contacts


Über diesen Endpunkt können folgende Aktionen ausgeführt werden:

Aktion	HTTP-Methode	Beschreibung
Kontakte abrufen	GET	Alle Kontakte laden
Kontakt erstellen	POST	Neuen Kontakt speichern
Kontakt bearbeiten	PUT	Bestehenden Kontakt aktualisieren
Kontakt löschen	DELETE	Kontakt entfernen

Beim Bearbeiten und Löschen wird die jeweilige documentId verwendet.

Datenübertragung

Das Frontend sendet und empfängt die Daten über HTTP-Anfragen.

Die Kommunikation erfolgt über Axios.

Strapi übernimmt dabei die Verarbeitung der Anfragen und die Speicherung der Daten.

8. Benutzerverwaltung und Authentifizierung

Für die Benutzerverwaltung wird das Strapi-Plugin users-permissions verwendet.

Es stellt die Funktionen zur Registrierung und Anmeldung bereit.

Die Benutzer können sich über das Frontend registrieren und anschließend mit ihren Zugangsdaten anmelden.

Die Authentifizierung wird über die entsprechenden Strapi-Endpunkte abgewickelt.

Die erforderlichen Benutzerrechte und Rollen müssen in Strapi entsprechend eingerichtet werden.

Sicherheitshinweis: Schreib- und Löschzugriffe auf Kontaktdaten dürfen nicht ungeschützt öffentlich zugänglich sein. Die Berechtigungen müssen passend zum gewünschten Zugriffskonzept eingerichtet werden.

9. Projektstruktur
text
anfo-backend-master/
│
├── config/
│   ├── database.ts
│   ├── server.ts
│   └── ...
│
├── database/
│   └── migrations/
│
├── public/
│
├── src/
│   ├── api/
│   │   └── ...
│   │
│   ├── extensions/
│   └── ...
│
├── types/
│   └── generated/
│
├── .env.example
├── .gitignore
├── package.json
├── package-lock.json
└── tsconfig.json


Die wichtigsten Ordner:

Ordner	Aufgabe
config/	Einstellungen für Strapi, Server und Datenbank
database/	Datenbankmigrationen
public/	Öffentlich verfügbare Dateien
src/api/	API-Endpunkte, Controller und Datenmodelle
src/extensions/	Erweiterungen und Anpassungen
types/generated/	Automatisch erzeugte TypeScript-Typen
10. Wichtige Hinweise
Verbindung zum Frontend

Das Frontend verwendet standardmäßig folgende API-Adresse:

text
http://localhost:1337/api


Diese wird im Frontend über die Umgebungsvariable NEXT_PUBLIC_API_URL festgelegt.

Falls das Frontend und Backend auf unterschiedlichen Servern betrieben werden, müssen die entsprechenden API-Adressen und CORS-Einstellungen angepasst werden.

API-Berechtigungen

Die Berechtigungen werden über die Strapi-Verwaltungsoberfläche eingerichtet.

Dabei sollte darauf geachtet werden, dass:

Nur notwendige API-Zugriffe freigegeben werden.
Benutzerrechte passend zur Anwendung eingerichtet sind.
Änderungen und Löschungen nur durch berechtigte Benutzer erfolgen.
Vertrauliche Daten nicht öffentlich zugänglich sind.
Datenbank

In den Abhängigkeiten ist better-sqlite3 als Datenbanktreiber hinterlegt.

Die tatsächliche Datenbankkonfiguration wird über die Backend-Konfiguration und die Umgebungsvariablen festgelegt.

Vor Änderungen an der Datenbank sollten Sicherungen erstellt werden.

Strapi-Updates

Für die Aktualisierung von Strapi sind folgende Skripte vorhanden:

Update vorbereiten und prüfen:

bash
npm run upgrade:dry


Strapi aktualisieren:

bash
npm run upgrade


Vor jedem Update sollte eine Sicherung der Datenbank und des Projekts erstellt werden.

11. Nützliche Befehle
Befehl	Aufgabe
npm install	Installiert Abhängigkeiten
npm ci	Installiert Abhängigkeiten anhand der Lockdatei
npm run develop	Startet Strapi im Entwicklungsmodus
npm run build	Erstellt den Produktions-Build
npm run start	Startet Strapi im Produktionsmodus
npm run console	Öffnet die Strapi-Konsole
npm run upgrade:dry	Prüft ein mögliches Strapi-Update
npm run upgrade	Führt das Strapi-Update aus
12. Weiterführende Dokumentation
Strapi: https://docs.strapi.io/
Strapi REST API: https://docs.strapi.io/cms/api/rest
Strapi Users & Permissions: https://docs.strapi.io/cms/features/users-permissions
Node.js: https://nodejs.org/
TypeScript: https://www.typescriptlang.org/docs/

Projekt: ANFO – Kontaktverwaltung
Backend: Strapi 5
Datenübertragung: REST-API
Copyright: © 2026
