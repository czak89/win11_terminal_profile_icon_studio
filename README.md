# Windows 11 Terminal Icon Studio

Jednoplikowy, bezinstalacyjny (`zero-build`) kreator ikon profili oraz schematów kolorów dla **Windows Terminal (Windows 11)** z przezroczystymi zaokrąglonymi narożnikami, podglądem 1:1 w makiecie systemu, edytorem pikseli i natywnym eksportem HiDPI.

## Główne funkcje

### Projektowanie ikony i podgląd Windows 11
- **Przejrzysty interfejs z 5 zakładkami:** *Szablony*, *Okno*, *Symbol*, *Detale* oraz *Schemat WT* — z lewą kolumną jako dedykowaną stacją podglądu, edycji i eksportu.
- **Dwie niezależne strefy okna:** 3 układy (*Górny pasek*, *Pasek boczny*, *Bezramkowy*), 2-kolorowe gradienty liniowe, tekstury (*CRT Scanlines*, kropki, siatka), pełna kontrola przycisków paska tytułu, inteligentna obwódka okna (*Auto* / własny kolor) oraz generator palet (`🎲 Losuj` z blokadą stref).
- **4 źródła symboli i ikon:**
  - **Nerd Fonts & Tekst:** wyszukiwalna biblioteka 110+ glifów BMP oraz globalny podgląd aplikacji w wybranym foncie (*JetBrainsMono*, *FiraCode*, *Hack*, *Silkscreen*, *VT323*).
  - **Matryce pikselowe 1-bit:** ostre piktogramy zaprojektowane pod siatkę `16×16`.
  - **Integracja `selfh.st/icons`:** oficjalne ikony SVG usług i systemów (w kolorze lub jako sylwetka) z czystym eksportem wektorowym do `.SVG`.
  - **Własny plik (Drag & Drop):** obsługa lokalnych plików SVG, PNG i WebP.
- **Znaczniki statusu (Badge) i etykiety tekstowe:** *Kropka*, *Tarcza*, *Piorun*, *Kłódka*, *Gwiazda* oraz pigułka tekstowa (*Pill Badge*, np. `DEV`, `STG`, `PRD`, `SSH`, `ADM`) z wycięciem halo, skalą i pozycją w dowolnym narożniku.
- **Ergonomiczna edycja i Edytor Pikseli 2.0:** domyślne narzędzie **✋ Przesuń** (przeciąganie symbolu + kółko myszy do skalowania), narzędzia *Ołówek*, *Wiadro (Flood Fill)*, *Gumka*, *Pipeta*, lustro `X/Y`, przesuwanie warstwy, globalna historia **Cofnij / Ponów (`Ctrl+Z` / `Ctrl+Y`)**, automatyczny szkic w `localStorage` oraz przycisk `↺ Reset`.
- **Makieta Windows 11 i WCAG 2.1:** podgląd `1:1` na pasku kart (*Karty*), w rozwijanym menu profili (*Menu ▾*) oraz na **pasku zadań Windows 11 (*Pasek*)** — w motywie ciemnym i jasnym, z automatyczną kontrolą kontrastu WCAG 2.1 i dynamiczną ikoną karty przeglądarki (*live favicon*).

### Szablony, schematy kolorów i integracja z Windows Terminal
- **50+ gotowych szablonów z podglądem na żywo:** profile systemowe, deweloperskie, DevOps i motywy kolorystyczne z miniaturowym podglądem `24×24`, wyszukiwarką, zapisem własnych profili (`★ Moje`) w `localStorage` (wraz z warstwą pikseli i ustawieniami schematu WT) oraz eksportem/importem `.JSON`.
- **Kreator schematu kolorów Windows Terminal (`🖥️ Schemat WT`):** pełna 20-kolorowa paleta ANSI (automatycznie wyliczana z kolorów ikony z kontrolą kontrastu WCAG + 16 gotowych schematów + ręczna edycja), konfiguracja wyglądu profilu (`font`, `cursorShape`, `opacity`, `useAcrylic`, `padding`) i interaktywny podgląd konsoli na żywo.
- **Importer `settings.json` (JSONC):** wklej lub wgraj swój plik `settings.json` Windows Terminal (z obsługą komentarzy `//`, `/* */` i trailing commas), dostosuj symbol i kolor dla każdego profilu osobno i pobierz gotową paczkę `.ZIP` dla wszystkich swoich profili naraz.

