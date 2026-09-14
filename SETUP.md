# Uurstaat instellen

Deze app staat online, maar heeft nog jouw eigen Firebase-project nodig voor het
opslaan/synchroniseren van je uren. Dit doe je één keer.

## 1. Firebase-project aanmaken

1. Ga naar https://console.firebase.google.com en log in met je Google-account.
2. Klik **"Project toevoegen"**, geef het een naam (bv. `uurstaat`), en maak het
   aan (Google Analytics mag je uitschakelen, dat heb je niet nodig).

## 2. Inloggen aanzetten

1. Ga in het project naar **Build > Authentication > Get started**.
2. Kies **"Email/Password"** in de lijst met providers, zet hem op **Enable**,
   en bewaar.

## 3. Database aanmaken

1. Ga naar **Build > Firestore Database > Create database**.
2. Kies een regio in de buurt (bv. `europe-west1` of `eur3`) en start in
   **production mode**.
3. Ga naar het tabblad **Rules** en vervang de inhoud door dit (zo kan enkel
   jij, ingelogd, bij je eigen uren):

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid}/{document=**} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```
4. Klik **Publish**.

## 4. Je app-configuratie ophalen

1. Ga naar **Project settings** (tandwiel-icoon linksboven) > tab **General**.
2. Scroll naar **"Your apps"** en klik het web-icoon `</>`.
3. Geef een bijnaam (bv. `uurstaat-web`) en klik **Register app**.
4. Je krijgt een blokje code met `const firebaseConfig = { ... }`. Kopieer die
   waarden naar `firebase-config.js` in dit project, op de plek van
   `"VUL_HIER_IN"`.

## 5. Online zetten

Zodra `firebase-config.js` is ingevuld, commit en push je de wijziging naar
GitHub (of laat Claude dit doen) — de live site update dan automatisch via
GitHub Pages.

## 6. Account aanmaken in de app

Open de site, kies **"Nog geen account? Account aanmaken"**, vul je
e-mailadres en een wachtwoord in. Dat account gebruik je voortaan op elk
toestel om in te loggen — je uren volgen automatisch mee.
