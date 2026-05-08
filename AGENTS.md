# Bauernskat - Agenten-Anweisungen

Dies ist ein HTML-basiertes Kartenspiel (Bauernskat) ohne Build-System oder externe Abhängigkeiten.

## Build/Lint/Test-Befehle

### Ausführung
```bash
# Spiel im Browser öffnen (einfachste Methode)
xdg-open Bauernskat0.15.html

# Oder mit einem lokalen Server (für korrekte Sound-Wiedergabe)
python3 -m http.server 8080
# Dann öffnen: http://localhost:8080/Bauernskat0.15.html
```

### Linting
Kein Linter konfiguriert. Empfohlene manuelle Checks:
- HTML-Validierung: Browser-Entwicklertools verwenden
- JavaScript-Syntax: Browser-Konsole auf Fehler prüfen

### Tests
Keine Tests vorhanden. Das Projekt hat kein Test-Framework.

## Projektstruktur

```
Bauernskat/
├── Bauernskat0.15.html    # Hauptdatei (HTML + CSS + JS)
├── readme.txt              # Sound-Datei-Benennung
├── info.txt                # Spielbeschreibung
├── Set01/                  # Kartenset 1 (PNG-Bilder)
├── Set02/                  # Kartenset 2 (PNG-Bilder)
├── sounds/                 # MP3-Sounddateien (optional)
└── Archiv/                 # Ältere Versionen
```

## Code-Stil-Richtlinien

### Sprache
- **Code-Kommentare**: Deutsch
- **UI-Texte**: Deutsch
- **Variablennamen**: Englisch (camelCase)
- **CSS-Klassennamen**: Englisch (kebab-case)

### JavaScript-Stil

#### Namenskonventionen
```javascript
// Klassen: PascalCase
class BauerskatGame { }

// Methoden: camelCase
playCard(card, isPlayer) { }
computerSelectTrump() { }

// Eigenschaften: camelCase
this.currentCardSet = 'Set01';
this.playerVisibleCards = [];

// Konstanten: camelCase (innerhalb von Objekten)
this.cardValues = { '7': 0, '10': 10, 'A': 11 };
this.suitValues = { 'Karo': 9, 'Herz': 10 };

// Private Methoden: kein Präfix (kein TypeScript)
getEffectiveSuit(card) { }
getTrumpOrder(card) { }
```

#### Variablen und Konstanten
- `const` für unveränderliche Referenzen
- `let` für veränderliche Variablen
- Kein `var` verwenden
- Objekte und Arrays mit `const` deklarieren

```javascript
const deck = [];
const firstCard = this.currentTrick[0];
let winner = 'player';
```

#### Funktionen und Methoden
- Arrow Functions für Callbacks und Event-Handler
- Klassische Function-Syntax für Klassenmethoden
- Frühe Returns verwenden

```javascript
// Callbacks
document.getElementById('cardSetSelect').addEventListener('change', (e) => {
    game.changeCardSet(e.target.value);
});

// Methode mit frühem Return
playSound(type) {
    if (!this.soundEnabled) return;
    // ...
}
```

#### String-Formatierung
- Template-Literale für Strings mit Variablen

```javascript
`url('./${this.currentCardSet}/${card.fileName}')`
`./sounds/${type}.mp3`
```

### CSS-Stil

#### Namenskonventionen
```css
/* Klassen: kebab-case */
.game-container { }
.trick-area { }
.card-played { }

/* BEM-ähnliche Struktur verwenden */
.modal { }
.modal-content { }
```

#### Farben und Werte
- Farbwerte als Hex oder rgba
- Einheiten: px für feste Größen, % für flexible Layouts
- Media Queries für Responsive Design

```css
background: rgba(0, 0, 0, 0.8);
color: #ffd700;
@media (max-width: 768px) { }
```

### HTML-Stil

#### Attribute-Reihenfolge
1. `id`
2. `class`
3. `style` (vermeiden, CSS-Klassen bevorzugen)
4. Event-Handler

```html
<div id="trumpModal" class="modal" style="display: none;">
<button onclick="newGame()">Neues Spiel</button>
```

#### Dokumentstruktur
- DOCTYPE-Definition
- `lang="de"` für deutsche Inhalte
- Viewport-Meta für Mobile-Unterstützung

## Architektur-Patterns

### Spielklasse
- Hauptspiellogik in einer Klasse `BauerskatGame`
- Status-Management über Instanzeigenschaften
- Trennung von Logik und Rendering

```javascript
class BauerskatGame {
    constructor() {
        // Initialisierung
        this.reset();
    }
    
    reset() {
        // Zurücksetzen des Spielzustands
    }
    
    // Render-Methoden
    renderCards() { }
    renderTrick() { }
    
    // Spiellogik-Methoden
    playCard(card, isPlayer) { }
    evaluateTrick() { }
}
```

### Event-Handling
- Inline-Handler für einfache Aktionen
- addEventListener für komplexere Interaktionen

```javascript
// Inline (für globale Funktionen)
<button onclick="newGame()">

// addEventListener (für Klassen-Methoden)
cardElement.addEventListener('click', () => {
    this.playCard(card, true);
});
```

## Dateinamen-Konventionen

### Kartenset-Bilder
Format: `{Farbe}-{Wert}.png`
```
Herz-A.png, Herz-10.png, Herz-Dame.png
Pik-Bauer.png, Kreuz-Koenig.png
Rueckseite.png (Rückseite)
```

### Sound-Dateien
Format: `{typ}.mp3` oder `{typ}_{variante}.mp3`
```
cardPlay.mp3, trump.mp3, win.mp3, lose.mp3
computerWinsTrick_male.mp3, computerWinsTrick_female.mp3
```

## Fehlerbehandlung

- Console-Logging für Debugging
- Try-Catch für Audio-Wiedergabe
- Frühzeitige Returns für Validierung

```javascript
try {
    const audio = new Audio(`./sounds/${type}.mp3`);
    audio.play().catch(e => {
        console.log(`Sound konnte nicht abgespielt werden: ${type}.mp3`);
    });
} catch (e) {
    console.error("Audio-Fehler:", e);
}

// Frühe Validierung
if (this.gameOver) return;
if (possibleCards.length === 0) { console.error("..."); return; }
```

## Wichtige Hinweise

1. **Keine externen Abhängigkeiten**: Das Spiel funktioniert vollständig ohne npm, yarn oder CDN-Links
2. **Mobile-First**: Responsive Design mit Media Queries für verschiedene Bildschirmgrößen
3. **Browser-Kompatibilität**: Modernes JavaScript (ES6+) ohne Transpilation
4. **Sound-Optional**: Sounds sind optional und blockieren nicht das Spiel bei Fehlern
