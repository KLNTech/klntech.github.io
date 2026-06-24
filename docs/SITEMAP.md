# KLNTech — mapa strony i sekcje

Jedna strona główna (sekcje z kotwicami) + 2 case studies + strony prawne.
Wszystkie teksty PL/EN z `content/*.json`. Przełączniki: **język (PL/EN)** i
**motyw (ciemny/jasny)**.

## Strona główna `/`

1. **Nav (sticky)** — wordmark KLNTech · linki do sekcji · przełącznik PL/EN ·
   przełącznik ciemny/jasny.
2. **Hero** (ciemny) — `company.tagline`. Duży nagłówek Fraunces, jedno CTA
   („Zobacz projekty” / „See the work”) + drugie („Kontakt”). W tle subtelny,
   ambientowy podgląd grafu skilli (opacity szeptu, wyłączany przy reduced-motion).
3. **Czym jest KLNTech** (paper) — `company.elevatorPitch` + 5 kafli `capabilities`
   (natywne mobile, AR, backend/płatności, systemy designu, dyscyplina inżynierska).
4. **Projekty — zajawki** (ciemny) — 2 duże karty: MakeItBakeIt i Platana
   (`projects.flagships`), każda z własnym akcentem produktu, miniaturą motywów i
   linkiem do pełnego case study. Pod spodem pasek „Lab” (`projects.lab`).
5. **★ Graf skilli organizacyjnych** (ciemny, sekcja-sygnatura) — interaktywny graf
   z `skills.json`. Węzły = projekty + skille (kolor = kategoria), krawędzie = relacje.
   Hover/klik węzła → panel z `blurb`. Legenda kategorii. Filtr kategorii.
   **Fallback bez JS / a11y:** lista skilli pogrupowana po kategorii + opis relacji.
6. **Jak pracujemy** (paper) — krótka narracja workflow develop→test→review na bazie
   skilli (task-decomposition → develop/test/review → versioning). 3–4 kroki, ikony.
7. **Kontakt + dane firmowe** (ciemny) — e-mail, GitHub; pełne dane: nazwa,
   forma prawna, NIP, REGON, PKD, adres, data rozpoczęcia. Mikrodane schema.org
   (`Organization` / `LocalBusiness`).
8. **Footer** — copyright, linki prawne, powtórzony przełącznik języka.

## `/projects/makeitbakeit`

Hero produktu (akcent złoty) → problem/rozwiązanie → **AR** (35 cm, świeczki, posypka)
→ **marketplace** (Spring Boot, Stripe Connect, model 5%) → **system designu**
(3 motywy „jadalne kolory” z przełącznikiem) → stack → status. Dane z
`projects.flagships[makeitbakeit]`.

## `/projects/platana`

Hero produktu (akcent butelkowa zieleń) → idea atlasu → **216 rycin** (animacja
ink-draw, jeśli zrobimy próbkę SVG) → **4 motywy** (przełącznik) → **5 języków** →
**jakość** (121 testów, snapshoty) → stack → status. Dane z
`projects.flagships[platana]`.

## `/legal/imprint` — „Dane firmowe / Company details”

Pełny zestaw: Wojciech Kłaniecki KLNTech · JDG · NIP 8863039727 · REGON 542099119 ·
PKD 62.10.B · Przyjaciół Żołnierza 22 lok. 11, 58-304 Wałbrzych · data rozpoczęcia
01.07.2025. To strona, na którą warto wskazać recenzentowi Apple.

## `/legal/privacy` — polityka prywatności (PL/EN)

Krótka, uczciwa: strona statyczna, brak third-party trackerów, brak ciasteczek
marketingowych (jeśli dodasz analitykę — opisz ją). Kontakt do administratora danych.

---

## Komponenty (jedna kanoniczna implementacja każdego — wzorowane na `candy-components`)

`SiteNav`, `LangToggle`, `ThemeToggle`, `Hero`, `CapabilityCard`, `ProjectCard`,
`ThemeSwatch` (miniatury motywów), `SkillsGraph` (wyspa) + `SkillsGraphFallback`,
`WorkflowSteps`, `ContactCard`, `CompanyFacts`, `Footer`, `SeoHead`.

## SEO / meta

`<title>` i `meta description` per strona (PL/EN), Open Graph + Twitter card z
wygenerowaną kartą OG (ciemna, wordmark + tagline + miniatura grafu), `sitemap.xml`,
`robots.txt`, JSON-LD `Organization`. `lang` atrybut zgodny z aktywnym językiem.
