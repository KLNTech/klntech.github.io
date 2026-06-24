# KLNTech — strona firmowa: analiza i propozycje

> Cel nadrzędny: **publicznie dostępna, funkcjonalna strona firmowa**, która spełni
> wymóg Apple przy zmianie konta Developer z osobistego na organizacyjne, a przy
> okazji realnie reprezentuje KLNTech jako studio software'owe.
> Stack: **Astro → GitHub Pages**. Język: **PL + EN**. Eksponujemy 2 flagowce
> (MakeItBakeIt, Platana) + interaktywny **graf skilli organizacyjnych**.

---

## 1. Co strona musi udowodnić (wymóg Apple)

Apple przy weryfikacji organizacji sprawdza, że strona jest:

1. **Publicznie dostępna i funkcjonalna** — nie placeholder, nie „strona w budowie”.
2. **O konkretnej treści** — odrzucają strony „z minimalną zawartością”.
3. **Pod domeną powiązaną z organizacją** — odrzucają linki do social mediów oraz
   strony pokazujące komunikat od rejestratora domeny.

Wniosek dla nas: strona ma mieć realną treść (projekty, opis działalności, dane
firmowe, kontakt) i — docelowo — własną domenę. To prowadzi do dwóch ostrzeżeń, które
trzeba świadomie obejść (sekcja 6).

---

## 2. Materiał, który mamy (i to jest mocna strona)

Z waszego repozytorium wyłania się obraz, którego większość jednoosobowych firm nie ma:

- **MakeItBakeIt** — Kotlin Multiplatform + Unity AR + marketplace na Spring Boot ze
  Stripe Connect. Realny, wielowarstwowy produkt.
- **Platana** — natywny iOS (SwiftUI), 216 rycin, 4 motywy, 5 języków, 121 testów.
  Dowód dbałości o rzemiosło i jakość.
- **Graf ~35 skilli organizacyjnych** — skodyfikowany sposób pracy (workflow
  develop→test→review, root-cause-analysis, versioning, system designu). To **unikat**:
  pokazuje, że za jedną osobą stoi powtarzalny proces inżynierski.

Strona ma ten materiał *pokazać*, nie tylko opisać. Graf skilli to nasz element-sygnatura.

---

## 3. Trzy kierunki (propozycje)

### Kierunek A — „Studio / Atelier” (klarowny, wiarygodny)
Edytorialny, spokojny portfel studia. Ciemny hero, sekcje na ciepłym papierze,
typografia Fraunces (serif) + Inter. Każdy produkt to osobny „pokój” z własną paletą.
Graf skilli jako jedna mocna sekcja w środku.
- **Plus:** maksymalna wiarygodność, najłatwiejszy do oceny przez recenzenta Apple, evergreen.
- **Minus:** mniej „wow” na pierwszy rzut oka.
- **Ryzyko realizacji:** niskie.

### Kierunek B — „Living Capability Graph” (techniczny, odważny)
Cała strona zorganizowana wokół **interaktywnego grafu**: węzły to projekty i skille,
krawędzie to zależności i orkiestracja. Klikasz węzeł → panel z detalem; klikasz
projekt → rozwija się case study. Strona *jest* dowodem inżynierii.
- **Plus:** najbardziej zapadające w pamięć, idealnie pokazuje „za tą firmą stoi system”.
- **Minus:** sam graf jako jedyna nawigacja bywa trudny dla części odbiorców (i recenzenta).
- **Ryzyko realizacji:** średnie (dostępność, fallback bez JS).

### Kierunek C — „Product Worlds” (wizualny, marketingowy)
Scrollytelling: duże makiety urządzeń, przełącznik motywów (oba produkty są
wielomotywowe!), immersyjne sekcje per produkt z własnym kolorem i ruchem.
- **Plus:** najładniejszy wizualnie, świetny do dzielenia się / promocji.
- **Minus:** więcej pracy nad assetami (makiety, zrzuty ekranu), mniej „firmowy”.
- **Ryzyko realizacji:** średnie/wysokie (zależne od jakości grafik).

---

## 4. Rekomendacja: synteza A + B (z elementami C)

**Rama z kierunku A** (wiarygodne studio, jasna nawigacja, kompletne dane firmowe)
**+ graf skilli z kierunku B jako interaktywne serce strony**
**+ przełącznik motywów i makiety z kierunku C w sekcjach produktów.**

