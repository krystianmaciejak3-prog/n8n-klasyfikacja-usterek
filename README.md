# n8n – Klasyfikacja usterek maszyn z AI

## Opis projektu
Projekt automatyzacji zgłoszeń usterek maszyn przemysłowych z wykorzystaniem n8n i lokalnego modelu AI Ollama.

## Technologie
- n8n
- Docker Desktop
- Ollama
- Qwen2.5:1.5b

## Zasada działania
1. Użytkownik wprowadza opis usterki.
2. Model AI analizuje zgłoszenie.
3. Zgłoszenie otrzymuje kategorię PILNE lub NIEPILNE.
4. Węzeł IF kieruje zgłoszenie do odpowiedniej gałęzi.
5. Automat przygotowuje komunikat dla pracownika utrzymania ruchu.

## Testy
- Przegrzewający się silnik przenośnika – PILNE.
- Zarysowanie lakieru obudowy – NIEPILNE.

Oba przykłady przetestowano pomyślnie.

## Bezpieczeństwo
Projekt ma charakter edukacyjny. AI wspomaga klasyfikację zgłoszeń, ale nie steruje maszynami. Ostateczne decyzje podejmuje wykwalifikowany pracownik utrzymania ruchu.
