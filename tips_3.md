Zadanie **JWT Unsigned / Alg: None** wykorzystuje podatność bibliotek obsługujących tokeny JSON Web Token (JWT), które bezkrytycznie akceptują algorytm `"none"`. Oznacza to, że serwer pomija weryfikację podpisu cyfrowego i ufa danym zawartym w ładunku (payload), o ile nagłówek określa brak algorytmu szyfrującego.

Struktura tokena JWT składa się z trzech części rozdzielonych kropkami: `NAGŁÓWEK.ŁADUNEK.PODPIS` (zazwyczaj zakodowanych w Base64URL).

1. **Zaloguj się na zwykłe konto i pobierz token JWT:** Pobranie oryginalnego tokena.
Zaloguj się w Juice Shop na dowolne zwykłe konto (np. `test@test.com`). Otwórz narzędzia deweloperskie przeglądarki (**F12** -> zakładka **Application / Aplikacja** -> **Local Storage**) i skopiuj wartość klucza `token` lub przechwyć nagłówek `Authorization: Bearer <token>` z dowolnego zapytania HTTP.


2. **Zdekoduj strukturę tokena:** Narzędzie: jwt.io, CyberChef lub Burp Suite.
Rozbij pobrany token na części i zdekoduj z formatu Base64URL jego nagłówek (Header) oraz ładunek (Payload).

Oryginalny nagłówek wygląda zazwyczaj tak:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}

```


3. **Zmodyfikuj treść nagłówka oraz ładunku:** Modyfikacja algorytmu i tożsamości.
1. Zmień w **nagłówku** wartość pola `"alg"` z `"HS256"` na `"none"` (w niektórych podatnych bibliotekach wielkość liter ma znaczenie, np. `"none"`, `"None"` lub `"NONE"`):

```json
{
  "alg": "none",
  "typ": "JWT"
}

```

2. W **ładunku (Payload)** zmień dane użytkownika na konto administratora (np. podmień e-mail na `admin@juice-sh.op` lub zaktualizuj pola roli/ID):

```json
{
  "email": "admin@juice-sh.op",
  "id": 1,
  "role": "admin"
}

```


4. **Zakoduj części i usuń podpis:** Format: Base64URL(Header).Base64URL(Payload)..
Zakoduj zmodyfikowany nagłówek oraz ładunek z powrotem do formatu **Base64URL** (upewnij się, że zakodowane ciągi nie zawierają znaków `=` na końcu).

Połącz obie części kropką i **pozostaw pustą sekcję podpisu na końcu** (kropka na końcu musi pozostać):
`eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJlbWFpbCI6ImFkbWluQGp1aWNlLXNoLm9wIiwiaWQiOjEsInJvbGUiOiJhZG1pbiJ9.`


5. **Podmień token i przetestuj dostęp:**
Wyślij dowolne żądanie do API (np. w **Burp Repeater** do endpointu `/rest/user/whoami` lub `/api/Users`) przekazując Twój sfałszowany token w nagłówku:
`Authorization: Bearer <twój_sfałszowany_token_z_kropką_na_końcu>`

Alternatywnie podmień wartość `token` w **Local Storage** przeglądarki i odśwież stronę.


6. **Potwierdź rozwiązanie zadania:**
Backend zaakceptuje niepodpisany token i zidentyfikuje Cię jako użytkownika `admin@juice-sh.op`, a w aplikacji wyzwoli się powiadomienie o sukcesie.
