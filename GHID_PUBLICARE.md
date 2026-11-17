# Tribus: cum ajunge pe Google Play

Totul e pregătit: jocul, proiectul Android (Capacitor), iconițele, ecranul de pornire, cheia de semnare, textele din magazin în ES/EN/RO, capturile de ecran și politica de confidențialitate. Rămân câțiva pași care trebuie făcuți din contul tău.

## 1. Compilarea aplicației (o dată, ~10 minute)

### Varianta A: GitHub, fără să instalezi nimic (recomandat)
1. Pe github.com creezi un repository **privat** gol, numit `triburi-android`.
2. Îmi spui că l-ai creat. Eu urc proiectul și compilarea pornește singură prin GitHub Actions (gratuit).
3. Adaugi două secrete în repository (Settings → Secrets and variables → Actions):
   - `KEYSTORE_BASE64` = conținutul fișierului `tribus-upload.jks.base64.txt`
   - `KEYSTORE_PASSWORD` = parola din `keystore-password.txt`
4. În tab-ul **Actions**, la ultima rulare, descarci `tribus-android`. Arhiva conține:
   - `app-release.aab`: pentru Google Play
   - `app-debug.apk`: îl instalezi direct pe S24 ca să testezi

### Varianta B: Android Studio (gratuit)
1. Instalezi Android Studio și deschizi folderul `android/`.
2. Build → Generate Signed App Bundle → folosești `tribus-upload.jks`, alias `tribus` și parola din `keystore-password.txt`.

⚠️ **Păstrează `tribus-upload.jks` și parola în siguranță**, de exemplu într-un manager de parole. Fără ele nu mai poți publica actualizări.

## 2. Google Play Console
1. **Creează aplicația**: nume `Tribus: Del fuego a las estrellas`, limba implicită spaniolă, tip Joc, **Plătită**.
2. **Configurează aplicația**: răspunsurile sunt în `store/ficha_google_play.md`, în tabelul de la final.
   - Politica de confidențialitate: publici `docs/privacy.html` (GitHub Pages din repository, sau orice link public) și pui linkul. Înlocuiește întâi `[TU_EMAIL_DE_CONTACTO]` cu emailul pe care vrei să-l folosești public.
   - Clasificarea conținutului: completezi chestionarul (violență de fantezie ușoară, fără sânge, fără chat, fără cumpărături).
   - Siguranța datelor: „Nu colectează date”.
3. **Pagina din magazin**, în trei limbi: textele sunt în `store/ficha_google_play.md`.
   - Iconiță: `store/icon_512.png`
   - Banner: `store/feature_1024x500.png`
   - Capturi telefon: `store/shots/es_*.png` (spaniolă) și `en_*.png` (engleză)
4. **Prețul**: Monetizare → Prețul aplicației. Ai nevoie de un cont de comerciant (Google Payments), legat de datele tale fiscale.
5. **Testare**: Google cere pentru conturile noi de dezvoltator un **test închis cu cel puțin 12 testeri timp de 14 zile** înainte de producție. Încarci AAB-ul în „Testare închisă”, adaugi emailurile (prieteni, familie) și aștepți cele 14 zile.
6. După test: promovezi versiunea în **Producție** și o trimiți la verificare (de obicei 1–7 zile).

## 3. Actualizări
- Modifici jocul, îl copiezi în `www/index.html`, crești `versionCode` în `android/app/build.gradle` (1 → 2 → 3…) și compilezi din nou.

## Date tehnice
- ID aplicație: `com.cristian.tribus` (nu se mai poate schimba după publicare)
- minSdk 24 (Android 7+), targetSdk 36
- Orientare: portret · Funcționează offline · Fără permisiuni speciale
