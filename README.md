# KLNTech — strona firmowa (paczka wdrożeniowa)

Statyczna, interaktywna strona-portfolio studia KLNTech. Działa w 100% po stronie
przeglądarki (HTML + JS), więc hostuje się ją jako **statyczne pliki na GitHub Pages**
— bez backendu i bez kroku builda.

## Co jest w paczce

```
klntech-site/
├── index.html              # przekierowanie na stronę główną (KLNTech.dc.html)
├── KLNTech.dc.html         # strona główna (hero, graf skilli, projekty, współpraca, kontakt)
├── Platana.dc.html         # case study — Platana
├── MakeItBakeIt.dc.html    # case study — MakeItBakeIt
├── Lab.dc.html             # /lab — 20 demonstracji technicznych
├── support.js              # runtime renderujący pliki .dc.html (KONIECZNY, leży obok)
├── demos/                  # osadzone, klikalne prototypy aplikacji (iframe)
├── assets/                 # zrzuty ekranów (Platana, MakeItBakeIt)
├── .nojekyll               # wyłącza Jekyll na GitHub Pages (zostaw)
├── .github/workflows/deploy.yml   # automatyczny deploy na Pages przy push do main
├── CLAUDE_CODE_PROMPT.md   # wklej to do Claude Code
└── docs/                   # kontekst: BRIEF, SITEMAP, PROPOZYCJA
```

## O plikach `.dc.html`

To **gotowa, działająca strona** (nie szkic do przepisania). Każdy plik `.dc.html`
renderuje się przez `support.js` po stronie klienta. Nic nie trzeba budować ani
kompilować — wystarczy serwować te pliki statycznie. Wszystkie ścieżki są względne,
więc działają od razu na GitHub Pages.

## Jak opublikować — skrót

1. Utwórz repozytorium na GitHub (zalecane: `klntech.github.io`).
2. Wrzuć całą zawartość folderu `klntech-site/` do repo (łącznie z `.github/`,
   `.nojekyll`, `index.html`).
3. Push do gałęzi `main`. Workflow `deploy.yml` sam opublikuje stronę.
4. W repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
5. Po chwili strona żyje pod `https://<user>.github.io/` (lub `klntech.github.io`).

Pełna instrukcja krok-po-kroku oraz podmiana na własną domenę `klntech.pl` —
patrz `CLAUDE_CODE_PROMPT.md`.

## Edycja treści

Teksty (PL/EN), dane firmy i dane grafu skilli siedzą w klasie `Component`
wewnątrz każdego `.dc.html` (obiekt `C = { pl:{...}, en:{...} }` oraz, w
`KLNTech.dc.html`, metoda `_expandGraph`). Zmiana tekstu = edycja stringa, bez
ruszania layoutu.
