## Baim - bezpieczenstwo API:

Zadania -> Idź do pliku zadania.md

Jesli chcesz, skorzystaj z naszego walkthrough na ekranie
##### If you want, you can go through exercises with the help from us - we're doing a walkthrough for some problems on the screen 

Dla osób robiących samemu: instrukcja poniżej:

instalacja:

#🧃 OWASP Juice Shop – Setup & Quickstart Guide

Welcome to the OWASP Juice Shop workshop! Follow the instructions below to get your local environment set up and running.

📋 Prerequisites

Before starting, make sure you have Node.js installed on your system.

Install Node.js (Version $\ge$ 20.x or latest LTS/Current):

Download the installer from Node.js Official Download.

⚠️ Important: Ensure you check the option to Add Node.js to PATH during installation!

Verify Installation:
Open your terminal (Terminal / Command Prompt / PowerShell) and verify:

node -v
npm -v


🚀 Step-by-Step Installation

1. Clone the Repository

Clone the shallow copy of the repository for faster download:

git clone https://github.com/juice-shop/juice-shop.git --depth 1


2. Navigate to the Project Directory

cd juice-shop


3. Install Dependencies

Install all required package dependencies (this only needs to be run before the first start or after updating source code):

npm install


4. Start the Application

Launch the local server:

npm start


5. Access the Application

Open your web browser and navigate to:

http://localhost:3000


🤝 Live Workshop & Troubleshooting

Live Walkthrough: Feel free to follow along with the exercises on-screen during the workshop presentation.

Alternative API / Connection Issues: If you encounter local runtime issues or installation problems, you can safely connect to a peer's running instance. Replace localhost with your colleague's IP address:

http://<COLLEAGUE_IP>:3000


🛠️ Quick Command Reference

Action

Command

Clone Repo

git clone https://github.com/juice-shop/juice-shop.git --depth 1

Enter Folder

cd juice-shop

Install Packages

npm install

Run Server

npm start


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

Metoda w API: Wyciągnij klucz sekretny z kodu aplikacji/repozytorium (jwtSecret), wygeneruj własny token JWT dla konta admin@juice-sh.op i przekaż go w nagłówku API.
