# Baim - bezpieczenstwo API:

Zadania -> Idź do pliku zadania.md
Polecenia -> http://localhost:3000/#/score-board

Jesli chcesz, skorzystaj z naszego walkthrough na ekranie
## Opis projektu 

Projekt dotyczy bezpieczeństwa API, skupiając się na zagrożeniach, zabezpieczeniach oraz testowaniu w oparciu o wytyczne Trend Micro i OWASP.

* Prezentacja wyjaśnia działanie API, gdzie aplikacja wysyła żądanie do określonego endpointu, a serwer zwraca odpowiednie dane.


* Wyróżniono trzy kluczowe obszary ochrony: poufność, integralność oraz dostępność danych.


* Omówiono procesy uwierzytelniania, czyli weryfikacji tożsamości, oraz autoryzacji kontrolującej uprawnienia do zasobów.


* Mapa ryzyk OWASP dzieli zagrożenia na kategorie związane z tożsamością, zasobami, integracjami oraz konfiguracją systemu.


* Szczególnym zagrożeniem jest BOLA, czyli podatność polegająca na braku odpowiedniej kontroli autoryzacji dla konkretnych obiektów.


* Projekt kładzie nacisk na prawidłową ochronę tokenów JWT, stosowanie zasady minimalnych uprawnień oraz unikanie trzymania sekretów w URL.


* Zmiana pól oraz funkcji administracyjnych wymaga ścisłej weryfikacji uprawnień bezpośrednio po stronie serwera.


* Usługi są chronione przed przeciążeniem za pomocą limitów częstotliwości żądań zwracających błąd 429.


* Kontrola danych z zewnątrz obejmuje zapobieganie iniekcjom oraz atakom typu SSRF na zewnętrze API.


* Istotne jest także usuwanie zapomnianych wersji API oraz prowadzenie aktualnego spisu wszystkich endpointów.


* Warstwy ochrony obejmują szyfrowanie TLS, bramy API, WAF, reguły biznesowe aplikacji oraz stały monitoring.


* Testy bezpieczeństwa sprawdzają scenariusze odmowy dostępu w przypadku braku tokenu lub niewłaściwych uprawnień.


* System monitoringu rejestruje zdarzenia i wykrywa sygnały ostrzegawcze, takie jak wielokrotne próby niedozwolonego odczytu.


* Praktyka autoryzacji opiera się na odrzucaniu nieautoryzowanych żądań bez ujawniania poufnych informacji o zasobach.


* Pierwsze kroki dla zespołu obejmują stworzenie spisu API, audyt uprawnień, konfigurację limitów oraz wycofanie starych wersji.


* Bezpieczeństwo wymaga ciągłej weryfikacji tożsamości, kontroli uprawnień oraz wykrywania nadużyć.


* Dokumentacja opiera się na zestawieniu OWASP API Security Top 10 z 2023 roku.


* Źródłami projektu są materiały edukacyjne oraz dobre praktyki udostępnione przez Trend Micro i OWASP.

* 
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

ny token JWT dla konta admin@juice-sh.op i przekaż go w nagłówku API.
