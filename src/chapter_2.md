# mdBook
## Installazione mdBook
Per installare mdBook, si deve prima di tutto installare Rust. Il link per scaricare Rust, linguaggio su cui si basa mdBook, è il seguente: [Download Rust](https://www.rust-lang.org/tools/install).
Una volta fatto ciò, si va su linea di comando, ci si sposta nella directory in cui si vuole installare mdBook, e si usa il comando:
```bash
cargo install mdbook
```

A questo punto abbiamo installato mdbook.

## Creazione Primo Progetto
Per creare il primo progetto, si crea una cartella, all'interno della quale si vuole salvare il progetto, e da linea di comando si usano i seguenti comandi:

```bash
mdbook init project-name
```
Con questo comando si crea il progetto, troveremo la cartella src, che conterrà il file SUMMARY.md e il file relativo al primo capitolo del libro, Chapter_1. Si vedranno poi i file .gitignore e book.toml, che gestisce le impostazioni del nostro libro.
Si entra nella cartella appena creata e, sempre da linea di comando, si digita:

```bash
mdbook build 
```

A questo punto viene creata la cartella book, che contiene tutti i file html e css necessari al progetto. Siamo pronti ad aggiungere i file markdown dentro la cartella src, e, per effettivamente vederli nel sito, si deve aggiornare il file SUMMARY.md

## Vedere il sito
Per vedere il sito si può:
- ad ogni modifica, fare la build del progetto con il comando ` mdbook build `, e aprire il sito con il comando `mdbook build --open`. Ciò che viene aperto è in realta una sorta di PDF, il sito non è ovviamente pubblico sulla rete;
- utilizzare il comando ` mdbook serve `, che guarderà ogni modifica fatta nella nostra cartella src e in automatico farà la build del sito. Con questo comando è possibile visitare il sito, salvato in locale, all'[indirizzo](http://localhost:3000/).

### Collegamento con GitHub
Per vedere come collegare il progetto a gitHub, vedi il capitolo 3.
