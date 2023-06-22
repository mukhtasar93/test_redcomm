Instructions for use/ installation:

Backend:
1. Make sure the local server and MySQL services are running
2. Make a MySQL database with the name: "lara_test_redcomm"
3. Open the terminal and go to the directory: test_stickynotes/backend
4. Install packages: "composer install"
4. Run migration and seeder: "php artisan migrate:refresh --seed"
5. Run Laravel backend application: "php artisan serve"
6. Open the browser and go to: "http://localhost:8000/" or "http://127.0.0.1:8000/" to welcome page application
7. Open the browser and go to: "http://localhost:8000/api/notes" or "http://127.0.0.1:8000/api/notes" to see APIs of notes (JSON data)

Frontend:
1. Open the new terminal and go to the directory: test_stickynotes/frontend
2. Install packages: "npm install"
3. Run Nuxt frontend application: "npm run dev"
4. Open the browser and go to: "http://localhost:3000/" to see frontend of the sticky-note application
5. In this application you can see some notes inserted with the seeder.
6. You can add, update, and delete the note.

Note:
Laravel 10.13.5 with PHP 8.2.0
Nuxt 3.5 with NodeJS 18.13.0
