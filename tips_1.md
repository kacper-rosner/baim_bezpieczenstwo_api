Zadanie **View Another User's Basket** polega na wykorzystaniu podatności **BOLA** (Broken Object Level Authorization / IDOR). Backend weryfikuje Twój token tożsamości, ale nie sprawdza, czy masz prawo dostępu do konkretnego identyfikatora koszyka przekazanego w ścieżce URL.

1. **Zarejestruj i zaloguj się na konto:** Strona aplikacji http://localhost:3000.
Przejdź do formularza rejestracji (`/#/register`), załóż dowolne konto (np. `test@test.com`), a następnie zaloguj się do sklepu.


2. **Dodaj produkt do koszyka:**
Kliknij **Add to Basket** przy dowolnym przedmiocie na stronie głównej. Wygeneruje to wpis w bazie danych i powiąże ID koszyka z Twoją sesją.


3. **Włącz przechwytywanie ruchu HTTP:**
Otwórz narzędzia deweloperskie w przeglądarce (**F12** -> zakładka **Network / Sieć**) lub uruchom proxy **Burp Suite** z włączoną opcją przechwytywania (*Proxy -> Intercept*).


4. **Otwórz widok koszyka:**
Kliknij ikonę koszyka w prawym górnym rogu interfejsu sklepu, aby wyzwolić pobranie danych koszyka z API.


5. **Zlokalizuj zapytanie do endpointu /rest/basket/:**
W liście zapytań sieciowych znajdź żądanie typu `GET` skierowane na adres:
`http://localhost:3000/rest/basket/{id}` (np. `/rest/basket/2`).

Zwróć uwagę, że w nagłówkach żądania przesłano Twój token dostępowy (`Authorization: Bearer <token>`).


6. **Zmień identyfikator koszyka w ścieżce:**
Prześlij to zapytanie do ponownego wykonania (np. za pomocą narzędzia **Burp Repeater** lub edytując zapytanie w konsoli przeglądarki). Zmień cyfrę na końcu adresu URL z własnego ID (np. `2`) na inny identyfikator (np. `1` lub `3`).


7. **Zweryfikuj odpowiedź JSON:**
Wyślij zmodyfikowane zapytanie `GET /rest/basket/1`. Serwer zwróci odpowiedź z kodem statusu **200 OK** oraz strukturą JSON zawierającą przedmioty należące do innego użytkownika. W aplikacji pojawi się powiadomienie o rozwiązaniu zadania.
