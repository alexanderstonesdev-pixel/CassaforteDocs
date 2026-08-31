# FAQ — Cassaforte / Vault

Sei lingue (IT, EN, FR, DE, ES, PT). Struttura ispirata alla FAQ di un
concorrente noto (Sgallery), ma riscritta sulla **nostra** realtà: crittografia
reale, zero account, zero server, nessuna backdoor, e il vault che **non**
sopravvive alla disinstallazione senza un backup.

Destinazione: scheda Play Store (link in descrizione) **e** schermata in-app
("Impostazioni → FAQ"). La versione in-app è più sintetica; questa pagina è la
versione estesa.

---

## IT

### Accesso e recupero

**Ho dimenticato il PIN. Come rientro?**
Se hai impostato un **codice di recupero** o le **domande di sicurezza**
(Impostazioni → "Recupero dell'accesso"), oppure se hai un **file di backup
`.csfbk`**, puoi rientrare e scegliere un nuovo PIN. Senza nessuno di questi, i
file **non** sono recuperabili: la crittografia è reale e la chiave deriva solo
dal tuo PIN. Nemmeno noi possiamo decifrarli — non è un limite, è il punto
dell'app.

**Il codice di recupero è una specie di password universale / backdoor?**
No. Il codice di recupero, il PIN e le risposte alle domande di sicurezza sono
tre "serrature" indipendenti sulla stessa chiave: ognuna la apre da sola, ma la
chiave resta cifrata e sul dispositivo. Non esiste un codice segreto valido per
tutte le installazioni (a differenza di alcune app concorrenti che usano un PIN
fisso come `11223344`).

**Quanti tentativi ho per il PIN?**
Cinque. Dopo il quinto errore parte una pausa che cresce ad ogni tentativo
sbagliato (30 secondi, poi 1, 5, 15 minuti). **Nessuna cancellazione dei dati**:
un errore onesto non ti fa perdere le foto.

**Ho attivato il travestimento (Calcolatrice/Meteo) e non riesco più a entrare.**
Con l'icona "Calcolatrice": apri l'app, digita il PIN come fosse un calcolo e
premi `=`. Con "Meteo": apri l'app e tieni premuto a lungo sulla temperatura.
Il tutorial al primo avvio lo spiega; la scheda Play Store e il primo avvio
restano comunque a nome "Cassaforte".

### Dove finiscono le foto

**Dopo aver importato una foto nella cassaforte, dove viene salvata?**
In uno spazio privato dell'app (`/data/data/…`), **non** accessibile ad altre
app né a un file manager, e **non** in una cartella visibile nella memoria del
telefono. Alcune app concorrenti creano una cartella tipo `.privacy_safe` nella
root: noi no, apposta — una cartella del genere svela la cassaforte e i file
dentro sono spesso recuperabili con strumenti banali.

**Il file è cifrato davvero o è solo nascosto dietro un PIN?**
Cifrato davvero: **AES-256-GCM**, chiave a 256 bit derivata dal PIN con
PBKDF2-SHA256 (600.000 iterazioni). Anche estraendo i file dallo storage
dell'app (serve un telefono con i permessi di root) si ottiene solo dati cifrati.

**Voi potete vedere le mie foto? Ci sono su un vostro server?**
No. Nessun account, nessun server nostro, nessun caricamento. Le uniche
connessioni di rete sono la pubblicità (solo versione gratuita) e — solo se usi
il travestimento "Meteo" — un servizio meteo pubblico che non tocca mai il
vault.

### Import ed export

**Ho aggiunto una foto alla cassaforte ma è ancora nella galleria del telefono.**
Questo è il punto più importante, leggilo tutto. Dopo aver cifrato la foto, l'app
chiede di **eliminare l'originale dal telefono**: viene cancellato
definitivamente, senza passare dal cestino di sistema. Ma:

- Se **annulli** quella richiesta, l'originale resta nella galleria. L'app te lo
  segnala.
- Se hai un **servizio di sincronizzazione cloud** attivo (Google Foto, Samsung
  Cloud, Xiaomi Cloud / "Galleria condivisa" di MIUI, HiCloud di Huawei), una
  **copia dell'originale può essere già stata caricata** o venire **ripristinata
  in automatico** dopo la rimozione. In questo caso: controlla l'album di
  sistema e il **cestino del cloud**, cancella l'originale anche da lì, e valuta
  di disattivare la sincronizzazione per le foto che metti in cassaforte.
- Alcune app Galleria di terze parti (soprattutto Samsung, Xiaomi) tengono un
  **cestino proprio** che intercetta comunque la cancellazione: se lo usi,
  svuotalo dopo l'import.

**Alcune foto o video non compaiono quando provo ad aggiungerli.**
L'app usa il selettore foto di sistema, che mostra solo file già presenti nella
libreria multimediale. Se un file non appare (per esempio scaricato di recente o
in una cartella non indicizzata): aprilo una volta nella galleria, oppure
condividilo verso Cassaforte dal file manager, oppure usa "Documenti" per i file
che non sono foto/video.

**Come tiro fuori una foto dalla cassaforte?**
Aprila e usa "In galleria": viene decifrata e reinserita nella galleria di
sistema. La copia cifrata resta nel vault finché non la elimini.

**Posso scattare foto o video dentro l'app?**
Sì. Tocca l'icona della fotocamera in alto e scegli "Scatta una foto" o
"Registra un video". Si apre la fotocamera del telefono; lo scatto viene cifrato
direttamente nel vault (foto nella cartella Foto, video in Video) e non passa mai
dalla galleria del telefono, quindi non lascia nessuna copia in chiaro.

**La cifratura o la decifratura ci mette molto.**
Dipende dalla dimensione del file e dalla potenza del telefono. Un video da
centinaia di MB richiede qualche secondo. L'operazione avviene tutta sul
dispositivo, senza rete.

### Cestino e perdita dei file

**Ho eliminato una foto per sbaglio.**
Gli elementi eliminati restano nel **Cestino** per 7 giorni: aprilo da
Impostazioni → Cestino e premi "Ripristina". Dopo 7 giorni vengono cancellati
per sempre.

**Perché l'app elimina gli originali dalla galleria?**
Perché altrimenti la cassaforte non serve a niente: la foto sarebbe cifrata nel
vault *e* in chiaro nella galleria. L'eliminazione è definitiva (non passa dal
cestino di sistema), quindi assicurati di avere l'originale già cifrato nel vault
prima di confermare.

**Come faccio a essere sicuro di non perdere mai i file?**
Un solo consiglio, ed è serio: **fai backup regolari**. Impostazioni → "Backup e
migrazione" → "Esporta backup" crea un unico file `.csfbk` (tutto il vault, già
cifrato, più le chiavi) da salvare su una chiavetta, una scheda SD o il tuo
cloud personale. Un telefono si può rompere, perdere o resettare: il backup è
l'unica vera rete di sicurezza.

### Cambio telefono

**Come sposto le foto su un telefono nuovo?**
Sul vecchio: Impostazioni → "Esporta backup" → salva il file `.csfbk` dove
vuoi. Sul nuovo: installa Cassaforte, al primo avvio scegli "Ho già un backup",
seleziona il file. Ti servirà **lo stesso PIN** di prima.

**Se disinstallo l'app perdo tutto?**
Sì. A differenza di alcune app concorrenti, che lasciano una cartella nella
memoria del telefono e "ritrovano" i file alla reinstallazione, qui il vault sta
nello storage privato dell'app: **la disinstallazione lo cancella**. Prima di
disinstallare (o di cambiare telefono, o di fare un reset) **esporta un backup**.

### Foto dell'intruso (intruder selfie)

