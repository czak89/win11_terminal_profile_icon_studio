# AGENTS.md — Wytyczne dla agentów AI

Ten plik definiuje zasady architektoniczne, konwencje oraz stan techniczny repozytorium **Windows 11 Terminal Icon Studio** dla agentów kodujących (GitHub Copilot, Claude Code, Cursor, Codex, Jules).

## 1\. Architektura projektu

* **Single-File Vanilla Web App:** Cała aplikacja musi mieścić się w jednym samowystarczalnym pliku HTML (`index.html`). Nie dodawaj bundlerów (Vite, Webpack), `node\_modules` ani osobnych plików `.js` / `.css` — projekt jest przystosowany do bezpośredniego hostingu na **GitHub Pages** i uruchamiania lokalnie z dysku.
* **Zależności zewnętrzne (wyłącznie CDN):**

  * Tailwind CSS (`https://cdn.tailwindcss.com`)
  * Google Fonts (`Fira Code`, `JetBrains Mono`, `Roboto Mono`, `Silkscreen`, `VT323`, `Inter`)
  * Webfonty Nerd Fonts v3.3.0 (`jetbrainsmono-nerd-font.css`, `firacode-nerd-font.css`, `hack-nerd-font.css`, `SymbolsNerdFont-Regular.ttf`) ładowane z jsDelivr z atrybutem `crossorigin="anonymous"`.
* **Globalna typografia:** Zmiana fontu aktualizuje zmienną CSS `--app-font` dla całego dokumentu oraz wymusza załadowanie czcionki przez `document.fonts.load(...)` przed przerenderowaniem płótna `<canvas>`.

## 2\. Kluczowe moduły w kodzie

* `renderIconToCanvas(targetCanvas, targetSize, overrides)` — główny, bezstanowy względem rozdzielczości renderer wektorowy. Używany jednocześnie do podglądu, eksportu `.PNG` (16–128 px), generowania wszystkich warstw HiDPI w pliku `.ICO` oraz renderowania ikon w paczce `.ZIP`.
* \*\* natywne generatory binarne (bez zewnętrznych bibliotek):\*\*

  * `buildIcoBufferFromCanvases(canvases, sizes)` — składa wielowarstwowy plik Windows `.ICO` z osadzonymi strumieniami PNG.
  * `buildZipBlob(files)` + `crc32(bytes)` — tworzy poprawne archiwum PKZIP zawierające ikony PNG, opcjonalne `.ICO` oraz `profiles.json`.
* **Edytor pikseli 2.0:** przechowuje ręczne nadpisania w `pixelOverrides` (`Map<"x,y", hex | null>`), wspiera historię `pixelHistory` (`Ctrl+Z` / `Ctrl+Y`), symetrię `X/Y`, przesuwanie warstwy oraz wypełnianie `floodFillAt()`.
* **Trwałość danych:** własne profile użytkownika zapisywane są w `localStorage` pod kluczem `win11\_terminal\_custom\_presets\_v1` oraz przez eksport/import `.JSON`.

## 3\. Znane braki do naprawy przy pierwszej edycji kodu

Jeśli w pliku HTML nadal występują ucięte fragmenty z wcześniejszych iteracji, należy je naprawić w pierwszej kolejności:

1. **Brakujące elementy HTML w panelu paska tytułu:** kontrolki `dotsStyle`, `dotsCount` (`dotsCountVal`), `dotSize` (`dotSizeVal`), `dotsPosX` (`dotsXVal`), `dotsPosY` (`dotsYVal`) oraz opcjonalne płótna podglądu skalowania (`scale1xCanvas`, `scale15xCanvas`, `scale2xCanvas`, `scale3xCanvas`).
2. **Brakujące referencje DOM w JS:** `gridOverlay`, `toggleGrid`, `presetSearch`, `fontSelect`, `symbolText`, `symbolColor`, `symbolColorHex`, `symbolSize`, `fontSizeVal`, `mediaScale`, `mediaScaleVal`, `symbolOffsetX`, `offsetXVal`, `symbolOffsetY`, `offsetYVal`, `fontBold`, `fontSmoothing`, `symbolShadow`, `symbolOutline`, `dotsStyle`, `dotsCount`, `dotsCountVal`, `dotSize`, `dotSizeVal`, `dotsPosX`, `dotsXVal`, `dotsPosY`, `dotsYVal`, `dotsSpacing`, `dotsSpacingVal`, `dotsColor`, `dotsColorHex`, `barHeight`, `barHeightVal`, `cornerRadiusPct`, `cornerRadiusVal`, `drawBorder`, `borderMode`, `borderColor`, `borderColorHex`, `borderOpacity`, `borderOpacityVal`, `drawGloss`, `badgeColor`, `badgePosition`, `badgeSize`, `badgeSizeVal`, `badgeHalo`.
3. **Urwane funkcje JS:** `setNerdGlyph()`, `drawBadgePath()` + `drawCornerBadge()`, `applyPixelGlyph()`, `loadSelfHostIcon()`, `loadSelfHostCustom()`, `alignDotsLeft()`, `alignDotsRight()`, `setBadgeType()`, `setBadgeColor()`.

## 4\. Konwencje i weryfikacja

* Język interfejsu użytkownika (etykiety, komunikaty toast, opisy szablonów): **polski**.
* Przy modyfikacji UI zachowuj pełną funkcjonalność istniejących kontrolek oraz spójną stylistykę ciemnego motywu Tailwind (`slate-950` / `slate-900` / `blue-600`).
* Po każdej zmianie zweryfikuj brak błędów składniowych oraz `ReferenceError` / `TypeError` podczas inicjalizacji `DOMContentLoaded` i renderowania `render16x16()`.

