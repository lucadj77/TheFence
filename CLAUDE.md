# Il Ricettatore (The Fence)

## Descrizione del Progetto

**Il Ricettatore** è un gioco di deduzione interattivo basato su web, ispirato al classico gioco da tavolo "Cluedo". Il gioco è completamente sviluppato in italiano e si svolge su una griglia 7x7 dove i giocatori devono dedurre la posizione di personaggi e oggetti attraverso un sistema di carte e risposte.

## Caratteristiche Tecniche

### Struttura del Progetto
```
/TheFence/
├── .git/           (Controllo versione Git)
└── index.html      (Applicazione completa - 541KB, 1132 righe)
```

### Tecnologie Utilizzate

- **HTML5**: Markup semantico con lingua italiana (`lang="it"`)
- **CSS3 Moderno**:
  - CSS Grid e Flexbox per layout responsive
  - Design glassmorphic con gradienti navy/teal
  - CSS Variables per theming
  - Backdrop filters per effetti di profondità
  - Media queries per supporto mobile (<500px)
  - Transizioni e animazioni
- **JavaScript Vanilla**:
  - Nessuna dipendenza esterna
  - Gestione dello stato locale
  - Manipolazione DOM nativa
  - Algoritmi di gioco e logica di deduzione
  - Immagini Base64 incorporate

### Architettura

Applicazione **single-page completamente autonoma** - tutto (HTML, CSS, JavaScript, immagini) è contenuto in un unico file `index.html`. Nessun server backend richiesto, nessuna dipendenza esterna da scaricare.

## Elementi del Gioco

### Personaggi (9)
- **Alan**
- **Bob**
- **Chuck**
- **Dalia**
- **Eric**
- **Frank**
- **Giulia**
- **Hank**
- **Igor**

### Oggetti da Trovare (4)
- **Lingotti** (Gold bars)
- **Quadro** (Painting)
- **Statua** (Statue)
- **Cristallo** (Crystal)

### Tabellone di Gioco

Griglia 7x7 con 16 celle denominate (A-P):

```
A    -    B    -    C    -    D
-    P1   -    P2   -    P3   -
E    -    F    -    G    -    H
-    P4   -    P5   -    P6   -
I    -    J    -    K    -    L
-    P7   -    P8   -    P9   -
M    -    N    -    O    -    P
```

Le celle intermedie rappresentano i 9 personaggi (P1-P9).

## Meccaniche di Gioco

### Sistema di Carte
- **32 carte** numerate da 1 a 32
- I giocatori giocano le carte in sequenza per fare domande

### Flusso di Gioco

1. **Inizializzazione**:
   - Generazione o caricamento di una scheda di gioco
   - Ogni scheda ha un codice univoco per condivisione

2. **Turni di Gioco**:
   - Il **Giocatore A** inserisce un numero di carta
   - Il sistema calcola e mostra la risposta per entrambi i giocatori
   - Il **Giocatore B** riceve informazioni complementari
   - Le risposte sono basate su:
     - Regole di adiacenza (ogni personaggio ha 4 celle adiacenti)
     - Vincoli di riga e colonna
     - Logica di eliminazione

3. **Accusa**:
   - Quando pronto, un giocatore può fare un'accusa
   - Deve selezionare la posizione corretta per ogni oggetto
   - Il sistema verifica se l'accusa è corretta

4. **Vittoria**:
   - Il primo giocatore che indovina correttamente la posizione di tutti e 4 gli oggetti vince

### Sistema di Codifica

- **Generazione Scheda**: Crea una configurazione casuale del gioco
- **Codifica**: Converte la scheda in un codice condivisibile
- **Decodifica**: Carica una scheda esistente da un codice

Questo permette ai giocatori di condividere la stessa configurazione di gioco.

## Funzioni Principali

### File: `index.html` (linee 588-1130)

#### Gestione del Gioco
- `generaScheda()` - Genera una nuova configurazione di gioco casuale
- `codificaScheda()` - Converte la scheda in un codice Base64
- `decodificaScheda(codice)` - Carica una scheda da un codice
- `caricaScheda()` - Gestisce il caricamento della scheda inserita dall'utente
- `avviaGioco()` - Inizializza la sessione di gioco

#### Sistema di Carte e Risposte
- `confermaCarta()` - Processa l'input della carta del giocatore
- `calcolaRisposta(carta)` - Calcola le risposte per entrambi i giocatori
- `aggiungiRisposta(giocatore, testo)` - Mostra le risposte nell'interfaccia
- `cancellaCarta()` - Rimuove l'ultima carta giocata

