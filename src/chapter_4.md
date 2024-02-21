# Settaggio delle Actions
Le _Actions_ sono le azioni automatiche che possono essere eseguite da GitHub all'avvenimenento di un certo trigger, come può essere, nel nostro caso, il commit di un file.
Nel nostro specifico caso, per attivare le actions è necessario andare prima su Settings, poi su Pages, quindi Build and Deployment e selezionare, dal menù a tendina l'opzione "**GitHub Actions**".

A questo punto si crea una o più actions, andando su Actions e creando uno o più file yml. I due file che ho usato io sono:
- build.yml
- pages.yml
Il primo è il seguente:
```
# build.yml
name: Mdbook build

on:
  push:
    branches: ["main"]

jobs:
  build:
    name: build
    runs-on: ubuntu-latest
    env:
      MDBOOK_VERSION: '0.4.12'
      MDBOOK_LINKCHECK_VERSION: '0.7.4'
      MDBOOK_MERMAID_VERSION: '0.8.3'
    steps:
    - uses: actions/checkout@v2
      with:
        submodules: true
    - name: Install mdbook
      run: |
        mkdir ~/tools
        curl -L https://github.com/rust-lang/mdBook/releases/download/v$MDBOOK_VERSION/mdbook-v$MDBOOK_VERSION-x86_64-unknown-linux-gnu.tar.gz | tar xz -C ~/tools
        curl -L https://github.com/badboy/mdbook-mermaid/releases/download/v$MDBOOK_MERMAID_VERSION/mdbook-mermaid-v$MDBOOK_MERMAID_VERSION-x86_64-unknown-linux-gnu.tar.gz | tar xz -C ~/tools
        curl -L https://github.com/Michael-F-Bryan/mdbook-linkcheck/releases/download/v$MDBOOK_LINKCHECK_VERSION/mdbook-linkcheck.v$MDBOOK_LINKCHECK_VERSION.x86_64-unknown-linux-gnu.zip -O
        unzip mdbook-linkcheck.v$MDBOOK_LINKCHECK_VERSION.x86_64-unknown-linux-gnu.zip -d ~/tools
        chmod +x ~/tools/mdbook-linkcheck
        curl -s https://api.github.com/repos/zjp-CN/mdbook-theme/releases/latest \
               | grep browser_download_url \
               | grep mdbook-theme_linux \
               | cut -d '"' -f 4 \
               | wget -qi -
        tar -xzf mdbook-theme_linux.tar.gz -C ~/tools
        echo ~/tools >> $GITHUB_PATH
    - name: Build
      run: mdbook build
    # share between different jobs
    - uses: actions/upload-artifact@v3
      with:
        name: book
        path: book/
```

mentre il secondo è:
```
# pages.yml
# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]
  workflow_run:
    workflows: ["Mdbook build"]
    types:
      - completed

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Disallow one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      # actions/download-artifact@v3 does not allow sharing across workflows
      - name: Download artifact
        id: download-artifact
        uses: dawidd6/action-download-artifact@v2
        with:
          name: book
          path: book/
          workflow: build.yml
      - name: Setup Pages
        uses: actions/configure-pages@v2
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: book
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

A questo punto è tutto pronto. Ad ogni commit dei file su github, si avvieranno in automatico le Actions che si occuperanno di buildare il sito correttamente ogni volta.
