# Windows 11 Terminal Icon Studio

Prosty, jednoplikowy kreator ikon profili dla **Windows Terminal (Windows 11)** z przezroczystymi zaokrąglonymi narożnikami, podziałem na strefę paska tytułu i okna roboczego oraz natywnym eksportem HiDPI.

## Główne funkcje

- **Dwie niezależne strefy okna:** osobne kolory i gradienty liniowe dla paska tytułu (górnego lub bocznego) oraz wnętrza terminala, tekstury (*CRT Scanlines*, kropki, siatka) i pełna kontrola przycisków paska.
- **4 źródła symboli i ikon:**
  - **Nerd Fonts & Tekst:** wyszukiwalna biblioteka 110+ glifów BMP oraz podgląd całej aplikacji w wybranym foncie (*JetBrainsMono*, *FiraCode*, *Hack*, *Silkscreen*, *VT323*).
  - **Matryce pikselowe 1-bit:** ostre piktogramy zaprojektowane pod siatkę `16×16`.
  - **Integracja `selfh.st/icons`:** oficjalne ikony SVG usług i systemów (w kolorze lub jako sylwetka).
  - **Własny plik (Drag & Drop):** obsługa lokalnych plików SVG, PNG i WebP.
- **50+ gotowych szablonów i własne profile:** profile systemowe, deweloperskie, DevOps oraz 50 motywów kolorystycznych, zapis własnych presetów w `localStorage` i eksport/import `.JSON`.
- **Edytor pikseli 2.0:** rysowanie bezpośrednio na podglądzie (*Ołówek*, *Wiadro*, *Gumka*, *Pipeta*), symetria `X/Y`, przesuwanie warstwy oraz historia `Ctrl+Z` / `Ctrl+Y`.
- **Makieta Windows 11 i WCAG 2.1:** podgląd `1:1` na pasku kart i w rozwijanym menu profili (tryb ciemny/jasny) wraz z automatyczną kontrolą kontrastu.
- **Kompletny eksport:** przezroczysty `.PNG` (`16–128 px`), wielowarstwowy `.ICO`, wektorowy `.SVG`, kopiowanie PNG do schowka, generator wpisu do `settings.json` oraz hurtowe paczki `.ZIP`.

## Uruchomienie

Aplikacja nie wymaga instalacji ani budowania (`zero-build`):
1. Otwórz plik `index.html` bezpośrednio w dowolnej nowoczesnej przeglądarce **lub**
2. Włącz **GitHub Pages** w ustawieniach repozytorium (`Settings → Pages → Deploy from a branch`).

## Dodawanie ikony do Windows Terminal

1. Pobierz wygenerowany plik `.png` (np. `16×16` lub `32×32`) albo wielowarstwowy `.ico`.
2. Kliknij **⚙️ settings.json** w aplikacji, skopiuj wygenerowany obiekt JSON i wklej go do sekcji `"profiles": { "list": [ ... ] }` w ustawieniach Windows Terminal (`Ctrl+,` → *Otwórz plik JSON*).

## Struktura repozytorium

```text
.
├── index.html      # Kompletna aplikacja (HTML + Tailwind CDN + Vanilla JS)
├── README.md       # Dokumentacja projektu
├── AGENTS.md       # Wytyczne architektoniczne dla agentów AI
└── LICENSE         # Licencja MIT
```

## Licencja

Projekt udostępniany na licencji [MIT](LICENSE).