**Come funziona?**
Opzione **disattivata di serie**. Se la attivi (Impostazioni → "Foto
dell'intruso"), dopo **3 PIN errati** l'app scatta in silenzio una foto con la
fotocamera frontale — nessuna anteprima, nessun suono. La foto viene cifrata
dentro il vault e la vedi in "Vedi i tentativi di accesso".

**L'ho attivata ma non scatta.**
Controlla che: il permesso Fotocamera sia concesso (Impostazioni di sistema →
App → Cassaforte → Autorizzazioni); il telefono abbia una fotocamera frontale;
la funzione non sia stata bloccata da restrizioni di risparmio energetico
aggressive (vedi la sezione successiva su Xiaomi/Huawei). Su alcuni telefoni
Oppo/Vivo/Huawei molto restrittivi lo scatto in background può non partire.

### Telefoni Xiaomi, Huawei, Oppo, Vivo, Samsung

Questi produttori sono più aggressivi degli altri nel chiudere le app in
background e nel "pulire" i dati. Due cose da sapere:

**1. Sincronizzazione cloud che ripristina gli originali.**
MIUI (Xiaomi), EMUI (Huawei) e le rispettive galleria-cloud a volte
**ripristinano** un file appena rimosso dalla galleria, o ne hanno già una
copia nel cloud. Dopo aver messo delle foto in cassaforte, controlla l'album di
sistema e il **cestino del servizio cloud** e cancella lì gli originali. Se ti
capita spesso, disattiva la sincronizzazione automatica della galleria.

**2. App di "sicurezza" e "pulizia" che cancellano i dati.**
Gli strumenti tipo *Sicurezza* / *Gestione telefono* / *Pulizia* di
Xiaomi/Huawei possono cancellare i dati privati di un'app se la considerano
"inattiva", e questo **cancellerebbe il vault**. Per evitarlo:

- Blocca Cassaforte nella schermata delle app recenti (icona lucchetto).
- Attiva **Avvio automatico** per Cassaforte (MIUI: Sicurezza → Autorizzazioni →
  Avvio automatico; EMUI: Impostazioni → App → Avvio app).
- Togli Cassaforte dall'ottimizzazione batteria / mettila su "Nessuna
  restrizione".
- Escludi Cassaforte dagli strumenti di pulizia automatica.

Anche facendo tutto questo, la regola numero uno resta: **fai backup regolari**
del file `.csfbk`. Nessuna impostazione di sistema è affidabile al 100%.

### Pubblicità e Premium

**Che pubblicità c'è nella versione gratuita?**
Un annuncio a schermo intero (saltabile dopo pochi secondi), non più di una
volta ogni ~4 minuti di uso, e **solo** sulla griglia principale — mai durante
import, export o visualizzazione di un file. Nessun banner permanente.

**Cosa sblocca il Premium?**
Toglie la pubblicità. Pagamento **unico** (~12,99 €), nessun abbonamento. I file
sono **illimitati** anche nella versione gratuita.

**Ho cambiato telefono / reinstallato: come recupero il Premium?**
Impostazioni → "Ripristina acquisti". L'acquisto è legato al tuo account Google
Play.

---

## EN

### Access and recovery

**I forgot my PIN. How do I get back in?**
If you set a **recovery code** or **security questions** (Settings → "Access
recovery"), or if you have a **`.csfbk` backup file**, you can get back in and
choose a new PIN. Without any of those, your files are **not** recoverable: the
encryption is real and the key is derived only from your PIN. Not even we can
decrypt them — that's the whole point of the app, not a limitation.

**Is the recovery code a kind of master password / backdoor?**
No. The recovery code, the PIN and the security-question answers are three
independent "locks" on the same key: each one opens it on its own, but the key
stays encrypted and on your device. There is no secret code that works across
installations (unlike some competing apps that use a fixed PIN such as
`11223344`).

**How many PIN attempts do I get?**
Five. After the fifth wrong PIN a pause kicks in and grows with each further
wrong attempt (30 seconds, then 1, 5, 15 minutes). **Data is never wiped**: an
honest mistake won't cost you your photos.

**I turned on the disguise (Calculator/Weather) and can't get in anymore.**
With the "Calculator" icon: open the app, type your PIN as if it were a
calculation and press `=`. With "Weather": open the app and long-press on the
temperature. The first-run tutorial explains this; the Play Store listing and
first launch always stay under the "Vault" name.

### Where your photos go

**After I import a photo into the vault, where is it stored?**
In the app's private storage (`/data/data/…`), **not** accessible to other apps
or to a file manager, and **not** in a visible folder in phone storage. Some
competing apps create a folder like `.privacy_safe` in the root: we don't, on
purpose — such a folder reveals the vault and the files inside are often
recoverable with trivial tools.

**Is the file really encrypted, or just hidden behind a PIN?**
Really encrypted: **AES-256-GCM**, 256-bit key derived from the PIN with
PBKDF2-SHA256 (600,000 iterations). Even pulling the files out of the app's
storage (which needs a rooted phone) only yields encrypted data.

**Can you see my photos? Are they on a server of yours?**
No. No account, no server of ours, no upload. The only network connections are
ads (free version only) and — only if you use the "Weather" disguise — a public
weather service that never touches the vault.

### Import and export

**I added a photo to the vault but it's still in my phone gallery.**
This is the most important point, read all of it. After encrypting the photo,
the app asks to **delete the original from the phone**: it is removed
permanently, without going through the system trash. But:

- If you **cancel** that request, the original stays in the gallery. The app
  tells you.
- If you have a **cloud sync service** on (Google Photos, Samsung Cloud, Xiaomi
  Cloud / MIUI "Shared gallery", Huawei HiCloud), a **copy of the original may
  already be uploaded** or may be **automatically restored** after removal. In
  that case: check the system album and the **cloud trash**, delete the
  original there too, and consider turning off sync for the photos you put in
  the vault.
- Some third-party Gallery apps (Samsung, Xiaomi especially) keep their **own
  trash** that intercepts the deletion anyway: if you use one, empty it after
  the import.

**Some photos or videos don't show up when I try to add them.**
The app uses the system photo picker, which only shows files already in the
media library. If a file doesn't appear (e.g. recently downloaded, or in a
non-indexed folder): open it once in the gallery, or share it to Vault from the
file manager, or use "Documents" for files that aren't photos/videos.

**How do I take a photo back out of the vault?**
Open it and use "To gallery": it's decrypted and put back into the system
gallery. The encrypted copy stays in the vault until you delete it.

**Can I take photos or videos inside the app?**
Yes. Tap the camera icon at the top and pick "Take a photo" or "Record a video".
The phone camera opens; the capture is encrypted straight into the vault (photos
in the Photos folder, videos in Videos) and never goes through the phone gallery,
so it leaves no clear copy.

**Encryption or decryption takes a long time.**
It depends on file size and phone power. A video of several hundred MB takes a
few seconds. Everything happens on-device, with no network.

### Trash and losing files

**I deleted a photo by mistake.**
Deleted items stay in the **Trash** for 7 days: open it from Settings → Trash
and tap "Restore". After 7 days they're deleted for good.

**Why does the app delete originals from the gallery?**
Because otherwise the vault is pointless: the photo would be encrypted in the
vault *and* in the clear in the gallery. The deletion is permanent (it does not
go through the system trash), so make sure the original is already encrypted in
the vault before you confirm.

**How do I make sure I never lose my files?**
One piece of advice, and it's serious: **make regular backups**. Settings →
"Backup and migration" → "Export backup" creates a single `.csfbk` file (the
whole vault, already encrypted, plus the keys) to save on a USB stick, an SD
card or your personal cloud. A phone can break, get lost or be reset: the backup
is the only real safety net.

### New phone

**How do I move my photos to a new phone?**
On the old one: Settings → "Export backup" → save the `.csfbk` file wherever you
want. On the new one: install Vault, on first launch choose "I already have a
backup", pick the file. You'll need **the same PIN** as before.

**If I uninstall the app, do I lose everything?**
Yes. Unlike some competing apps, which leave a folder in phone storage and
"find" the files again on reinstall, here the vault lives in the app's private
storage: **uninstalling deletes it**. Before uninstalling (or switching phones,
or doing a reset) **export a backup**.

### Intruder selfie

**How does it work?**
**Off by default.** If you enable it (Settings → "Intruder photo"), after **3
wrong PINs** the app silently takes a photo with the front camera — no preview,
no sound. The photo is encrypted inside the vault and shown in "View access
attempts".

**I enabled it but it doesn't take a photo.**
Check that: the Camera permission is granted (System Settings → Apps → Vault →
Permissions); the phone has a front camera; the feature hasn't been blocked by
aggressive battery-saving restrictions (see the next section on Xiaomi/Huawei).
On some very restrictive Oppo/Vivo/Huawei phones the background capture may not
fire.

### Xiaomi, Huawei, Oppo, Vivo, Samsung phones

These makers are more aggressive than others at killing background apps and
"cleaning" data. Two things to know:

**1. Cloud sync that restores originals.**
MIUI (Xiaomi), EMUI (Huawei) and their cloud galleries sometimes **restore** a
file right after it's removed from the gallery, or already hold a copy in the
cloud. After putting photos in the vault, check the system album and the
**cloud service's trash** and delete the originals there. If it keeps
happening, turn off automatic gallery sync.

**2. "Security" and "cleaner" apps that wipe data.**
Tools like *Security* / *Phone Manager* / *Cleaner* on Xiaomi/Huawei can wipe an
app's private data if they think it's "inactive", and that **would wipe the
vault**. To prevent this:

- Lock Vault in the recent-apps screen (padlock icon).
- Enable **Autostart** for Vault (MIUI: Security → Permissions → Autostart;
  EMUI: Settings → Apps → App launch).
- Remove Vault from battery optimization / set it to "No restrictions".
- Exclude Vault from automatic cleaner tools.

Even with all of this, rule number one still stands: **make regular backups** of
the `.csfbk` file. No system setting is 100% reliable.

### Ads and Premium

**What ads are in the free version?**
One full-screen ad (skippable after a few seconds), no more than once every ~4
minutes of use, and **only** on the main grid — never during import, export or
while viewing a file. No permanent banner.

**What does Premium unlock?**
It removes the ads. **One-time** payment (~€12.99), no subscription. Files are
**unlimited** in the free version too.

**I switched phones / reinstalled: how do I get Premium back?**
Settings → "Restore purchases". The purchase is tied to your Google Play
account.

---

## FR

### Accès et récupération

**J'ai oublié mon PIN. Comment revenir ?**
Si vous avez défini un **code de récupération** ou des **questions de sécurité**
(Paramètres → « Récupération de l'accès »), ou si vous avez un **fichier de
sauvegarde `.csfbk`**, vous pouvez revenir et choisir un nouveau PIN. Sans aucun
de ces éléments, vos fichiers sont **irrécupérables** : le chiffrement est réel
et la clé dérive uniquement de votre PIN. Nous non plus ne pouvons pas les
déchiffrer — ce n'est pas une limite, c'est tout l'intérêt de l'application.

**Le code de récupération est-il une sorte de mot de passe universel / porte dérobée ?**
Non. Le code de récupération, le PIN et les réponses aux questions de sécurité
sont trois « serrures » indépendantes sur la même clé : chacune l'ouvre seule,
mais la clé reste chiffrée et sur votre appareil. Il n'existe aucun code secret
valable pour toutes les installations (contrairement à certaines applications
concurrentes qui utilisent un PIN fixe comme `11223344`).

**Combien de tentatives ai-je pour le PIN ?**
Cinq. Après la cinquième erreur, une pause démarre et s'allonge à chaque nouvelle
tentative erronée (30 secondes, puis 1, 5, 15 minutes). **Aucune suppression de
données** : une erreur honnête ne vous fait pas perdre vos photos.

**J'ai activé le déguisement (Calculatrice/Météo) et je n'arrive plus à entrer.**
Avec l'icône « Calculatrice » : ouvrez l'application, tapez le PIN comme un
calcul et appuyez sur `=`. Avec « Météo » : ouvrez l'application et faites un
appui long sur la température. Le tutoriel du premier lancement l'explique ; la
fiche Play Store et le premier lancement restent au nom « Vault ».

### Où vont les photos

**Après avoir importé une photo dans le coffre, où est-elle enregistrée ?**
Dans l'espace privé de l'application (`/data/data/…`), **non** accessible aux
autres applications ni à un gestionnaire de fichiers, et **pas** dans un dossier
visible de la mémoire du téléphone. Certaines applications concurrentes créent un
dossier type `.privacy_safe` à la racine : nous ne le faisons pas, volontairement
— un tel dossier révèle le coffre et les fichiers qu'il contient sont souvent
récupérables avec des outils basiques.

**Le fichier est-il vraiment chiffré, ou juste caché derrière un PIN ?**
Vraiment chiffré : **AES-256-GCM**, clé de 256 bits dérivée du PIN avec
PBKDF2-SHA256 (600 000 itérations). Même en extrayant les fichiers du stockage de
l'application (il faut un téléphone rooté), on n'obtient que des données
chiffrées.

**Pouvez-vous voir mes photos ? Sont-elles sur un de vos serveurs ?**
Non. Aucun compte, aucun serveur de notre part, aucun envoi. Les seules
connexions réseau sont la publicité (version gratuite uniquement) et — seulement
si vous utilisez le déguisement « Météo » — un service météo public qui ne touche
jamais au coffre.

### Import et export

**J'ai ajouté une photo au coffre mais elle est toujours dans la galerie du téléphone.**
C'est le point le plus important, lisez-le en entier. Après avoir chiffré la
photo, l'application propose de **supprimer l'original du téléphone** : il est
effacé définitivement, sans passer par la corbeille du système. Mais :

- Si vous **annulez** cette demande, l'original reste dans la galerie.
  L'application vous le signale.
- Si vous avez un **service de synchronisation cloud** actif (Google Photos,
  Samsung Cloud, Xiaomi Cloud / « Galerie partagée » de MIUI, HiCloud de Huawei),
  une **copie de l'original peut déjà être envoyée** ou être **restaurée
  automatiquement** après la suppression. Dans ce cas : vérifiez l'album système
  et la **corbeille du cloud**, supprimez l'original là aussi, et envisagez de
  désactiver la synchronisation pour les photos que vous mettez au coffre.
- Certaines applis Galerie tierces (Samsung, Xiaomi surtout) gardent leur
  **propre corbeille** qui intercepte quand même la suppression : si vous en
  utilisez une, videz-la après l'import.

**Certaines photos ou vidéos n'apparaissent pas quand j'essaie de les ajouter.**
L'application utilise le sélecteur de photos du système, qui n'affiche que les
fichiers déjà présents dans la médiathèque. Si un fichier n'apparaît pas (par
exemple téléchargé récemment ou dans un dossier non indexé) : ouvrez-le une fois
dans la galerie, ou partagez-le vers Vault depuis le gestionnaire de fichiers, ou
utilisez « Documents » pour les fichiers qui ne sont pas des photos/vidéos.

**Comment sortir une photo du coffre ?**
Ouvrez-la et utilisez « Vers la galerie » : elle est déchiffrée et replacée dans
la galerie du système. La copie chiffrée reste dans le coffre jusqu'à ce que vous
la supprimiez.

**Puis-je prendre des photos ou des vidéos dans l'app ?**
Oui. Touchez l'icône appareil photo en haut et choisissez « Prendre une photo »
ou « Enregistrer une vidéo ». L'appareil photo du téléphone s'ouvre ; la prise
est chiffrée directement dans le coffre (les photos dans le dossier Photos, les
vidéos dans Vidéos) et ne passe jamais par la galerie du téléphone, elle ne
laisse donc aucune copie en clair.

**Le chiffrement ou le déchiffrement prend beaucoup de temps.**
Cela dépend de la taille du fichier et de la puissance du téléphone. Une vidéo de
plusieurs centaines de Mo prend quelques secondes. Tout se passe sur l'appareil,
sans réseau.

### Corbeille et perte de fichiers

**J'ai supprimé une photo par erreur.**
Les éléments supprimés restent dans la **Corbeille** pendant 7 jours : ouvrez-la
depuis Paramètres → Corbeille et appuyez sur « Restaurer ». Après 7 jours, ils sont
supprimés définitivement.

**Pourquoi l'application supprime-t-elle les originaux de la galerie ?**
Parce que sinon le coffre ne sert à rien : la photo serait chiffrée dans le
coffre *et* en clair dans la galerie. La suppression est définitive (elle ne
passe pas par la corbeille du système) : assurez-vous donc que l'original est
déjà chiffré dans le coffre avant de confirmer.

**Comment être sûr de ne jamais perdre mes fichiers ?**
Un seul conseil, et il est sérieux : **faites des sauvegardes régulières**.
Paramètres → « Sauvegarde et migration » → « Exporter la sauvegarde » crée un seul
fichier `.csfbk` (tout le coffre, déjà chiffré, plus les clés) à enregistrer sur
une clé USB, une carte SD ou votre cloud personnel. Un téléphone peut se casser,
se perdre ou être réinitialisé : la sauvegarde est le seul vrai filet de
sécurité.

### Nouveau téléphone

**Comment déplacer mes photos vers un nouveau téléphone ?**
Sur l'ancien : Paramètres → « Exporter la sauvegarde » → enregistrez le fichier
`.csfbk` où vous voulez. Sur le nouveau : installez Vault, au premier lancement
choisissez « J'ai déjà une sauvegarde », sélectionnez le fichier. Il vous faudra
**le même PIN** qu'avant.

**Si je désinstalle l'application, est-ce que je perds tout ?**
Oui. Contrairement à certaines applications concurrentes, qui laissent un dossier
dans la mémoire du téléphone et « retrouvent » les fichiers à la réinstallation,
ici le coffre se trouve dans le stockage privé de l'application : **la
désinstallation l'efface**. Avant de désinstaller (ou de changer de téléphone, ou
de faire une réinitialisation), **exportez une sauvegarde**.

