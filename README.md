# English Phrases — site e política de privacidade

Site estático do aplicativo **English Phrases**, publicado pelo GitHub Pages em
<https://englishphrasesapp.github.io/>.

## Escopo de divulgação

Nesta primeira fase, a landing page divulga apenas as versões **Android e iOS**.
A política de privacidade continua cobrindo todas as plataformas do código, com
uma nota de que a distribuição pública atual é mobile.

A landing também deixa explícito que o app **exibe traduções já cadastradas ou
importadas** e **não traduz frases automaticamente**; a IA local gera novas
frases com tradução, mas não é um tradutor de frases existentes.

## Estrutura

```text
.
├── index.html                  # landing page em português
├── en/
│   └── index.html              # landing page em inglês
├── privacidade/
│   ├── index.html              # política de privacidade em português
│   └── en/
│       └── index.html          # política de privacidade em inglês
├── assets/
│   ├── estilo.css
│   ├── app-icon.png            # ícone do app (512 px)
│   ├── app-icon-192.png        # ícone para favicon/touch icon
│   └── capturas/               # capturas reais do app no iPhone 12
│       ├── visualizar-claro.png / .webp
│       ├── frases-claro.png / .webp
│       ├── criar-claro.png / .webp
│       ├── visualizar-escuro.png / .webp
│       └── *-en.png / .webp    # mesmas telas com a interface em inglês
├── 404.html
├── robots.txt
├── sitemap.xml
└── .nojekyll
```

Não há build, dependências de JavaScript, fontes externas, cookies de
rastreamento ou analytics. A página é HTML e CSS puros.

## Rodar localmente

```bash
python3 -m http.server 8000
```

Depois abra <http://localhost:8000/>.

## Publicar

O repositório remoto é `englishphrasesapp/englishphrasesapp.github.io` e o site
é servido pela branch `main`, na raiz:

```bash
git add .
git commit -m "Atualiza o site"
git push origin main
```

No GitHub, em **Settings → Pages**, a origem deve estar configurada como
**Deploy from a branch → main → / (root)**.

## Atualizar as capturas

As capturas foram geradas no simulador do iPhone 12, com o app em português
(`visualizar-claro.png`, etc.) e em inglês (`visualizar-claro-en.png`, etc.),
sempre sem anúncios. Para refazer:

1. Rode o app no simulador com anúncios e Firebase desligados.
2. Use as telas Visualizar, Frases e Criar no tema claro e a Visualizar no
   tema escuro.
3. Salve os PNGs em `assets/capturas/` com os mesmos nomes (sufixo `-en` para
   a interface em inglês).
4. Gere as versões WebP:

```bash
cd assets/capturas
for f in *.png; do cwebp -q 82 "$f" -o "${f%.png}.webp"; done
```

O site usa `<picture>` com WebP e fallback PNG.

## Política de privacidade

A URL pública usada no app, no AdMob e nas lojas é:

```text
https://englishphrasesapp.github.io/privacidade/
```

A versão em inglês fica em `/privacidade/en/`.

## Contato

<englishphrases.app@gmail.com>
