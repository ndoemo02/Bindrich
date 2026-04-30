# Notatki z Migracji: Piekarnia Bindrich

## 1. Analiza Techniczna (Legacy Stack)
- **CMS:** WordPress 6.9.4
- **Builder:** Oxygen Builder (Templates ID 47, 70, etc.)
- **Uwagi:** Treść jest "zaszyta" w shortcode'ach Oxygena, co utrudnia automatyczny eksport. Wymagane było manualne parsowanie HTML.

## 2. Audyt Contentu (Co przenosimy, a co usuwamy)

### Do przeniesienia (Verified)
- [x] **Dane teleadresowe punktów sprzedaży:** 41 lokalizacji (wyciągnięte do `locations.csv`).
- [x] **Logotypy:** Pobrane do `assets/source/logos/`.
- [x] **Główna misja firmy:** Teksty o naturalnym zakwasie i tradycji z strony Home.
- [x] **Dane rejestrowe:** NIP i adres centrali.

### Do weryfikacji / Ręcznej poprawy
- [ ] **Adresy e-mail:** Usunąć `sales@example.com`. Zweryfikować `support@piekarniabindrich.pl`.
- [ ] **Godziny otwarcia:** Skrypt wyciągnął surowe dane tekstowe. Warto ujednolicić format (np. "6:00 - 18:00").
- [ ] **Linki Social Media:** Usunąć Twitter, LinkedIn, YouTube, jeśli firma ich nie prowadzi.

### Do usunięcia (Placeholders / Garbage)
- [!] Teksty "This is a block of text. Double-click this text to edit it." (np. na `/lody/`).
- [!] Linki w stopce: "SANDBOX", "OXYGEN", "CHECKLIST".
- [!] Stare skrypty śledzące / nieaktywne pluginy widoczne w kodzie HTML.

## 3. Rekomendacje dla nowej architektury
1. **Dynamiczne Lokalizacje:** Zamiast statycznych podstron dla każdego miasta, warto rozważyć interaktywną mapę (np. Mapbox/Google Maps) zasilaną z `locations.csv` (lub docelowo z bazy danych/CMS).
2. **Katalog Produktów:** Zastąpienie placeholderów realnym katalogiem z filtrowaniem po alergenach i typie pieczywa.
3. **SEO:** Zachować strukturę nagłówków `H1-H3` (obecnie Oxygen generuje ich dużo, czasem chaotycznie). Użyć czystego HTML5 (semantic tags).
4. **Wydajność:** Oryginalna strona ładuje dużo CSS/JS z Oxygena. Nowy prototyp powinien być lżejszy (Vanilla CSS + minimal JS).

## 4. Ostrzeżenia (Red Flags)
- Strona `/lody/` jest praktycznie pusta, mimo że kategoria figuruje w menu jako kluczowa.
- Brak certyfikatu SSL na niektórych zasobach (widoczne linki `http://` w kodzie).
