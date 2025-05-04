# Svelte Projekt WMC

Um fortgeschrittene Konzepte der Webentwicklung mit Svelte zu erlernen, soll als Abschluss dieses Semesters ein Projekt mit Svelte umgesetzt werden.

## Allgemeine Informationen

Dieses Projekt ist eine **Einzelarbeit** und es kann zwischen drei verschiedenen Projektideen gewählt oder auch eine eigenen Projektidee umgesetzt werden. Die Abgabe muss in euem Projekt-Reposirtory, das euch über GitHub Classroom zur Verfügung gestellt wird, **bis zum 11.06.2025 um 23:59 Uhr** erfolgen. Nutzt die gemeinsamen WMC Termine, um Fragen zu stellen und um Feedback zu erhalten.

### Beurteilung

Folgende Punkte werden bei der Beurteilung berücksichtigt:

- **Anforderungen**: Es müssen alle Anforderungen, die in der Beschreibung der ausgewählten Projektidee enthalten sind, erfüllt werden. Für ein *Gut* und *Sehr Gut* müssen die Anforderungen noch um zusätzliche Features erweitert werden.
- **Architektur**: Die Webanwendung muss modular aufgebaut sein. Es sollen verschiedene Komponenten erstellt werden, die sinnvoll miteinander kommunizieren.
- **Codequalität**: Der Code muss gut strukturiert und lesbar sein.
- **Performance**: Die Webanwendung muss performant sein. Es sollen keine unnötigen Daten geladen werden.
- **Design und Usability**: Das Design der Anwendung muss responsiv und ansprechend sein. Die Anwendung muss auf verschiedenen Endgeräten (Desktop, Tablet, Smartphone) gut aussehen und funktionieren, daher muss mit Tailwind CSS gearbeitet werden. Zudem muss die Bedienung der Webanwendung intuitiv und benutzerfreundlich sein. Eine entsprechende Fehlerbehandlung von möglichen Problemen, die auftreten können, muss implementiert werden.
- **Regelmäßige und sprechende Commits**: Es wird erwartet, dass ihr regelmäßig und sprechende Commits in eurem Repository macht. Wir können euch im Unterricht jederzeit Fragen zum aktuelle Stand eures Projektes stellen. Ihr solltet in der Lage sein, den aktuellen Stand eures Projektes zu erklären und zu begründen, warum ihr euch für bestimmte Lösungen entschieden habt.
- **Deployment**: Für ein *Sehr Gut* muss die Webanwendung auf einem Server deployed werden. Hierfür kann zB [Github Pages](https://pages.github.com/) verwendet werden. Der Link zur Webanwendung muss in einer Readme.md bei der Abgabe im Repository zu finden sein.

### Grundfunktionalität aller Projektideen

Alle Projektideen sollen folgende Grundfunktionalität besitzen, die in mindestens drei Seiten umgesetzt werden soll:

- Startseite mit einer Übersicht (zB. Übersicht aller Produkte, Rezepte)
- Detailseite mit weiteren Informationen zu einem einzelnen Element (zB. Detailseite eines Produkts, eines Rezepts)
- Suchfunktion, um bestimmte Elemente zu finden
- Speichern von Daten im Local Storage (zB. Warenkorb mit Produkte, den Favoriten bei Rezepten)
- Nutzung externer APIs
- Nutzung von Tailwind CSS für das Design der Anwendung
- Fehlerbehandlung (zB. wenn keine Daten gefunden werden, wenn die API nicht erreichbar ist oder ungülstige Werte eingegeben werden)

\pagebreak

## Projektidee 1: Wetter Dashboard

Die Wetter-App zeigt aktuelle Wetterdaten für beliebige Städte an und bietet zudem eine 3-Tage-Vorhersage. Für die Wetterdaten sollte eine API wie zB [Open-Meteo](https://open-meteo.com/) verwendet werden.

### Funktionalitäten

**Für eine gesuchte Stadt** gibt es eine Anzeige der **aktuellen Wetterdaten** wie Temperatur, Luftfeuchtigkeit, Regenmenge und Windgeschwindigkeit. Bei der Anzeige soll auch der Ort der Wetterstation, das Datum und die Uhrzeit, wann der aktuelle Wert gemessen wurde, sichtbar sein. Je nach Wetterzustand soll sich das Design anpassen.

Neben den aktuellen Wetterdaten soll es auch möglich sein, **das Wetter für die nächsten 3 Tage** anzuzeigen. Dabei soll für jeden der drei zukünftigen Tage der Wochentag, die Tageshöchst- und -tiefsttemperatur und die Niederschlagsmenge angezeigt werden.

Nutzer:innen der App sollen die Möglichkeit haben, **ihre Lieblingsorte** zu speichern. Die Orte sollen im Local Storage gespeichert und in einer eigenen Ansicht angezeigt werden. Beim Start der App sollen die gespeicherten Orte automatisch geladen werden. Die gespeicherten Orte sollen auch wieder gelöscht werden können. Wenn noch keine Orte gespeichert sind, sollen die 5 nächsten Wetterstationen zu den Koordinaten aus dem Webbrowser angezeigt werden.

### Technische Anforderungen

Die Anwendung sollte modular aufgebaut sein und verschiedene Svelte-Komponenten enthalten, die sinnvoll miteinander kommunizieren.

Beachte bei der Implementierung, dass die API effizient genutzt wird, also möglichst nur Daten abgerufen werden, die auch wirklich benötigt werden.

In der Anwendung soll es auch eine entsprechende **Fehlerbehandlung** geben, die dem Nutzenden anzeigt, wenn keine Daten gefunden werden, wenn die API nicht erreichbar ist oder ungültige Werte eingegeben werden.

Nutze für das Design der Anwendung **Tailwind CSS**. Die Anwendung soll responsiv sein und auf verschiedenen Endgeräten gut aussehen. Die Navigation soll intuitiv und benutzerfreundlich sein.

Für ein *Sehr Gut* muss die Webanwendung auf einem Server deployed werden. Hierfür kann zB [Github Pages](https://pages.github.com/) verwendet werden. Der Link zur Webanwendung muss in einer Readme.md bei der Abgabe im Repository zu finden sein.

## Projektidee 2: Cocktail-Rezeptverwaltung

Die Anwendung zeigt eine Sammlung von Cocktailrezepten, erlaubt das Durchsuchen und Favorisieren von Cocktails und bietet Detailinformationen zu jedem Drink. Die Rezepte sollten von einer API wie [TheCocktailDB](https://www.thecocktaildb.com/) abgerufen werden.

### Funktionalitäten

Auf der Startseite soll eine **Übersicht verschiedener Cocktails** angezeigt werden. Die Auswahl der Cocktails kann zufällig erfolgen (zB die Cocktails der Woche). Zu jedem Cocktail soll ein Bild, der Name und die Kategorie angezeigt werden.

Die Ansicht soll auch eine **Suchfunktion** enthalten, um nach bestimmten Cocktails zu suchen. Dabei soll man auch nach Kategorien filtern können. Die Suchergebnisse sollen in einer eigenen Ansicht gezeigt werden.

Es soll zudem eine Detailseite für jeden Cocktail geben, die bei Klick auf den Cocktail in der Übersicht angezeigt wird. Auf dieser Detailseite sollen neben den Daten aus der Übersicht die Zutaten mit Mengenangaben und die Zubereitungsschritte des Cocktails angezeigt werden.

Nutzer:innen der App sollen die Möglichkeit haben, **ihre Lieblingscocktails** zu speichern. Diese Cocktails sollen im Local Storage gespeichert und in einer eigenen Ansicht angezeigt werden. Es soll in dieser Ansicht auch eine Möglichkeit geben, die Cocktails zu löschen.

### Technische Anforderungen

Die Anwendung sollte modular aufgebaut sein und verschiedene Svelte-Komponenten enthalten, die sinnvoll miteinander kommunizieren.

Beachte bei der Implementierung, dass die API effizient genutzt wird, also möglichst nur Daten abgerufen werden, die auch wirklich benötigt werden.

In der Anwendung soll es auch eine entsprechende **Fehlerbehandlung** geben, die dem Nutzenden anzeigt, wenn keine Daten gefunden werden, wenn die API nicht erreichbar ist oder ungültige Werte eingegeben werden.

Nutze für das Design der Anwendung **Tailwind CSS**. Die Anwendung soll responsiv sein und auf verschiedenen Endgeräten gut aussehen. Die Navigation soll intuitiv und benutzerfreundlich sein.

Für ein *Sehr Gut* muss die Webanwendung auf einem Server deployed werden. Hierfür kann zB [Github Pages](https://pages.github.com/) verwendet werden. Der Link zur Webanwendung muss in einer Readme.md bei der Abgabe im Repository zu finden sein.

## Projektidee 3: Webshop

Die Anwendung zeigt eine Auswahl an Produkten, die in einem Webshop verkauft werden und in einen Warenkorb abgelegt werden können. Die Produkte sollten von einer API wie [Fake Store API](https://fakestoreapi.com/) abgerufen werden.

### Funktionalitäten

Auf der Startseite soll eine **Auswahl an Produkten** angezeigt werden. Zu jedem Produkt soll ein Bild, der Name, der Preis und eine Produktkategorie angezeigt werden. Die Produktkategorien sollen als Filter verwendet werden können.

Es soll zudem auch eine **Suchfunktion** enthalten sein, um nach bestimmten Produkten zu suchen. Die Suchergebnisse sollen in einer eigenen Ansicht angezeigt werden.

Wird ein Produkt ausgewählt, soll eine **Detailseite** angezeigt werden. Auf dieser Detailseite sollen neben den Daten aus der Übersicht auch eine Beschreibung des Produkts und die Möglichkeit, das Produkt in den Warenkorb zu legen, angezeigt werden.

Der **Warenkorb** soll in einer eigenen Ansicht angezeigt werden. Dort sollen alle Produkte aufgelistet werden, die in den Warenkorb gelegt wurden. Zudem soll es eine Möglichkeit geben, die Produkte aus dem Warenkorb zu entfernen. Die Produkte sollen im Local Storage gespeichert werden, damit sie auch nach einem Neuladen der Seite erhalten bleiben.

### Technische Anforderungen

Die Anwendung sollte modular aufgebaut sein und verschiedene Svelte-Komponenten enthalten, die sinnvoll miteinander kommunizieren.

Beachte bei der Implementierung, dass die API effizient genutzt wird, also möglichst nur Daten abgerufen werden, die auch wirklich benötigt werden.

In der Anwendung soll es auch eine entsprechende **Fehlerbehandlung** geben, die dem Nutzenden anzeigt, wenn keine Daten gefunden werden, wenn die API nicht erreichbar ist oder ungültige Werte eingegeben werden.

Nutze für das Design der Anwendung **Tailwind CSS**. Die Anwendung soll responsiv sein und auf verschiedenen Endgeräten gut aussehen. Die Navigation soll intuitiv und benutzerfreundlich sein.

Für ein *Sehr Gut* muss die Webanwendung auf einem Server deployed werden. Hierfür kann zB [Github Pages](https://pages.github.com/) verwendet werden. Der Link zur Webanwendung muss in einer Readme.md bei der Abgabe im Repository zu finden sein.