### Photo de l'intrus (intruder selfie)

**Comment ça marche ?**
Option **désactivée par défaut**. Si vous l'activez (Paramètres → « Photo de
l'intrus »), après **3 PIN erronés** l'application prend en silence une photo
avec la caméra frontale — aucun aperçu, aucun son. La photo est chiffrée dans le
coffre et visible dans « Voir les tentatives d'accès ».

**Je l'ai activée mais elle ne prend pas de photo.**
Vérifiez que : l'autorisation Caméra est accordée (Paramètres système → Applis →
Vault → Autorisations) ; le téléphone a une caméra frontale ; la fonction n'a pas
été bloquée par des restrictions d'économie de batterie agressives (voir la
section suivante sur Xiaomi/Huawei). Sur certains téléphones Oppo/Vivo/Huawei
très restrictifs, la capture en arrière-plan peut ne pas se déclencher.

### Téléphones Xiaomi, Huawei, Oppo, Vivo, Samsung

Ces fabricants sont plus agressifs que les autres pour fermer les applications en
arrière-plan et « nettoyer » les données. Deux choses à savoir :

**1. Synchronisation cloud qui restaure les originaux.**
MIUI (Xiaomi), EMUI (Huawei) et leurs galeries-cloud **restaurent** parfois un
fichier juste après son retrait de la galerie, ou en ont déjà une copie dans le
cloud. Après avoir mis des photos au coffre, vérifiez l'album système et la
**corbeille du service cloud** et supprimez-y les originaux. Si cela arrive
souvent, désactivez la synchronisation automatique de la galerie.

