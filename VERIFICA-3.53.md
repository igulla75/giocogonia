# Giocogonia 3.53 – verifica (24 novembre 2026)

Collaudo fatto da Claude, che ha scritto anche le modifiche: non è una verifica indipendente. Browser: Google Chrome senza finestra, pilotato da script; l'app era servita in HTTPS da un server locale.

## Che cosa cambia rispetto alla 3.52
1. **Nome visibile**: AttivaMente → Giocogonia in 47 punti (titolo, barra in alto, guida, installazione, condivisione, stampa, messaggi), sottotitolo «Dove nascono i giochi», spiegazione del nome nella guida, nomi dei file esportati (`giocogonia-….json`), manifest. Script `patch353.py`: ogni sostituzione deve trovare il testo esatto il numero di volte previsto.
2. **Restano uguali apposta** (invisibili): la chiave dell'archivio nel browser `attivamente.v1` (così i lavori salvati restano), le chiavi temporanee. L'importazione non guarda il nome dell'app nei file, quindi i file esportati con AttivaMente si aprono ancora.
3. **Service worker**: cache con prefisso `giocogonia-` (v73). Le due app sono sullo stesso sito (igulla75.github.io), dove le cache sono in comune: ognuna cancella solo le sue.
4. **Vecchio indirizzo** (cartella `vecchio-indirizzo`): una pagina che porta a `../giocogonia/` conservando la parte dopo `#` (i giochi ricevuti con un link), e un service worker che cancella solo le copie della vecchia app e si disattiva.
5. **Difetto della 3.51 trovato con una prova nuova** («svuota il foglio»): in Unisci i puntini e Pentamini un foglio svuotato con «Cancella la figura», «Svuota» o «Ricomincia da capo», esportato e reimportato, veniva rifiutato (lo schema dei dati non aveva mai visto quelle liste vuote). Ora è accettato.

## Prove
| Prova | Esito |
|---|---|
| Gioca: 31 giochi × tutti i livelli (156 partite) con Controlla, Aiuto, Soluzione, Stampa | 0 errori |
| Crea: 50 strumenti, clic a caso (prima della correzione 5, che tocca solo lo schema dei dati) | 0 errori |
| «Svuota il foglio»: tutti i pulsanti di cancellazione di 50 strumenti, poi esporta/reimporta | prima 4 rifiuti (puntini, penta), dopo 0 |
| Andata e ritorno: 150 lavori con clic a caso, esportati e reimportati | 150 accettati |
| Link ostili: 30 giochi × 8 tipi di contenuto | 0 errori, 0 richieste esterne, nessun codice eseguito |
| File e partite esportati con il vecchio nome | si aprono |
| Vecchio nome visibile (8 pagine e guida) | assente |
| Passaggio dal vecchio indirizzo: lavoro salvato con la vecchia app, poi pagina di rinvio | lavoro ritrovato in Giocogonia; vecchio link di gioco aperto nella nuova app; cache e registrazione della vecchia app tolte, quelle di Giocogonia intatte |
| Senza connessione | pagina e dizionario disponibili |
| Telefono 375×800 | intestazione 115 px, nessun comando sotto 24 px, nessuno scorrimento laterale |

## Limiti
- Su GitHub oggi c'è una versione vecchia (cache v45), il cui service worker serve la pagina dalla copia salvata: chi l'ha installata vedrà il rinvio dopo che il browser avrà aggiornato il service worker (di solito alla seconda o terza apertura). La prova è stata fatta con la 3.52 al posto della v45, che non è disponibile.
- Nessuna prova su dispositivi veri.
- La verifica del nome sul registro italiano dei marchi (UIBM) non è stata completata: TMview era bloccato; il registro UE non contiene «giocogonia».
- Il libro, le slide e il QR usano ancora il vecchio nome.