### Kompletny eksport (bez zewnętrznych bibliotek)
- **Obrazy i wektory:** przezroczysty `.PNG` (`16–128 px` oraz HiDPI), wielowarstwowy `.ICO` (`16×16` aż do `256×256 px`), czysty wektorowy `.SVG` (z osadzonym wektorem `selfh.st` i `@font-face` Nerd Fonts), kopiowanie PNG do schowka oraz kod Base64.
- **Udostępnianie linkiem (`🔗 Link`):** zapisuje pełny stan ikony i schematu WT w adresie URL (`#state=...` z kompresją `deflate-raw`) — bez żadnego backendu.
- **Konfiguracja i instalator PowerShell:** modal `⚙️ settings.json` (gotowe bloki profilu z GUID i schematu kolorów) oraz generator paczek `.ZIP` (z szablonami wbudowanymi, własnymi `★ Moje` i/lub zaimportowanymi profilami) zawierający bezpieczny skrypt **`install-icons.ps1`** automatycznie robiący kopię zapasową `settings.json` i aktualizujący ścieżki ikon.

## Skróty klawiszowe

Naciśnij `?` w aplikacji, aby otworzyć podręczną ściągawkę:

| Skrót | Akcja |
| --- | --- |
| `V` / `M` | Narzędzie **Przesuń symbol** |
| `B` / `P` | **Ołówek** (edycja pikseli) |
| `G` | **Wiadro** (Flood Fill) |
| `E` | **Gumka** |
| `I` | **Pipeta** |
| `R` | Losuj paletę kolorów |
| `← ↑ ↓ →` (+ `Shift`) | Precyzyjne przesuwanie symbolu (`0.5 px` / `1 px`) |
| `Ctrl+Z` / `Ctrl+Y` | Globalne Cofnij / Ponów |
| `?` | Pokaż / ukryj okno skrótów |
| `Esc` | Zamknij aktywne okno modalne |

## Uruchomienie

Aplikacja nie wymaga instalacji, Node.js ani budowania (`zero-build`):
1. Otwórz plik `index.html` bezpośrednio w dowolnej nowoczesnej przeglądarce **lub**
2. Uruchom przez **GitHub Pages** (repozytorium zawiera gotowy workflow `.github/workflows/deploy2pages.yml`).

## Dodawanie ikon do Windows Terminal

- **Pojedynczy profil:** pobierz `.png` lub wielowarstwowy `.ico`, kliknij **⚙️ settings.json**, skopiuj blok profilu (i opcjonalnie schematu kolorów) i wklej do ustawień Windows Terminal (`Ctrl+,` → *Otwórz plik JSON*).
- **Cały zestaw profili (automatycznie):** otwórz **⚙️ settings.json → 📥 Importuj**, wczytaj swój `settings.json`, dostosuj ikony i pobierz paczkę **📦 Paczka ZIP** — rozpakuj archiwum i uruchom dołączony skrypt `install-icons.ps1`.

## Struktura repozytorium

```text
.
├── index.html                          # Kompletna aplikacja (HTML + Tailwind CDN + Vanilla JS)
├── README.md                           # Dokumentacja projektu
├── AGENTS.md                           # Wytyczne architektoniczne dla agentów AI
├── LICENSE                             # Licencja MIT
└── .github/workflows/deploy2pages.yml  # Automatyczny deploy na GitHub Pages
```

## Licencja

Projekt udostępniany na licencji [MIT](LICENSE).
