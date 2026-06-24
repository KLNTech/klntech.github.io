# Prompt dla Claude Code — opublikuj stronę KLNTech na GitHub Pages

Wklej poniższą treść do Claude Code, mając otwarty folder `klntech-site/`.

---

Jesteś inżynierem DevOps. W tym folderze jest **gotowa, statyczna strona** firmy
KLNTech (pliki `.dc.html` renderowane po stronie klienta przez `support.js`).
Twoim zadaniem jest opublikować ją na **GitHub Pages**. NIE przepisuj ani nie
przebudowuj strony — to działający produkt. Nie ma kroku builda; to czysto
statyczne pliki.

## Zrób po kolei

1. **Zweryfikuj pliki.** Upewnij się, że obok `.dc.html` leży `support.js`,
   oraz że są: `index.html`, `.nojekyll`, `.github/workflows/deploy.yml`,
   foldery `demos/` i `assets/`. Wszystkie odwołania są względne — nie zmieniaj
   ścieżek.

2. **Lokalny test (opcjonalnie).** `python3 -m http.server 8080` w tym folderze,
   otwórz `http://localhost:8080/` — powinno przekierować na stronę główną i
   pokazać działający graf skilli oraz osadzone prototypy.

3. **Repozytorium.** Zainicjuj repo i wypchnij na GitHub:
   ```bash
   git init -b main
   git add -A
   git commit -m "KLNTech site"
   git remote add origin git@github.com:<USER>/klntech.github.io.git
   git push -u origin main
   ```
   Zalecana nazwa repo: `klntech.github.io` (wtedy adres to `https://klntech.github.io/`).
   Jeśli użyjesz innej nazwy, strona będzie pod `https://<USER>.github.io/<repo>/`
   — wszystkie linki są względne, więc zadziała w obu przypadkach.

4. **Włącz Pages.** W repo: **Settings → Pages → Build and deployment →
   Source: „GitHub Actions"**. Workflow `.github/workflows/deploy.yml` opublikuje
   stronę przy każdym push do `main`. Sprawdź zakładkę **Actions**, że deploy
   przeszedł na zielono, i otwórz wydany adres.

5. **Sanity check po wdrożeniu:** strona główna ładuje się, działają przełączniki
   PL/EN i jasny/ciemny, graf skilli reaguje na kliknięcia (zoom + fale), linki
   „Pełne case study" otwierają `Platana` i `MakeItBakeIt`, a `/lab` (link w nawigacji)
   pokazuje 20 efektów.

## Własna domena `klntech.pl` (zalecane pod weryfikację Apple)

GitHub Pages wymaga jednego pliku + 2 wpisów DNS:

1. Dodaj plik **`CNAME`** w korzeniu repo z jedną linią:
   ```
   klntech.pl
   ```
2. U rejestratora domeny ustaw DNS:
   - 4 rekordy **A** dla `@` → `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`
   - rekord **CNAME** dla `www` → `<USER>.github.io`
3. W repo: **Settings → Pages → Custom domain** → wpisz `klntech.pl`, zapisz,
   a po propagacji DNS zaznacz **Enforce HTTPS**.

Commit z plikiem `CNAME` wystarczy, by workflow przepchnął domenę.

## Czego NIE robić

- Nie zmieniaj treści `.dc.html` ani nie usuwaj `support.js` (bez niego strona się
  nie wyrenderuje).
- Nie dodawaj frameworka ani kroku builda — to niepotrzebne.
- Nie zmieniaj nazw plików `*.dc.html` (linki między stronami zależą od nich).
