# KLNTech — brief realizacyjny (kierunek artystyczny + wymagania)

> Przeczytaj po `PROPOZYCJA.md`. To jest „co i jak” dla builda. Reguły wyglądu:
> `brand/brand.md` + `brand/tokens.css`. Treść: `content/*.json`.

## Zadanie w jednym zdaniu

Zbuduj nowoczesną, dwujęzyczną (PL/EN) stronę-portfolio studia KLNTech w **Astro**,
publikowaną na **GitHub Pages**, z interaktywnym **grafem skilli** jako sercem strony —
która jednocześnie spełnia wymóg „funkcjonalnej strony organizacji” Apple.

## Kierunek artystyczny

Synteza „Studio/Atelier + Living Capability Graph” (patrz `PROPOZYCJA.md` §4):

- **Ton:** dorosły, rzemieślniczy, inżynierski. Fraunces (serif, display) + Inter
  (UI) + JetBrains Mono (etykiety grafu, dane firmowe).
- **Baza:** dark-first hero (`--bg-page`), sekcje treści przełączane na papier przez
  `[data-surface="paper"]`. Jeden akcent CTA: złoto `--accent`.
- **Światy produktów:** MakeItBakeIt wnosi złoto/wisienkę, Platana butelkową
  zieleń/miedź. Używaj ich TYLKO w sekcjach tych produktów i jako kolorów węzłów grafu.
- **Ruch znaczący (nie kicz):** ink-draw / fade / subtelny parallax. Każda animacja coś
  znaczy. Zawsze respektuj `prefers-reduced-motion` (wyłącza graf-ambient, ink-draw,
  parallax). To wprost wasza reguła `botanical-not-kitsch`.

## Twarde wymagania (must-have)

1. **Dwujęzyczność PL/EN** — przełącznik trwały (localStorage **niedozwolone w
   artefaktach Claude, ale na realnej stronie OK**; preferuj routing `/` i `/en/` lub
   parametr — wybierz prostsze w Astro). Domyślny PL, `lang` atrybut poprawny.
2. **Graf skilli** — interaktywny (hover/klik → panel), z legendą i filtrem kategorii,
   ORAZ dostępny fallback (lista) działający bez JS i dla czytników ekranu.
3. **Kompletne dane firmowe** na `/legal/imprint` + w stopce (NIP, REGON, adres,
   forma prawna, PKD, data startu) — to dowód dla Apple.
4. **Dwa case studies** (MakeItBakeIt, Platana) z przełącznikiem motywów produktu.
5. **Dostępność:** kontrast AA, nawigacja klawiaturą, focus states, alt-y, semantyczny
   HTML, `prefers-reduced-motion`.
6. **Wydajność:** 0 JS tam, gdzie niepotrzebny (Astro islands). Lighthouse ≥ 95
   Performance/Best-Practices/SEO na stronie głównej (zweryfikuj).
7. **Bez third-party** w produkcji: fonty samo-hostowane, brak Google Fonts/analytics
   trackerów (jeśli analityka — tylko prywatna/cookieless, opisana w polityce).
8. **SEO:** title/description per strona, Open Graph (wygenerowana karta OG),
   `sitemap.xml`, `robots.txt`, JSON-LD `Organization`.
9. **Hosting:** build i deploy przez GitHub Actions na push do `main` (patrz
   `DEPLOYMENT.md`). `base` w `astro.config` ustawiony pod `klntech.github.io`
   (z łatwą podmianą na własną domenę).

## Graf skilli — szczegóły implementacji

- Dane: `content/skills.json` (`nodes`, `edges`, `categories`).
- Layout: force-directed (np. d3-force) **lub** policzony statycznie i zapisany
  (preferowane dla determinizmu i SSR). Klastry wg kategorii; projekty wyróżnione
  kształtem (kwadrat) i rozmiarem.
- Interakcja: hover podświetla węzeł + sąsiadów + krawędzie; klik otwiera panel z
  `label` + `blurb` (w aktywnym języku) + listą połączeń. Filtr kategorii (legenda
  klikalna). Na mobile: tap zamiast hover, panel jako bottom-sheet.
- Wydajność/a11y: render SVG (nie canvas) dla ostrości i dostępności; każdy węzeł
  to element fokusowalny z `aria-label`. Fallback `SkillsGraphFallback` renderuje te
  same dane jako pogrupowaną listę z opisem relacji — widoczny gdy brak JS.

## Czego unikać

- Stockowych zdjęć, „korporacyjnego” banału, gradientów-tęcz, emoji jako ikon UI
  (emoji wolno w danych motywów, np. 🍦/🌿, jako etykiety — nie jako interfejs).
- Forkowania kolorów per sekcja (używaj ról + `data-surface`).
- Bibliotek-ciężarów dla efektu; graf to jedyna uzasadniona większa zależność.

## Definicja ukończenia (Definition of Done)

- [ ] Buduje się `npm run build` bez błędów; działa `npm run preview`.
- [ ] PL i EN kompletne na wszystkich stronach; przełącznik działa.
- [ ] Graf interaktywny + fallback; działa bez JS (treść widoczna).
- [ ] Dane firmowe kompletne (imprint + stopka), mikrodane `Organization`.
- [ ] Lighthouse ≥ 95 (Perf/BP/SEO) na `/`; brak third-party requestów.
- [ ] `prefers-reduced-motion` respektowane; nawigacja klawiaturą OK.
- [ ] GitHub Actions publikuje na Pages; strona żyje pod `klntech.github.io`.
- [ ] `VERSION.md` podbity, README zaktualizowane.
