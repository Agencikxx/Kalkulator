# ⚔️ AlbionForge — Kalkulator Craftingu i Resellu

Darmowe narzędzie dla graczy **Albion Online** do analizy opłacalności craftowania, rafinacji i resellowania przedmiotów na rynku.

🔗 **[Otwórz kalkulator → albionforge.cba.pl](http://albionforge.cba.pl)**

---

## 📋 Spis funkcji

- [Przerabianie surowców](#-przerabianie-surowców)
- [Masowe craftowanie](#-masowe-craftowanie)
- [Reseller i Porównanie](#-reseller)
- [Skup itemów](#-skup-itemów)
- [API — ceny na żywo](#-api--ceny-na-żywo)
- [Eksport do XLSX](#-eksport-do-xlsx)

---

## ⚗ Przerabianie surowców

Kalkulator rafinacji dla wszystkich typów surowców (Ruda, Drewno, Włókno, Skóra, Kamień) w tierach T2–T8 z enchantem .0–.4.

**Co oblicza:**
- Zysk netto ze sprzedaży przetworzonego surowca
- Koszt zakupu surówki + przetworzonego niższego tieru
- Zwrot surowców (RRR) — iteracyjna symulacja kaskadowa
- Opłata stacyjna (Station Fee) wg wzoru: `ItemValue × 0.05 × (StationFee/100)`
- Tryb **Skupienie (Focus)** — kalkulator Tablicy Przeznaczenia z hybrydem
- Kalkulator **"Od zera"** — ile surówek T2 potrzebujesz dla danego tieru

**Tryby wyniku:**
- 💰 Zarobek — pełny zysk/strata
- 🔧 Koszty — tylko koszty bez ceny sprzedaży

---

## 🔨 Masowe craftowanie

Najbardziej rozbudowany moduł — analizuj setki kombinacji przedmiotów jednocześnie.

**Filtry i wybór:**
- Kategorie broni i zbroi (Miecze, Topory, Buławy, Łuki, Kostury, Zbroje itd.)
- Tiery T4–T8 × Enchanty .0–.4 (tabela z kolorami)
- Masowe ustawianie ilości (jeden klik dla całej kategorii)

**Obliczenia:**
- Zysk per przedmiot × tier × enchant
- Iteracyjny zwrot surowców (RRR) — mniej surowców niż myślisz
- Opłata stacyjna: `ItemValue × 0.1125 × (StationFee/100)` z enchant mnożnikiem (×2 per poziom)
- Artefakty i Serca Peleryn Miejskich — per tier, współdzielone dla .0–.4

**Skupienie (Focus) — tryb hybrydowy:**
```
Wydajność = (WęzełGłówny × 30) + (Specjalizacja × 250) + (Pozostałe × 15)
KosztFocus = BaseCost × 0.5^(Wydajność/10000)
```
Kalkulator dzieli craft na dwie pule: ze skupieniem i bez, gdy punkty się kończą.

**Dzienniki rzemieślnicze:**
- Blacksmith's (Kowal), Fletcher's (Łuczarz), Imbuer's (Zaklinacz), Tinker's (Majsterkowicz)
- Kaskadowanie sławy — T6 może ładować T5 jeśli PPF (Profit/Fame) jest wyższy
- Moduł Sugestii — automatycznie wybiera optymalny układ dzienników
- Tryb Market Flip i Robotnik

**📥 Eksport XLSX:**
Pobierz wyniki jako arkusz Excel z 4 zakładkami — patrz sekcja niżej.

---

## 🔄 Reseller

Sprawdź czy bardziej opłaca się wycraftować przedmiot, czy skupić go z rynku i sprzedać.

**Tryb pojedynczy:**
- Wybierz przedmiot, tier, enchant
- Wpisz cenę zakupu (rynek) i sprzedaży (Black Market)
- Wynik: zysk, ROI%, porównanie z craftem

**Tryb masowy:**
- Ten sam panel wyboru itemów co w Craftowaniu (kategorie + tabela Tier × Enchant)
- Wpisz ceny zakupu i BM dla każdej kombinacji
- Ranking opłacalności posortowany po zysku / ROI

**Porównanie trzech scenariuszy:**
1. 🔨 Craft → sprzedaj na BM
2. 🔄 Kup z rynku → sprzedaj na BM (resell/flip)
3. 📦 Sprzedaj surowce zamiast craftować

---

## 💰 Skup itemów

Prosty kalkulator skupu z 3 miejsc × 7 kategorii.

`Zysk = wartość rynkowa − cena skupu` (bez podatku, bo skup to transakcja poza rynkiem)

---

## 🔌 API — ceny na żywo

Jeden przycisk **"⬇ Pobierz ceny ze wszystkich miast"** automatycznie:

1. Pobiera ceny z **8 miast jednocześnie**: Caerleon, Bridgewatch, Fort Sterling, Lymhurst, Martlock, Thetford, Brecilien, Black Market
2. Wybiera **najlepszą cenę zakupu** (najtańszy sell_price dla surowców)
3. Wybiera **najlepszą cenę sprzedaży** (najdroższy sell dla przedmiotów)
4. Wypełnia **wszystkie pola** w kalkulatorach automatycznie
5. Pokazuje **wolumen dzienny** i czas ostatniej aktualizacji przy każdej cenie

**Przegląd rynku (📊):**
Tabela wszystkich surowców × 8 miast z:
- Cena w każdym mieście (kolor: 🔵 best buy, 🟢 best sell)
- Wolumen dzienny per miasto
- Sortowanie po nazwie / cenie / wolumenie

Dane pochodzą z **[Albion Online Data Project](https://www.albion-online-data.com)** — darmowego, community-driven API zbierającego dane bezpośrednio od graczy.

---

## 📥 Eksport do XLSX

Po obliczeniu craftowania kliknij **"📥 Pobierz XLSX"** aby pobrać arkusz z 4 zakładkami:

| Arkusz | Zawartość |
|--------|-----------|
| **% zysku** | Tabela: wiersze = Tier.Enchant (T4, T4.1...), kolumny = przedmioty, wartości = % ROI |
| **Zysk na szt** | Ta sama tabela, wartości w silver/szt. |
| **Ceny** | Wszystkie wpisane ceny: surowce, artefakty, serca, ceny sprzedaży |
| **Surowce wymagane** | Per przedmiot: ile surowca/szt i łącznie **po zwrocie** + sekcja zbiorcza |

Wiersz 1 każdego arkusza zawiera parametry sesji (zwrot surowców %).

---

## ⚙️ Mechaniki gry — implementacja

### Opłata stacji (Station Fee / Nutrition)
```
ItemValue = suma(mat.ilość × IV[tier]) × 2^enchant
IV: T4=13, T5=37, T6=101, T7=261, T8=581

Nutrition (craft)   = ItemValue × 0.1125
Nutrition (rafin.)  = ItemValue × 0.05
Koszt silver = Nutrition × (StationFee / 100)
```
Wpisujesz koszt za **100 Nutrition** (np. 450), kalkulator liczy resztę.

### Zwrot surowców (RRR)
Symulacja iteracyjna — kalkulator oblicza **minimalną ilość** surowców do kupienia:
```
minBuy(targetQty, recipePerItem, rr) → binary search
```
Enchanted surowce wymagają tej samej ilości co .0 — kalkulator uwzględnia to poprawnie.

### Fame dzienników (Base Fame)
```
FAME_PER_MAT: T4=22.5, T5=90, T6=270, T7=645, T8=1395
Pojemność:    T4=3600, T5=7200, T6=14400, T7=28380, T8=58590
```
**Enchant NIE wpływa na fame** trafiającą do dziennika — T6.3 = T6.0.

### Skupienie (Focus)
```
BaseCost craft:  T4=75,  T5=150, T6=300, T7=600, T8=1200
BaseCost rafin.: T4=9,   T5=39,  T6=167, T7=714, T8=3055
RealCost = BaseCost × 0.5^(Wydajność/10000)
```

---

## 🛠️ Technologia

| Element | Szczegół |
|---------|----------|
| Frontend | 100% Vanilla JavaScript — zero frameworków |
| Plik | Single-file HTML (~1 MB) |
| Baza danych | 247 przedmiotów wbudowanych w kod |
| API | Albion Online Data Project (Europe server) |
| Eksport | SheetJS (XLSX) |
| Persystencja | localStorage (Focus Destiny Board) |
| Hosting | GitHub Pages / CBA.pl |

---

## 🔄 Aktualizowanie

**GitHub Pages:** wgraj nowy `index.html` do repozytorium → strona aktualizuje się automatycznie w ~1 min.

**CBA.pl:** zaloguj się → Panel → Wysyłanie plików → wybierz nowy `index.html`.

---

## 📊 Baza przedmiotów

**247 przedmiotów** podzielonych na kategorie:

| Kategoria | Ilość |
|-----------|-------|
| Broń wojownika (Miecze, Topory, Buławy, Młoty, Rękawice, Kusze) | 48 |
| Broń łowcy (Łuki, Sztylety, Włócznie, Kije, Shapeshifter, Natura) | 48 |
| Broń maga (Ogień, Świętość, Arkan, Mróz, Klątwa) | 40 |
| Off-hands (Tarcze, Pochodnie, Tomy) | 18 |
| Zbroje (Płytowa, Skórzana, Tkaninowa) | 72 |
| Pozostałe (Peleryny, Torby, Narzędzia) | 21 |

---

*Wszystkie prawa do zasobów gry należą do Sandbox Interactive GmbH.*
*Dane rynkowe: Albion Online Data Project (community project, dozwolony przez TOS)*
