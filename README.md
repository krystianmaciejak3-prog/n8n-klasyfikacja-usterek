# Klasyfikacja usterek maszyn z AI – n8n

## Cel projektu
Automat służy do wstępnej klasyfikacji zgłoszeń usterek maszyn przemysłowych jako PILNE lub NIEPILNE. Projekt wykonano w ramach ćwiczeń z automatyzacji AI.

## Technologie
- n8n uruchomione w Docker Desktop
- Ollama – lokalne modele językowe
- qwen2.5:1.5b – model używany podczas wcześniejszych ćwiczeń
- qwen3.5:2b – model zastosowany w końcowej wersji
- Data Table – lokalny rejestr zgłoszeń

## Jak działa automat?
1. Manual Trigger uruchamia przepływ.
2. Edit Fields wprowadza testowy opis usterki.
3. Basic LLM Chain przekazuje opis do Ollama.
4. AI ocenia pilność i przygotowuje uzasadnienie.
5. If wybiera gałąź PILNE lub NIEPILNE.
6. Edit Fields1 / Edit Fields2 przygotowują komunikat.
7. Insert row / Insert row1 zapisują wynik w tabeli Rejestr_usterek_AI.

Workflow zawiera 9 węzłów.

## Testy modeli AI
| Przypadek | Model | Wynik |
|---|---|---|
| Niewielkie zarysowanie lakieru | qwen2.5:1.5b | Błędnie: PILNE |
| Niewielkie zarysowanie lakieru | qwen3.5:2b | Poprawnie: NIEPILNE |
| Dym, przegrzewanie i hałas silnika | qwen3.5:2b | Poprawnie: PILNE |

Pierwszy model niepoprawnie klasyfikował drobne uszkodzenie. Po zmianie modelu na qwen3.5:2b oba scenariusze testowe zakończyły się poprawnie. Nie gwarantuje to niezawodności w innych przypadkach.

## Gdzie człowiek sprawdza wynik?
Pracownik utrzymania ruchu sprawdza opis usterki, ocenę pilności i uzasadnienie zapisane w tabeli Rejestr_usterek_AI. Każda klasyfikacja jest wyłącznie propozycją AI. Ostateczną decyzję podejmuje wykwalifikowany pracownik.

## Dwa ryzyka
1. Błędna klasyfikacja AI – model może pomylić zgłoszenie pilne z niepilnym. Zabezpieczenie: weryfikacja przez człowieka i testowanie różnych scenariuszy.
2. Ujawnienie danych – eksport JSON może zawierać identyfikatory konfiguracji, a dane wejściowe mogą być poufne. Zabezpieczenie: kontrola plików przed publikacją, brak kluczy API i danych osobowych.

## Uruchamianie
1. Uruchom Docker Desktop i lokalne n8n.
2. Zaimportuj plik workflow JSON.
3. Skonfiguruj połączenie Ollama i wybierz model qwen3.5:2b.
4. Utwórz tabelę Rejestr_usterek_AI z kolumnami tekstowymi: opis_usterki, pilnosc, uzasadnienie_ai.
5. Wskaż tę tabelę w obu węzłach Insert row.
6. Uruchom Execute i sprawdź wynik w tabeli.

## Wnioski
Projekt pokazuje możliwość wspomagania utrzymania ruchu przez lokalną sztuczną inteligencję. Wybór modelu miał istotny wpływ na wyniki przeprowadzonych testów. Automat ma charakter edukacyjny i nie jest systemem bezpieczeństwa maszyny.