#### Accusa e Soluzione
- `apriAccusa()` - Apre l'interfaccia di accusa
- `confermaAccusa()` - Verifica l'accusa del giocatore
- `mostraSoluzione()` - Mostra la soluzione (modalità debug)
- `verificaPasswordDebug()` - Gestisce l'accesso debug (password: `debug2024`)

#### Visualizzazione
- `generaTabelloneVisuale()` - Genera la rappresentazione visiva del tabellone con personaggi e oggetti
- `mostraSchermata(id)` - Gestisce la navigazione tra le schermate

#### Utility
- `ottieniAdiacenti(cella)` - Restituisce le 4 celle adiacenti a una cella data
- `cellaRiga(cella)` / `cellaColonna(cella)` - Calcola riga/colonna di una cella
- `ottieniRigaCella(riga)` / `ottieniColonnaCella(colonna)` - Ottiene celle per riga/colonna

## Design e UI

### Tema Visivo
- **Colori**: Gradiente scuro con navy (#0a0e27, #1a1a2e) e teal (#16213e, #0f3460)
- **Stile**: Glassmorphism moderno con backdrop blur
- **Font**: System fonts per prestazioni ottimali
- **Responsive**: Layout adattivo per desktop, tablet e mobile

### Schermate Principali

1. **Schermata Inizializzazione**: Genera o carica una scheda di gioco
2. **Schermata di Gioco**: Input carte e visualizzazione risposte
3. **Schermata Accusa**: Selezione posizioni oggetti
4. **Schermata Risultato**: Vittoria o sconfitta
5. **Schermata Debug**: Accesso alla soluzione (protetta da password)
6. **Schermata Soluzione**: Visualizzazione tabellone completo

### Elementi Interattivi
- Pulsanti con stati hover e active
- Card input responsive
- Box di risposta colorati per giocatore (blu per A, verde per B)
- Grid di selezione per personaggi e oggetti
- Visualizzazione tabellone con immagini

## Immagini e Asset

Tutte le immagini sono incorporate come stringhe Base64 in formato WebP:
- **9 ritratti** dei personaggi (~40x40px)
- **4 icone** degli oggetti (~60x60px)
- Nessun asset esterno richiesto

## Modalità Debug

**Password**: `debug2024`

Permette di:
- Visualizzare la soluzione completa
- Vedere il tabellone con tutte le posizioni corrette
- Utile per testing e sviluppo

## Storia del Progetto

### Commit Recenti
```
5f364a0 - Update index.html (Corretto errore di caricamento)
a024031 - Update index.html
143d083 - Rename the-fence.html to index.html
97537b2 - Add files via upload
```

### Repository Git
- **Remote**: Local proxy su `http://127.0.0.1:21453/git/lucadj77/TheFence`
- **Branch principale**: Configurazione standard Git

## Installazione e Utilizzo

### Requisiti
- Nessuno! Solo un browser web moderno

### Come Eseguire
1. Apri `index.html` in qualsiasi browser web moderno
2. Il gioco funziona completamente offline
3. Nessuna installazione o configurazione richiesta

### Compatibilità Browser
- Chrome/Edge (moderno)
- Firefox (moderno)
- Safari (moderno)
- Richiede supporto per:
  - CSS Grid
  - CSS Backdrop Filter
  - JavaScript ES6+
  - Base64 decoding

## Caratteristiche Distintive

✓ **Zero dipendenze**: Nessuna libreria esterna
✓ **Completamente offline**: Funziona senza connessione internet
✓ **Single file**: Facile da distribuire e condividere
✓ **Responsive**: Funziona su desktop e mobile
✓ **Codici condivisibili**: I giocatori possono giocare sulla stessa scheda
✓ **Due giocatori**: Sistema di risposta asimmetrico per entrambi i giocatori
✓ **Design moderno**: Interfaccia pulita con glassmorphism

## Note di Sviluppo

- Lingua: Italiano
- Formato file: HTML5 con CSS e JS embedded
- Dimensione: ~541KB (comprese immagini Base64)
- Linee di codice: 1,132
- Performance: Ottimizzate per caricamento istantaneo

## Possibili Miglioramenti Futuri

- Multiplayer online con WebSocket
- Salvataggio stato di gioco in localStorage
- Modalità difficoltà variabili
- Timer per limitare il tempo di gioco
- Statistiche e storico partite
- Più temi visivi
- Supporto multilingua
- Tutorial interattivo
- Sistema di hint

---

**Progetto**: Il Ricettatore
**Tipo**: Single-Page Web Application Game
**Linguaggio**: Italiano
**Licenza**: Non specificata
**Autore**: lucadj77
