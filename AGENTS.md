# AGENTS.md — Wytyczne dla agentów AI

Ten plik definiuje zasady architektoniczne, konwencje oraz stan techniczny repozytorium **Windows 11 Terminal Icon Studio** dla agentów kodujących (GitHub Copilot, Claude Code, Cursor, Codex, Jules, Antigravity).

## 1. Architektura projektu

* **Single-File Vanilla Web App:** Cała aplikacja musi mieścić się w jednym samowystarczalnym pliku HTML (`index.html`). Nie dodawaj bundlerów (Vite, Webpack), `package.json`, `node_modules` ani osobnych plików `.js` / `.css` — projekt jest przystosowany do bezpośredniego hostingu na **GitHub Pages** i uruchamiania lokalnie z dysku.
* **Zależności zewnętrzne (wyłącznie CDN):**
  * Tailwind CSS (`https://cdn.tailwindcss.com`)
  * Google Fonts (`Fira Code`, `JetBrains Mono`, `Roboto Mono`, `Silkscreen`, `VT323`, `Inter`)
  * Webfonty Nerd Fonts v3.3.0 (`jetbrainsmono-nerd-font.css`, `firacode-nerd-font.css`, `hack-nerd-font.css`, `SymbolsNerdFont-Regular.ttf`) ładowane z jsDelivr z atrybutem `crossorigin="anonymous"`.
* **Globalna typografia:** Zmiana fontu aktualizuje zmienną CSS `--app-font` dla całego dokumentu oraz wymusza załadowanie czcionki przez `document.fonts.load(...)` przed przerenderowaniem płótna `<canvas>`.

## 2. Kluczowe moduły w kodzie

* **Renderer i podglądy:**
  * `renderIconToCanvas(targetCanvas, targetSize, overrides)` — główny, bezstanowy względem rozdzielczości renderer wektorowy. Używany do podglądu, eksportu `.PNG` (16–128 px), wielowarstwowego `.ICO` (`16–256 px`), paczek `.ZIP`, miniatur szablonów `24×24` oraz dynamicznego favicona (`scheduleFaviconUpdate()`).
  * `setWin11PreviewMode('tabs' | 'menu' | 'taskbar')` i `setWin11PreviewTheme('dark' | 'light')` — makiety Windows 11 z kontrolą kontrastu WCAG 2.1.
* **Interfejs zakładkowy (`switchMainEditorTab`):**
  * Prawy panel podzielony na 5 zakładek: `editorTabPresets` (*Szablony*), `editorTabWindow` (*Okno*), `editorTabSymbol` (*Symbol*), `editorTabDetails` (*Detale*), `editorTabWtScheme` (*Schemat WT*).
* **Kreator schematu kolorów WT i importer JSONC:**
  * 20-kolorowa paleta ANSI (`wtSchemeState`), auto-derywacja z kolorów ikony z gwarancją kontrastu WCAG, 16 gotowych motywów, ustawienia wyglądu profilu (`wtAppearanceState`) oraz podgląd konsoli na żywo (`renderWtSchemePreview()`).
  * Importer `settings.json` (`stripJsoncComments()`, `parseImportedWtSettings()`) z obsługą komentarzy JSONC, trailing commas oraz edycją symbolu i koloru dla każdego zaimportowanego profilu.
* **Natywne generatory binarne i wektorowe (bez zewnętrznych bibliotek):**
  * `buildIcoBufferFromCanvases(canvases, sizes)` — składa wielowarstwowy plik Windows `.ICO` (`16–256 px`) z osadzonymi strumieniami PNG.
  * `buildZipBlob(files)` + `crc32(bytes)` — tworzy archiwum PKZIP zawierające ikony PNG, opcjonalne `.ICO`, `profiles.json` oraz skrypt instalacyjny PowerShell `install-icons.ps1` (z backupem `settings.json` i zapisem UTF-8 bez BOM).
  * `buildSvgMarkup()` — generuje czysty wektorowy `.SVG` (w tym inline SVG dla ikon `selfh.st`, pigułkę tekstową `pill` oraz reguły `@font-face` dla Nerd Fonts).
* **Edytor pikseli 2.0 i globalna historia zmian:**
  * Domyślne narzędzie `move` (*Przesuń symbol* z przeciąganiem i kółkiem myszy) + `pencil`, `floodfill`, `eraser`, `eyedropper`, symetria `X/Y`, przesuwanie warstwy.
  * `pixelOverrides` (`Map<"x,y", hex | null>`) oraz globalny stos Cofnij/Ponów `stateHistory` (`Ctrl+Z` / `Ctrl+Y`, maks. 60 migawek) obejmujący zarówno piksele, jak i wszystkie ustawienia ikony oraz schematu WT.
* **Trwałość danych i udostępnianie:**
  * Własne profile użytkownika: `localStorage` pod kluczem `win11_terminal_custom_presets_v1` oraz eksport/import `.JSON`.
  * Automatyczny szkic roboczy: `localStorage` pod kluczem `win11_terminal_draft_state_v1` (z przyciskiem `↺ Reset`).
  * Udostępnianie linkiem (`#state=z:...` / `#state=j:...` z `CompressionStream('deflate-raw')` i fallbackiem base64url) — ładowane z priorytetem nad szkicem roboczym przy `DOMContentLoaded`.

## 3. Konwencje i weryfikacja

* Język interfejsu użytkownika (etykiety, komunikaty toast, opisy szablonów, dokumentacja): **polski**.
* Przy modyfikacji UI zachowuj pełną funkcjonalność istniejących kontrolek oraz spójną stylistykę ciemnego motywu Tailwind (`slate-950` / `slate-900` / `blue-600`).
* Po każdej zmianie zweryfikuj:
  1. Brak błędów składniowych JS oraz zduplikowanych `id` w HTML.
  2. Spójność wszystkich wywołań `document.getElementById(...)` i atrybutów `onclick`/`oninput` z faktycznymi elementami i funkcjami.
  3. Brak `ReferenceError` / `TypeError` podczas `DOMContentLoaded`, `render16x16()` oraz kluczowych eksportów (PNG/ICO/SVG/ZIP/URL).