**2. Applis de « sécurité » et de « nettoyage » qui effacent les données.**
Les outils type *Sécurité* / *Gestionnaire du téléphone* / *Nettoyage* de
Xiaomi/Huawei peuvent effacer les données privées d'une application s'ils la
considèrent « inactive », et cela **effacerait le coffre**. Pour l'éviter :

- Verrouillez Vault dans l'écran des applications récentes (icône cadenas).
- Activez le **Démarrage automatique** pour Vault (MIUI : Sécurité →
  Autorisations → Démarrage automatique ; EMUI : Paramètres → Applis → Lancement
  des applis).
- Retirez Vault de l'optimisation de la batterie / mettez-la sur « Aucune
  restriction ».
- Excluez Vault des outils de nettoyage automatique.

Même en faisant tout cela, la règle numéro un reste : **faites des sauvegardes
régulières** du fichier `.csfbk`. Aucun réglage système n'est fiable à 100 %.

### Publicité et Premium

**Quelles publicités y a-t-il dans la version gratuite ?**
Une publicité plein écran (ignorable après quelques secondes), pas plus d'une
fois toutes les ~4 minutes d'utilisation, et **uniquement** sur la grille
principale — jamais pendant l'import, l'export ou la consultation d'un fichier.
Aucune bannière permanente.

**Que débloque le Premium ?**
Il retire la publicité. Paiement **unique** (~12,99 €), sans abonnement. Les
fichiers sont **illimités** aussi dans la version gratuite.

**J'ai changé de téléphone / réinstallé : comment récupérer le Premium ?**
Paramètres → « Restaurer les achats ». L'achat est lié à votre compte Google Play.

---

## DE

### Zugriff und Wiederherstellung

**Ich habe meine PIN vergessen. Wie komme ich zurück?**
Wenn du einen **Wiederherstellungscode** oder **Sicherheitsfragen** eingerichtet
hast (Einstellungen → „Zugriffswiederherstellung“) oder eine
**`.csfbk`-Backup-Datei** hast, kommst du zurück und wählst eine neue PIN.
Ohne all das sind deine Dateien **nicht wiederherstellbar**: die Verschlüsselung
ist echt und der Schlüssel wird nur aus deiner PIN abgeleitet. Auch wir können
sie nicht entschlüsseln — das ist keine Einschränkung, das ist der ganze Sinn
der App.

**Ist der Wiederherstellungscode eine Art Universalpasswort / Hintertür?**
Nein. Wiederherstellungscode, PIN und die Antworten auf die Sicherheitsfragen
sind drei unabhängige „Schlösser“ am selben Schlüssel: jedes öffnet ihn allein,
aber der Schlüssel bleibt verschlüsselt und auf deinem Gerät. Es gibt keinen
geheimen Code, der für alle Installationen gilt (anders als bei manchen
konkurrierenden Apps, die eine feste PIN wie `11223344` verwenden).

**Wie viele PIN-Versuche habe ich?**
Fünf. Nach dem fünften Fehlversuch beginnt eine Pause, die mit jedem weiteren
länger wird (30 Sekunden, dann 1, 5, 15 Minuten). **Es werden nie Daten
gelöscht**: ein ehrlicher Fehler kostet dich nicht deine Fotos.

