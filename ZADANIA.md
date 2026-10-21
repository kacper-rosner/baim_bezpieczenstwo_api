
# Zadania: 

http://127.0.0.1:3000/#/score-board

w zależności od tego, jak jesteś zaawansowany w takich rzeczach, możesz robić zadania o dowolnej trudności.

Proponowane zadania:

1. BOLA / IDOR (Broken Object Level Authorization)
Podatność polegająca na braku weryfikacji, czy zalogowany użytkownik ma prawo do zasobu o danym ID.

View Another User's Basket

Kategoria: BOLA / IDOR

Cel: Przejrzyj zawartość koszyka zakupowego innego użytkownika.

Metoda w API: Po zalogowaniu przechwyć zapytanie GET /rest/basket/<ID> i zmień identyfikator koszyka w ścieżce na inny (np. 1, 2, 3).

Access Other User's Order History

Kategoria: BOLA

Cel: Uzyskaj dostęp do historii zamówień innego klienta.

Metoda w API: Zmodyfikuj parametr identyfikatora zamówienia / użytkownika w zapytaniach do ścieżek /rest/order-history/....

2. Mass Assignment / Broken Property Level Authorization
Sytuacja, w której API przyjmuje i zapisuje więcej pól JSON niż powinno (np. pola uprawnień).

Admin Registration (Mass Assignment)

Kategoria: Mass Assignment / Escalation of Privilege

Cel: Zarejestruj konto bezpośrednio z uprawnieniami administratora.

Metoda w API: Przechwyć zapytanie rejestracyjne POST /api/Users/ i dopisz do obiektu JSON pole z rolą: "role": "admin".

Forged Review / User Impersonation

Kategoria: Property Level Authorization

Cel: Dodaj recenzję produktu w imieniu innego użytkownika.

Metoda w API: Podczas wysyłania opinii przez PUT /api/Feedbacks/ lub POST /api/Products/1/reviews podmień pole UserId / author na e-mail lub ID innego użytkownika.

3. Broken Authentication & JWT Vulnerabilities
Wady w mechanizmach uwierzytelniania oraz weryfikacji tokenów API.

JWT Unsigned / Alg: None

Kategoria: Broken Authentication

Cel: Zaloguj się jako administrator bez znajomości jego hasła, modyfikując token JWT.

Metoda w API: Pobierz swój token JWT z nagłówka Authorization: Bearer <token>, zdekoduj go, zmień algorytm w nagłówku na "alg": "none" (lub zresetuj podpis) i zmień nazwę użytkownika w payloadzie na admina.

JWT Forgery (Weak Secret Key)

Kategoria: Cryptographic Flaw / JWT

Cel: Złam sekret HMAC tokena JWT i wygeneruj prawidłowy token administratora.

Metoda w API: Wyciągnij klucz sekretny z kodu aplikacji/repozytorium (jwtSecret), wygeneruj włas
