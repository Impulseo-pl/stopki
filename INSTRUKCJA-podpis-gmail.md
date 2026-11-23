# Instrukcja dla Claude'a: ustaw firmową stopkę Impulseo w Gmailu

Ten plik czyta Claude pracownika Impulseo. Zadanie: ustawić w Gmailu tej osoby (konto `<imię>@impulseo.pl`, przeglądarka Chrome) firmową stopkę jako domyślny podpis. Robisz to sam przez Chrome (Claude in Chrome), człowiek tylko patrzy. **Niczego nie wysyłasz.**

## Pliki

Imię podaje człowiek w prompcie (np. `szymon`, `marceli`).

- Stopka HTML: `https://raw.githubusercontent.com/impulseo-pl/stopki/main/stopka-<imię>.html`
- Stopka tekstowa (do telefonu): `https://raw.githubusercontent.com/impulseo-pl/stopki/main/stopka-<imię>.txt`

Nie zmieniaj treści stopki. Jeśli pliku dla danego imienia nie ma, przerwij i powiedz o tym.

## Kroki

1. **Pobierz stopkę HTML** (np. `curl -s <adres> -o <folder tymczasowy>/stopka.html`) i sprawdź, że zawiera `KRS 0001255164` i `impulseo-pl.github.io/stopki/`.
2. **Włóż stopkę do schowka jako sformatowaną treść, nie jako kod.**
   - Mac (sprawdzone): skrypt Swift
     ```swift
     import AppKit
     let h = try! String(contentsOfFile: CommandLine.arguments[1], encoding: .utf8)
     let pb = NSPasteboard.general
     pb.clearContents()
     pb.setString(h, forType: .html)
     pb.setString("Stopka", forType: .string)
     ```
     uruchom: `swift schowek.swift <folder>/stopka.html`
   - Windows albo brak Swifta: otwórz `https://impulseo-pl.github.io/stopki/stopka-<imię>.html` w Chrome, zaznacz wszystko i skopiuj (Ctrl/Cmd+A, Ctrl/Cmd+C).
   - ⚠️ Wstawianie skryptem (JavaScript, `insertHTML`, `innerHTML`) do edytora Gmaila **nie działa**: Gmail blokuje to (TrustedHTML). Wklejasz ze schowka klawiszami.
3. **Gmail → koło zębate → „Zobacz wszystkie ustawienia” → zakładka „Ogólne” → sekcja „Podpis”.**
   - Jest stary podpis: kliknij go na liście, kliknij w jego edytor, zaznacz całą treść (Cmd/Ctrl+A) i wklej (Cmd/Ctrl+V). Starego podpisu **nie usuwaj koszem** (okno potwierdzenia blokuje przeglądarkę).
   - Nie ma podpisu: „Utwórz nowy”, nazwa `Impulseo`, „Utwórz”, kliknij w edytor i wklej (Cmd/Ctrl+V).
4. **Sprawdź w edytorze:** okrągłe zdjęcie, imię i nazwisko, telefon, mail, dwa przyciski („Zobacz impulseo.pl →”, „Sprawdź nas w KRS”), szary wiersz z `KRS 0001255164`. Coś brakuje → wyczyść i wklej jeszcze raz.
5. **„Domyślne ustawienia podpisu”:** przy „Dla nowych e-maili użyj” i „Przy odpowiedzi/przekazywaniu użyj” wybierz ten podpis. Zaznacz „Wstaw podpis przed cytowanym tekstem w odpowiedziach i usuń poprzedzający wiersz --”.
6. Na samym dole strony kliknij **„Zapisz zmiany”**.
7. **Sprawdzenie:** kliknij „Utwórz” i zobacz, czy stopka sama pojawia się w nowym mailu i stoi po lewej. Zamknij pusty szkic (krzyżyk). Nic nie wysyłaj.
8. **Telefon:** aplikacja Gmail w telefonie nie bierze podpisu z komputera. Pokaż człowiekowi treść `stopka-<imię>.txt` i powiedz, gdzie ją wkleić: aplikacja Gmail → Ustawienia → konto → „Podpis mobilny”.
9. Zamelduj krótko: co ustawione, czy sprawdzenie w punkcie 7 wyszło dobrze.