**Ich habe die Tarnung (Rechner/Wetter) aktiviert und komme nicht mehr rein.**
Mit dem „Rechner“-Symbol: öffne die App, tippe die PIN wie eine Rechnung ein und
drücke `=`. Mit „Wetter“: öffne die App und mache einen langen Druck auf die
Temperatur. Das Tutorial beim ersten Start erklärt das; der Play-Store-Eintrag
und der erste Start bleiben unter dem Namen „Vault“.

### Wohin die Fotos kommen

**Nachdem ich ein Foto in den Tresor importiert habe, wo wird es gespeichert?**
Im privaten Speicher der App (`/data/data/…`), **nicht** für andere Apps oder
einen Dateimanager zugänglich und **nicht** in einem sichtbaren Ordner im
Telefonspeicher. Manche konkurrierenden Apps legen einen Ordner wie
`.privacy_safe` im Stammverzeichnis an: wir nicht, absichtlich — ein solcher
Ordner verrät den Tresor, und die Dateien darin sind oft mit trivialen Werkzeugen
wiederherstellbar.

**Ist die Datei wirklich verschlüsselt oder nur hinter einer PIN versteckt?**
Wirklich verschlüsselt: **AES-256-GCM**, 256-Bit-Schlüssel aus der PIN mit
PBKDF2-SHA256 (600.000 Iterationen). Selbst wenn man die Dateien aus dem
App-Speicher zieht (dazu braucht man ein gerootetes Telefon), erhält man nur
verschlüsselte Daten.

**Könnt ihr meine Fotos sehen? Liegen sie auf einem eurer Server?**
Nein. Kein Konto, kein Server von uns, kein Upload. Die einzigen
Netzwerkverbindungen sind Werbung (nur Gratisversion) und — nur wenn du die
Tarnung „Wetter“ nutzt — ein öffentlicher Wetterdienst, der den Tresor nie
berührt.

### Import und Export

**Ich habe ein Foto in den Tresor gelegt, aber es ist noch in der Telefongalerie.**
Das ist der wichtigste Punkt, lies ihn ganz. Nach dem Verschlüsseln bietet die
App an, das **Original vom Telefon zu löschen**: Es wird endgültig entfernt,
ohne den Umweg über den System-Papierkorb. Aber:

- Wenn du diese Anfrage **abbrichst**, bleibt das Original in der Galerie. Die
  App weist dich darauf hin.
- Wenn du einen **Cloud-Synchronisierungsdienst** aktiv hast (Google Fotos,
  Samsung Cloud, Xiaomi Cloud / „Geteilte Galerie“ von MIUI, HiCloud von
  Huawei), kann eine **Kopie des Originals bereits hochgeladen sein** oder nach
  dem Entfernen **automatisch wiederhergestellt** werden. In diesem Fall: prüfe
  das System-Album und den **Cloud-Papierkorb**, lösche das Original auch dort
  und überlege, die Synchronisierung für die Fotos im Tresor auszuschalten.
- Manche Galerie-Apps von Drittanbietern (vor allem Samsung, Xiaomi) haben einen
  **eigenen Papierkorb**, der die Löschung trotzdem abfängt: wenn du so eine
  nutzt, leere ihn nach dem Import.

**Manche Fotos oder Videos erscheinen nicht, wenn ich sie hinzufügen will.**
Die App nutzt die System-Fotoauswahl, die nur Dateien anzeigt, die schon in der
Mediathek sind. Wenn eine Datei nicht erscheint (z. B. kürzlich heruntergeladen
oder in einem nicht indexierten Ordner): öffne sie einmal in der Galerie, oder
teile sie aus dem Dateimanager an Vault, oder nutze „Dokumente“ für Dateien, die
keine Fotos/Videos sind.

**Wie hole ich ein Foto aus dem Tresor?**
Öffne es und nutze „In die Galerie“: es wird entschlüsselt und zurück in die
System-Galerie gelegt. Die verschlüsselte Kopie bleibt im Tresor, bis du sie
löschst.

**Kann ich Fotos oder Videos in der App aufnehmen?**
Ja. Tippe oben auf das Kamera-Symbol und wähle „Foto aufnehmen“ oder „Video
aufnehmen“. Die Telefonkamera öffnet sich; die Aufnahme wird direkt in den Tresor
verschlüsselt (Fotos in den Ordner Fotos, Videos in Videos) und geht nie durch
die Telefongalerie, sie hinterlässt also keine Klartextkopie.

**Das Verschlüsseln oder Entschlüsseln dauert lange.**
Das hängt von der Dateigröße und der Leistung des Telefons ab. Ein Video von
mehreren hundert MB dauert einige Sekunden. Alles passiert auf dem Gerät, ohne
Netzwerk.

### Papierkorb und Datenverlust

**Ich habe ein Foto versehentlich gelöscht.**
Gelöschte Elemente bleiben 7 Tage im **Papierkorb**: öffne ihn über
Einstellungen → Papierkorb und tippe auf „Wiederherstellen“. Nach 7 Tagen werden
sie endgültig gelöscht.

**Warum löscht die App die Originale aus der Galerie?**
Weil der Tresor sonst nutzlos ist: das Foto wäre im Tresor verschlüsselt *und* im
Klartext in der Galerie. Die Löschung ist endgültig (kein Umweg über den
System-Papierkorb) — stelle also sicher, dass das Original schon im Tresor
verschlüsselt ist, bevor du bestätigst.

**Wie stelle ich sicher, dass ich meine Dateien nie verliere?**
Ein einziger Rat, und er ist ernst: **mach regelmäßige Backups**.
Einstellungen → „Backup und Migration“ → „Backup exportieren“ erstellt eine
einzige `.csfbk`-Datei (der ganze Tresor, bereits verschlüsselt, plus die
Schlüssel) zum Speichern auf einem USB-Stick, einer SD-Karte oder deiner
persönlichen Cloud. Ein Telefon kann kaputtgehen, verloren gehen oder
zurückgesetzt werden: das Backup ist das einzige echte Sicherheitsnetz.

### Neues Telefon

**Wie verschiebe ich meine Fotos auf ein neues Telefon?**
Auf dem alten: Einstellungen → „Backup exportieren“ → speichere die
`.csfbk`-Datei, wo du willst. Auf dem neuen: installiere Vault, wähle beim ersten
Start „Ich habe schon ein Backup“, wähle die Datei. Du brauchst **dieselbe
PIN** wie zuvor.

**Wenn ich die App deinstalliere, verliere ich alles?**
Ja. Anders als manche konkurrierenden Apps, die einen Ordner im Telefonspeicher
lassen und die Dateien bei der Neuinstallation „wiederfinden“, liegt der Tresor
hier im privaten Speicher der App: **die Deinstallation löscht ihn**. Bevor du
deinstallierst (oder das Telefon wechselst oder es zurücksetzt), **exportiere
ein Backup**.

### Eindringling-Foto (intruder selfie)

**Wie funktioniert das?**
Standardmäßig **deaktiviert**. Wenn du es aktivierst (Einstellungen →
„Eindringling-Foto“), nimmt die App nach **3 falschen PINs** lautlos ein Foto mit
der Frontkamera auf — keine Vorschau, kein Ton. Das Foto wird im Tresor
verschlüsselt und unter „Zugriffsversuche ansehen“ angezeigt.

**Ich habe es aktiviert, aber es wird kein Foto aufgenommen.**
Prüfe: die Kamera-Berechtigung ist erteilt (System-Einstellungen → Apps → Vault →
Berechtigungen); das Telefon hat eine Frontkamera; die Funktion wurde nicht durch
aggressive Akkuspar-Einschränkungen blockiert (siehe den nächsten Abschnitt zu
Xiaomi/Huawei). Auf manchen sehr restriktiven Oppo/Vivo/Huawei-Telefonen kann die
Hintergrundaufnahme ausbleiben.