Dlaczego: spełnia Apple od ręki (klarowna treść + dane + kontakt), a jednocześnie
wykorzystuje wasz unikalny atut (graf) bez ryzyka, że recenzent „się zgubi”. Strona
jest nowoczesna i interaktywna tam, gdzie to coś znaczy — nie dla samego efektu
(spójne z waszym `botanical-not-kitsch`: animacja zawsze coś znaczy).

Pełny opis wyglądu i sekcji: **`SITEMAP.md`** i **`BRIEF.md`**. Wizualna makieta hero:
**`mockup-home.html`** (dołączona w paczce).

---

## 5. Architektura strony (skrót)

Jedna strona główna z kotwicami + 2 podstrony case study + lekkie strony prawne:

```
/                    Hero → Czym jest KLNTech → Projekty (zajawki) → GRAF SKILLI
                     → Jak pracujemy (workflow) → Kontakt + dane firmowe
/projects/makeitbakeit   pełne case study (AR, marketplace, motywy)
/projects/platana        pełne case study (atlas, motywy, testy)
/legal/privacy           polityka prywatności (PL/EN)
/legal/imprint           „Dane firmowe / Impressum” — NIP, REGON, adres, forma prawna
```

Przełącznik **PL/EN** i **jasny/ciemny**; graf skilli jako wyspa interaktywna z
fallbackiem listowym (działa bez JS i dla czytników ekranu).

---

## 6. Domena i Apple — dwie rzeczy do świadomej decyzji

**(a) Domena.** Wybrałeś na teraz `klntech.github.io`. Działa technicznie i ruszamy
od razu, ale **to najsłabszy punkt pod weryfikację Apple** — `github.io` należy do
GitHuba, nie do KLNTech, a Apple wymaga „domeny powiązanej z organizacją”. Dlatego
paczka jest zbudowana tak, że **przejście na `klntech.pl` to zmiana ~5-minutowa**
(plik `CNAME` + rekordy DNS + jedna zmienna w configu). Mocna rekomendacja: zarejestruj
`klntech.pl` (~30–60 zł/rok) **przed** wysłaniem wniosku do Apple i podaj ten adres.
Masz już `makeitbakeit.pl` — ale to domena produktu, nie organizacji.

**(b) Forma prawna.** To nie dotyczy strony, ale uprzedzam, bo łatwo się o to potknąć:
KLNTech to **jednoosobowa działalność (JDG)**, a Apple dla „Organization” wymaga
podmiotu prawnego i numeru **D-U-N-S**, i nie akceptuje nazw handlowych/DBA — jako
„seller” pojawi się wtedy **Wojciech Kłaniecki**. Warto wyrobić D-U-N-S dla danych
firmy (NIP 8863039727) z wyprzedzeniem (bywa, że trwa). Strona sama w sobie jest
potrzebna niezależnie od tego.

---

## 7. Plan techniczny (dlaczego Astro)

- **Astro** generuje statyczny HTML (0 JS domyślnie) — idealny pod GitHub Pages, szybki
  i bezpieczny; interaktywność (graf, przełączniki) wstrzykujemy jako „wyspy”.
- **GitHub Actions** buduje i publikuje na każdy push do `main` (workflow w paczce).
- Treść trzymana w danych (`content/*.json`) — łatwo dodać projekt bez ruszania layoutu
  (analogia do waszego `design-source-of-truth`).
- Fonty samo-hostowane, brak skryptów third-party → lepsza prywatność i czystszy
  odbiór przy ocenie.

> Uwaga o „Node.js”: na GitHub Pages nie ma serwera Node w runtime — Node służy tu
> wyłącznie do **builda** (Astro). To dokładnie to, czego chcesz: nowoczesny pipeline,
> statyczny, darmowy hosting.

---

## 8. Co dostajesz w tej paczce

1. **`PROPOZYCJA.md`** — ten dokument.
2. **`BRIEF.md`** — kierunek artystyczny + wymagania do realizacji.
3. **`SITEMAP.md`** — pełna struktura stron i sekcji.
4. **`DEPLOYMENT.md`** — GitHub Pages krok po kroku + podmiana na `klntech.pl`.
5. **`content/`** — gotowe dane (firma, projekty, graf skilli) PL/EN.
6. **`brand/`** — tokeny kolorów/typografii + brand guide.
7. **`mockup-home.html`** — wizualna makieta strony głównej (podgląd kierunku).
8. **`CLAUDE_CODE_PROMPT.md`** — gotowy prompt do wklejenia w Claude Code, który
   zbuduje stronę Astro z tej paczki.

Następny krok: otwórz folder `klntech-website-kit/` w Claude Code i wklej zawartość
`CLAUDE_CODE_PROMPT.md`.
