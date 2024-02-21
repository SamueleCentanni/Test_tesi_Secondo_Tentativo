# GitHub
## Collegamento GitHub con l'mdBook locale
Per prima cosa bisogna andare dentro la cartella in cui è stato creato il progetto mdbook. A questo punto, da linea di comando, si digita:
`git init`

Si deve ora collegare il link del repo GitHub (che deve ovviamente già esistere) al progetto mdBook. Lo si fa inserendo:
`git remote add origin URL_DEL_TUO_REPOSITORY`

## Aggiunta dei file locali al repository
Ora possiamo inserire i file locali (quindi la cartella src, il file .toml e il file .gitignore) nel nostro repo. Per farlo, è sufficiente digitare:
```bash
git add .
git commit -m "Commento del commit"
```

Prima di fare il push dei tuoi file, se il tuo repository su GitHub utilizza main come branch principale (pratica standard per i repository creati dopo il 2020), assicurati di essere sul branch corretto eseguendo:
```bash
git branch -M main
```
Questo comando rinomina il branch locale in main, allineandolo con il nome del branch principale su GitHub. Ora puoi eseguire il push sul branch main:
```bash
git push -u origin main
```
> nota che, nel caso ci fossero problemi, è possibile usare il comando `git fetch`.

Abbiamo fatto. Nel nostro repo troveremo il nostro mdBook.
E' possibile in ogni momento aggiornare la propria directory locale (quella sul tuo pc, creata seguendo il primo capitolo) usando, dal prompt dei comandi, il comando:
```bash
git pull
```

Nel capitolo successivo vedremo come settare le Actions.