### Xiaomi-, Huawei-, Oppo-, Vivo-, Samsung-Telefone

Diese Hersteller sind aggressiver als andere beim Beenden von Hintergrund-Apps
und beim „Aufräumen“ von Daten. Zwei Dinge, die man wissen sollte:

**1. Cloud-Synchronisierung, die Originale wiederherstellt.**
MIUI (Xiaomi), EMUI (Huawei) und ihre Cloud-Galerien **stellen** eine Datei
manchmal direkt nach dem Entfernen aus der Galerie **wieder her** oder haben
schon eine Kopie in der Cloud. Nachdem du Fotos in den Tresor gelegt hast, prüfe
das System-Album und den **Papierkorb des Cloud-Dienstes** und lösche die
Originale dort. Wenn es oft passiert, schalte die automatische
Galerie-Synchronisierung aus.

**2. „Sicherheits“- und „Reiniger“-Apps, die Daten löschen.**
Werkzeuge wie *Sicherheit* / *Telefonmanager* / *Reiniger* von Xiaomi/Huawei
können die privaten Daten einer App löschen, wenn sie sie für „inaktiv“ halten,
und das **würde den Tresor löschen**. Um das zu verhindern:

- Sperre Vault im Bildschirm der letzten Apps (Schloss-Symbol).
- Aktiviere den **Autostart** für Vault (MIUI: Sicherheit → Berechtigungen →
  Autostart; EMUI: Einstellungen → Apps → App-Start).
- Nimm Vault aus der Akku-Optimierung / stelle sie auf „Keine Einschränkungen“.
- Schließe Vault von automatischen Reiniger-Werkzeugen aus.

Auch wenn du all das tust, gilt weiterhin Regel Nummer eins: **mach regelmäßige
Backups** der `.csfbk`-Datei. Keine System-Einstellung ist zu 100 %
zuverlässig.

### Werbung und Premium

**Welche Werbung gibt es in der Gratisversion?**
Eine Vollbildanzeige (nach wenigen Sekunden überspringbar), höchstens einmal pro
~4 Minuten Nutzung, und **nur** im Hauptraster — nie während Import, Export oder
beim Ansehen einer Datei. Kein Dauerbanner.

**Was schaltet Premium frei?**
Es entfernt die Werbung. **Einmalzahlung** (~12,99 €), kein Abo. Dateien sind
auch in der Gratisversion **unbegrenzt**.

**Ich habe das Telefon gewechselt / neu installiert: wie bekomme ich Premium zurück?**
Einstellungen → „Käufe wiederherstellen“. Der Kauf ist an dein
Google-Play-Konto gebunden.

---

## ES

### Acceso y recuperación

**He olvidado el PIN. ¿Cómo vuelvo a entrar?**
Si configuraste un **código de recuperación** o **preguntas de seguridad**
(Ajustes → «Recuperación del acceso»), o si tienes un **archivo de copia de
seguridad `.csfbk`**, puedes volver a entrar y elegir un PIN nuevo. Sin nada de
eso, tus archivos son **irrecuperables**: el cifrado es real y la clave deriva
solo de tu PIN. Ni siquiera nosotros podemos descifrarlos: no es una limitación,
es todo el sentido de la app.

**¿El código de recuperación es una especie de contraseña universal / puerta trasera?**
No. El código de recuperación, el PIN y las respuestas a las preguntas de
seguridad son tres «cerraduras» independientes sobre la misma clave: cada una la
abre por sí sola, pero la clave permanece cifrada y en tu dispositivo. No existe
un código secreto válido para todas las instalaciones (a diferencia de algunas
apps de la competencia que usan un PIN fijo como `11223344`).

**¿Cuántos intentos tengo para el PIN?**
Cinco. Tras el quinto fallo empieza una pausa que crece con cada nuevo intento
erróneo (30 segundos, luego 1, 5, 15 minutos). **Nunca se borran datos**: un
error honesto no te hace perder las fotos.

**Activé el disfraz (Calculadora/Tiempo) y ya no consigo entrar.**
Con el icono «Calculadora»: abre la app, escribe el PIN como si fuera un cálculo
y pulsa `=`. Con «Tiempo»: abre la app y mantén pulsada la temperatura. El
tutorial del primer inicio lo explica; la ficha de Play Store y el primer inicio
se mantienen con el nombre «Vault».

### Dónde van las fotos

**Después de importar una foto a la caja fuerte, ¿dónde se guarda?**
En el espacio privado de la app (`/data/data/…`), **no** accesible para otras
apps ni para un explorador de archivos, y **no** en una carpeta visible de la
memoria del teléfono. Algunas apps de la competencia crean una carpeta tipo
`.privacy_safe` en la raíz: nosotros no, a propósito; una carpeta así revela la
caja fuerte y los archivos que contiene suelen ser recuperables con herramientas
básicas.

**¿El archivo está cifrado de verdad o solo oculto tras un PIN?**
Cifrado de verdad: **AES-256-GCM**, clave de 256 bits derivada del PIN con
PBKDF2-SHA256 (600.000 iteraciones). Incluso extrayendo los archivos del
almacenamiento de la app (hace falta un teléfono con root), solo se obtienen
datos cifrados.

**¿Podéis ver mis fotos? ¿Están en algún servidor vuestro?**
No. Sin cuenta, sin servidor nuestro, sin subida. Las únicas conexiones de red
son la publicidad (solo versión gratuita) y —solo si usas el disfraz «Tiempo»— un
servicio meteorológico público que nunca toca la caja fuerte.

### Importar y exportar

**He añadido una foto a la caja fuerte pero sigue en la galería del teléfono.**
Este es el punto más importante, léelo entero. Tras cifrar la foto, la app
propone **eliminar el original del teléfono**: se borra definitivamente, sin
pasar por la papelera del sistema. Pero:

- Si **cancelas** esa petición, el original se queda en la galería. La app te lo
  avisa.
- Si tienes un **servicio de sincronización en la nube** activo (Google Fotos,
  Samsung Cloud, Xiaomi Cloud / «Galería compartida» de MIUI, HiCloud de
  Huawei), una **copia del original puede estar ya subida** o **restaurarse
  automáticamente** tras la eliminación. En ese caso: revisa el álbum del sistema
  y la **papelera de la nube**, borra el original también ahí, y valora
  desactivar la sincronización para las fotos que metes en la caja fuerte.
- Algunas apps de Galería de terceros (Samsung, Xiaomi sobre todo) tienen su
  **propia papelera** que intercepta la eliminación igualmente: si usas una,
  vacíala tras la importación.

**Algunas fotos o vídeos no aparecen cuando intento añadirlos.**
La app usa el selector de fotos del sistema, que solo muestra archivos que ya
están en la biblioteca multimedia. Si un archivo no aparece (por ejemplo,
descargado hace poco o en una carpeta no indexada): ábrelo una vez en la galería,
o compártelo con Vault desde el explorador de archivos, o usa «Documentos» para
los archivos que no son fotos/vídeos.

**¿Cómo saco una foto de la caja fuerte?**
Ábrela y usa «A la galería»: se descifra y se vuelve a poner en la galería del
sistema. La copia cifrada se queda en la caja fuerte hasta que la elimines.

**¿Puedo hacer fotos o vídeos dentro de la app?**
Sí. Toca el icono de la cámara arriba y elige «Hacer una foto» o «Grabar un
vídeo». Se abre la cámara del teléfono; la toma se cifra directamente en la caja
fuerte (las fotos en la carpeta Fotos, los vídeos en Vídeos) y nunca pasa por la
galería del teléfono, así que no deja ninguna copia en claro.

