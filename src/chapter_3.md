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

Ora bisogna pushare il tutto sul branch principale, che è il branch **main**. Per farlo, prima si esegue `git fetch`. Esso serve per mettere come predefinito il branch main (qualora non venisse trovato da gitHub).
Infatti, dal 2020 in poi, il branch principale si chiama **master**, anche se quando si crea il repository ci si trova di default sul branch **main**. Dunque con il comando `git fetch` risolviamo questo problema.
A questo punto, si esegue il push:
```
git push -u origin main
```

Abbiamo fatto. Nel nostro repo troveremo il nostro mdBook.