**El cifrado o el descifrado tarda mucho.**
Depende del tamaño del archivo y de la potencia del teléfono. Un vídeo de varios
cientos de MB tarda unos segundos. Todo ocurre en el dispositivo, sin red.

### Papelera y pérdida de archivos

**He eliminado una foto por error.**
Los elementos eliminados se quedan en la **Papelera** durante 7 días: ábrela
desde Ajustes → Papelera y pulsa «Restaurar». Después de 7 días se eliminan para
siempre.

**¿Por qué la app elimina los originales de la galería?**
Porque si no la caja fuerte no sirve de nada: la foto estaría cifrada en la caja
fuerte *y* en claro en la galería. La eliminación es definitiva (no pasa por la
papelera del sistema), así que asegúrate de tener el original ya cifrado en la
caja fuerte antes de confirmar.

**¿Cómo me aseguro de no perder nunca mis archivos?**
Un solo consejo, y es serio: **haz copias de seguridad regulares**. Ajustes →
«Copia de seguridad y migración» → «Exportar copia» crea un único archivo
`.csfbk` (toda la caja fuerte, ya cifrada, más las claves) para guardar en un
pendrive, una tarjeta SD o tu nube personal. Un teléfono puede romperse, perderse
o restablecerse: la copia de seguridad es la única red de seguridad real.

### Teléfono nuevo

**¿Cómo paso mis fotos a un teléfono nuevo?**
En el viejo: Ajustes → «Exportar copia» → guarda el archivo `.csfbk` donde
quieras. En el nuevo: instala Vault, en el primer inicio elige «Ya tengo una
copia de seguridad», selecciona el archivo. Necesitarás **el mismo PIN** que
antes.

**Si desinstalo la app, ¿lo pierdo todo?**
Sí. A diferencia de algunas apps de la competencia, que dejan una carpeta en la
memoria del teléfono y «recuperan» los archivos al reinstalar, aquí la caja
fuerte está en el almacenamiento privado de la app: **desinstalar la borra**.
Antes de desinstalar (o de cambiar de teléfono, o de hacer un restablecimiento)
**exporta una copia de seguridad**.

### Foto del intruso (intruder selfie)

**¿Cómo funciona?**
Opción **desactivada de fábrica**. Si la activas (Ajustes → «Foto del intruso»),
tras **3 PIN incorrectos** la app toma en silencio una foto con la cámara frontal
—sin vista previa, sin sonido—. La foto se cifra en la caja fuerte y se ve en
«Ver los intentos de acceso».

**La he activado pero no toma ninguna foto.**
Comprueba que: el permiso de Cámara está concedido (Ajustes del sistema → Apps →
Vault → Permisos); el teléfono tiene cámara frontal; la función no ha sido
bloqueada por restricciones de ahorro de batería agresivas (ver la siguiente
sección sobre Xiaomi/Huawei). En algunos teléfonos Oppo/Vivo/Huawei muy
restrictivos la captura en segundo plano puede no dispararse.

### Teléfonos Xiaomi, Huawei, Oppo, Vivo, Samsung

Estos fabricantes son más agresivos que los demás al cerrar apps en segundo plano
y al «limpiar» datos. Dos cosas que hay que saber:

**1. Sincronización en la nube que restaura los originales.**
MIUI (Xiaomi), EMUI (Huawei) y sus galerías-nube a veces **restauran** un archivo
justo después de quitarlo de la galería, o ya tienen una copia en la nube.
Después de meter fotos en la caja fuerte, revisa el álbum del sistema y la
**papelera del servicio en la nube** y borra ahí los originales. Si te pasa a
menudo, desactiva la sincronización automática de la galería.

**2. Apps de «seguridad» y «limpieza» que borran los datos.**
Las herramientas tipo *Seguridad* / *Gestor del teléfono* / *Limpieza* de
Xiaomi/Huawei pueden borrar los datos privados de una app si la consideran
«inactiva», y eso **borraría la caja fuerte**. Para evitarlo:

- Bloquea Vault en la pantalla de apps recientes (icono de candado).
- Activa el **Inicio automático** para Vault (MIUI: Seguridad → Permisos → Inicio
  automático; EMUI: Ajustes → Apps → Inicio de apps).
- Quita Vault de la optimización de batería / ponla en «Sin restricciones».
- Excluye Vault de las herramientas de limpieza automática.

Aun haciendo todo esto, la regla número uno sigue siendo: **haz copias de
seguridad regulares** del archivo `.csfbk`. Ningún ajuste del sistema es fiable al
100 %.

### Publicidad y Premium

**¿Qué publicidad hay en la versión gratuita?**
Un anuncio a pantalla completa (que se puede saltar tras unos segundos), no más
de una vez cada ~4 minutos de uso, y **solo** en la cuadrícula principal —nunca
durante la importación, la exportación o la visualización de un archivo—. Sin
banner permanente.

**¿Qué desbloquea el Premium?**
Quita la publicidad. Pago **único** (~12,99 €), sin suscripción. Los archivos son
**ilimitados** también en la versión gratuita.

**He cambiado de teléfono / reinstalado: ¿cómo recupero el Premium?**
Ajustes → «Restaurar compras». La compra está vinculada a tu cuenta de Google
Play.

---

## PT

### Acesso e recuperação

**Esqueci-me do PIN. Como volto a entrar?**
Se definiste um **código de recuperação** ou **perguntas de segurança**
(Definições → «Recuperação do acesso»), ou se tens um **ficheiro de cópia de
segurança `.csfbk`**, podes voltar a entrar e escolher um novo PIN. Sem nada
disso, os teus ficheiros são **irrecuperáveis**: a cifragem é real e a chave
deriva apenas do teu PIN. Nem nós conseguimos decifrá-los — não é uma limitação,
é todo o objetivo da aplicação.

**O código de recuperação é uma espécie de palavra-passe universal / porta dos fundos?**
Não. O código de recuperação, o PIN e as respostas às perguntas de segurança são
três «fechaduras» independentes na mesma chave: cada uma abre-a sozinha, mas a
chave permanece cifrada e no teu dispositivo. Não existe um código secreto válido
para todas as instalações (ao contrário de algumas aplicações concorrentes que
usam um PIN fixo como `11223344`).

**Quantas tentativas tenho para o PIN?**
Cinco. Após o quinto erro começa uma pausa que aumenta a cada nova tentativa
errada (30 segundos, depois 1, 5, 15 minutos). **Nunca são apagados dados**: um
erro honesto não te faz perder as fotos.

**Ativei o disfarce (Calculadora/Meteorologia) e já não consigo entrar.**
Com o ícone «Calculadora»: abre a aplicação, digita o PIN como se fosse um
cálculo e prime `=`. Com «Meteorologia»: abre a aplicação e faz uma pressão longa sobre
a temperatura. O tutorial do primeiro arranque explica isto; a página da Play
Store e o primeiro arranque mantêm-se com o nome «Vault».

### Para onde vão as fotos

**Depois de importar uma foto para o cofre, onde é guardada?**
No espaço privado da aplicação (`/data/data/…`), **não** acessível a outras
aplicações nem a um gestor de ficheiros, e **não** numa pasta visível na memória
do telemóvel. Algumas aplicações concorrentes criam uma pasta do tipo
`.privacy_safe` na raiz: nós não, de propósito — uma pasta dessas revela o cofre
e os ficheiros lá dentro são muitas vezes recuperáveis com ferramentas triviais.

**O ficheiro está mesmo cifrado ou só escondido atrás de um PIN?**
Mesmo cifrado: **AES-256-GCM**, chave de 256 bits derivada do PIN com
PBKDF2-SHA256 (600 000 iterações). Mesmo retirando os ficheiros do armazenamento
da aplicação (é preciso um telemóvel com root), só se obtêm dados cifrados.

**Conseguem ver as minhas fotos? Estão num servidor vosso?**
Não. Sem conta, sem servidor nosso, sem envio. As únicas ligações de rede são a
publicidade (só versão gratuita) e — apenas se usares o disfarce «Meteorologia» — um
serviço meteorológico público que nunca toca no cofre.

### Importar e exportar

**Adicionei uma foto ao cofre mas continua na galeria do telemóvel.**
Este é o ponto mais importante, lê-o todo. Depois de cifrar a foto, a aplicação
propõe **eliminar o original do telemóvel**: é apagado definitivamente, sem
passar pela reciclagem do sistema. Mas:

- Se **cancelares** esse pedido, o original fica na galeria. A aplicação avisa-te.
- Se tiveres um **serviço de sincronização na nuvem** ativo (Google Fotos, Samsung
  Cloud, Xiaomi Cloud / «Galeria partilhada» do MIUI, HiCloud da Huawei), uma
  **cópia do original pode já estar enviada** ou ser **restaurada
  automaticamente** após a remoção. Nesse caso: verifica o álbum do sistema e a
  **reciclagem da nuvem**, apaga o original também aí, e pondera desativar a
  sincronização para as fotos que colocas no cofre.
- Algumas aplicações de Galeria de terceiros (Samsung, Xiaomi sobretudo) têm uma
  **reciclagem própria** que interceta a eliminação à mesma: se usas uma,
  esvazia-a depois da importação.

**Algumas fotos ou vídeos não aparecem quando tento adicioná-los.**
A aplicação usa o seletor de fotos do sistema, que só mostra ficheiros já
presentes na biblioteca multimédia. Se um ficheiro não aparecer (por exemplo,
descarregado há pouco ou numa pasta não indexada): abre-o uma vez na galeria, ou
partilha-o para o Vault a partir do gestor de ficheiros, ou usa «Documentos» para
os ficheiros que não são fotos/vídeos.

**Como tiro uma foto do cofre?**
Abre-a e usa «Para a galeria»: é decifrada e recolocada na galeria do sistema. A
cópia cifrada fica no cofre até a eliminares.

**Posso tirar fotos ou vídeos dentro da app?**
Sim. Toca no ícone da câmara em cima e escolhe «Tirar uma foto» ou «Gravar um
vídeo». Abre-se a câmara do telemóvel; a captura é cifrada diretamente no cofre
(as fotos na pasta Fotos, os vídeos em Vídeos) e nunca passa pela galeria do
telemóvel, por isso não deixa nenhuma cópia em claro.

**A cifragem ou a decifragem demora muito.**
Depende do tamanho do ficheiro e da potência do telemóvel. Um vídeo de várias
centenas de MB demora alguns segundos. Tudo acontece no dispositivo, sem rede.

### Reciclagem e perda de ficheiros

**Eliminei uma foto por engano.**
Os itens eliminados ficam na **Reciclagem** durante 7 dias: abre-a em Definições
→ Reciclagem e toca em «Restaurar». Após 7 dias são eliminados para sempre.

**Porque é que a aplicação elimina os originais da galeria?**
Porque senão o cofre não serve para nada: a foto estaria cifrada no cofre *e* em
claro na galeria. A eliminação é definitiva (não passa pela reciclagem do
sistema), por isso confirma só depois de teres o original já cifrado no cofre.

**Como garanto que nunca perco os meus ficheiros?**
Um só conselho, e é sério: **faz cópias de segurança regulares**. Definições →
«Cópia de segurança e migração» → «Exportar cópia» cria um único ficheiro
`.csfbk` (todo o cofre, já cifrado, mais as chaves) para guardar numa pen USB,
num cartão SD ou na tua nuvem pessoal. Um telemóvel pode partir-se, perder-se ou
ser reposto: a cópia de segurança é a única verdadeira rede de segurança.

### Telemóvel novo

**Como passo as minhas fotos para um telemóvel novo?**
No antigo: Definições → «Exportar cópia» → guarda o ficheiro `.csfbk` onde
quiseres. No novo: instala o Vault, no primeiro arranque escolhe «Já tenho uma
cópia de segurança», seleciona o ficheiro. Vais precisar do **mesmo PIN** de
antes.

**Se desinstalar a aplicação, perco tudo?**
Sim. Ao contrário de algumas aplicações concorrentes, que deixam uma pasta na
memória do telemóvel e «reencontram» os ficheiros na reinstalação, aqui o cofre
está no armazenamento privado da aplicação: **a desinstalação apaga-o**. Antes de
desinstalar (ou de mudar de telemóvel, ou de fazer uma reposição), **exporta uma
cópia de segurança**.

### Foto do intruso (intruder selfie)

**Como funciona?**
Opção **desativada por predefinição**. Se a ativares (Definições → «Foto do
intruso»), após **3 PIN errados** a aplicação tira em silêncio uma foto com a
câmara frontal — sem pré-visualização, sem som. A foto é cifrada no cofre e vista
em «Ver as tentativas de acesso».

**Ativei-a mas não tira nenhuma foto.**
Verifica que: a permissão da Câmara está concedida (Definições do sistema →
Aplicações → Vault → Permissões); o telemóvel tem câmara frontal; a função não
foi bloqueada por restrições de poupança de bateria agressivas (ver a secção
seguinte sobre Xiaomi/Huawei). Em alguns telemóveis Oppo/Vivo/Huawei muito
restritivos a captura em segundo plano pode não ocorrer.

### Telemóveis Xiaomi, Huawei, Oppo, Vivo, Samsung

Estes fabricantes são mais agressivos do que os outros a fechar aplicações em
segundo plano e a «limpar» dados. Duas coisas a saber:

**1. Sincronização na nuvem que restaura os originais.**
O MIUI (Xiaomi), o EMUI (Huawei) e as respetivas galerias-nuvem por vezes
**restauram** um ficheiro logo após ser retirado da galeria, ou já têm uma cópia
na nuvem. Depois de colocares fotos no cofre, verifica o álbum do sistema e a
**reciclagem do serviço de nuvem** e apaga aí os originais. Se acontecer com
frequência, desativa a sincronização automática da galeria.

**2. Aplicações de «segurança» e «limpeza» que apagam os dados.**
As ferramentas do tipo *Segurança* / *Gestor do telemóvel* / *Limpeza* da
Xiaomi/Huawei podem apagar os dados privados de uma aplicação se a considerarem
«inativa», e isso **apagaria o cofre**. Para o evitar:

- Bloqueia o Vault no ecrã das aplicações recentes (ícone de cadeado).
- Ativa o **Arranque automático** para o Vault (MIUI: Segurança → Permissões →
  Arranque automático; EMUI: Definições → Aplicações → Arranque de aplicações).
- Retira o Vault da otimização da bateria / coloca-o em «Sem restrições».
- Exclui o Vault das ferramentas de limpeza automática.

Mesmo fazendo tudo isto, a regra número um mantém-se: **faz cópias de segurança
regulares** do ficheiro `.csfbk`. Nenhuma definição do sistema é 100 % fiável.

### Publicidade e Premium

**Que publicidade há na versão gratuita?**
Um anúncio em ecrã inteiro (ignorável após alguns segundos), no máximo uma vez a
cada ~4 minutos de utilização, e **apenas** na grelha principal — nunca durante a
importação, a exportação ou a visualização de um ficheiro. Sem banner permanente.

**O que desbloqueia o Premium?**
Remove a publicidade. Pagamento **único** (~12,99 €), sem subscrição. Os
ficheiros são **ilimitados** também na versão gratuita.

**Mudei de telemóvel / reinstalei: como recupero o Premium?**
Definições → «Restaurar compras». A compra está associada à tua conta Google
Play.
