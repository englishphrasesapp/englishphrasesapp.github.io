# AGENTS.md

## Visão geral do projeto

Site estático do aplicativo **English Phrases**, publicado pelo GitHub Pages em
<https://englishphrasesapp.github.io/>.

Este repositório é independente do projeto Flutter do app. Ele contém apenas a
landing page, as páginas de política de privacidade e os assets do site. Não há
build, backend, banco de dados, framework de JavaScript, analytics ou cookies de
rastreamento.

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
│   ├── app-icon.png
│   ├── app-icon-192.png
│   └── capturas/               # capturas reais do app no iPhone 12
├── 404.html
├── robots.txt
├── sitemap.xml
├── .nojekyll
└── README.md
```

## Escopo de divulgação

- Na primeira fase, a landing page divulga **apenas Android e iOS**.
- Não adicionar macOS, Windows, Linux ou Web à landing sem uma decisão explícita
  de produto.
- A política de privacidade continua cobrindo todas as plataformas do código,
  com uma nota de que a distribuição pública atual é mobile. Não remover essa
  nota nem restringir a política sem alinhamento.
- Não criar links de loja inexistentes. Enquanto o app não estiver publicado,
  usar **“Em breve para Android e iOS”**.
- Não inventar avaliações, depoimentos, prêmios, números de usuários ou recursos
  que o app ainda não tenha.

## Conteúdo e tradução

- O app **exibe traduções já cadastradas ou importadas**. Ele **não traduz
  frases automaticamente**.
- A IA local gera novas frases com tradução, mas **não é um tradutor de frases
  existentes**.
- Nunca usar expressões como “traduza frases”, “tradução automática”,
  “tradução instantânea” ou equivalentes em inglês.
- Ao falar dos 14 idiomas, deixar claro que são **idiomas de interface** e que o
  campo de tradução aceita qualquer idioma.
- Manter as versões PT e EN sincronizadas em conteúdo, links, metadados e tom.
- Contato oficial: `englishphrases.app@gmail.com`.

## Regras técnicas

- Usar apenas HTML e CSS estáticos. Não adicionar frameworks, bundlers,
  `package.json`, JavaScript de aplicação, fontes externas, analytics, pixels ou
  cookies de rastreamento.
- Usar caminhos absolutos para links e assets internos:
  `/assets/...`, `/privacidade/`, `/privacidade/en/` e `/en/`.
- Manter em todas as páginas:
  - `lang` correto (`pt-BR` ou `en`);
  - meta description;
  - canonical;
  - `hreflang` para PT, EN e `x-default`;
  - Open Graph e Twitter Card;
  - JSON-LD quando aplicável.
- Acessibilidade:
  - HTML semântico e hierarquia de headings;
  - skip link;
  - `alt` em todas as imagens;
  - foco visível;
  - contraste adequado;
  - respeito a `prefers-reduced-motion`.
- Responsividade:
  - validar em 360, 390, 430, 768, 1024 e 1440 px;
  - não permitir overflow horizontal;
  - manter o layout mobile com texto antes das capturas.
- Imagens:
  - usar WebP com fallback PNG via `<picture>`;
  - `loading="lazy"` e `decoding="async"` abaixo da dobra;
  - `fetchpriority="high"` apenas na imagem principal;
  - manter `width` e `height` para evitar layout shift.
- Não commitar `.DS_Store`, arquivos temporários ou segredos.

## Capturas de tela

As capturas são reais, feitas no simulador do **iPhone 12**, com o app em
português e inglês, nos temas claro e escuro.

- Não capturar anúncios, cartões de consentimento do Firebase, notificações ou
  dados pessoais.
- Manter a frase principal e a tradução visíveis.
- Nomes atuais:
  - `visualizar-claro.png` / `.webp`
  - `frases-claro.png` / `.webp`
  - `criar-claro.png` / `.webp`
  - `visualizar-escuro.png` / `.webp`
  - os mesmos nomes com sufixo `-en` para a interface em inglês.
- Redimensionar para 900 px de largura e gerar WebP:

```bash
cd assets/capturas
for f in *.png; do
  sips --resampleWidth 900 "$f" >/dev/null
  cwebp -quiet -q 82 "$f" -o "${f%.png}.webp"
done
```

## Privacidade

- A política deve refletir o comportamento real do app:
  - dados locais;
  - AdMob com anúncios não personalizados (NPA), UMP e sem ATT/IDFA;
  - Firebase Analytics e Crashlytics opcionais;
  - IA local, IA do sistema e downloads do Hugging Face;
  - hospedagem do site no GitHub Pages.
- NPA **não** significa coleta zero. Nunca afirmar que o app não coleta nenhum
  dado.
- Não afirmar que o app envia o conteúdo das frases para servidores próprios.
- Manter a data de “última atualização” da política ao alterar o documento.
- Recomendar revisão jurídica antes do lançamento; o texto do site não substitui
  aconselhamento jurídico.

## Publicação

- Repositório remoto: `englishphrasesapp/englishphrasesapp.github.io`.
- Branch publicada: `main`.
- GitHub Pages: **Deploy from a branch → main → / (root)**.
- **Nunca fazer commit ou push sem solicitação explícita.**
- Antes de publicar, validar localmente e revisar o diff.
- Após o push, confirmar que o conteúdo novo apareceu nas URLs públicas. O
  deploy do GitHub Pages pode levar alguns minutos e o CDN pode manter cache por
  até 10 minutos.
- Atualizar `README.md` e `sitemap.xml` quando a estrutura, o escopo ou as URLs
  mudarem.

## Validação local

```bash
python3 -m http.server 8765
```

- Abrir `/`, `/en/`, `/privacidade/` e `/privacidade/en/`.
- Verificar o 404 personalizado em uma URL inexistente.
- Conferir links internos e assets.
- Testar as larguras mobile, tablet e desktop.
- Não rodar `flutter analyze` nem `flutter test` neste repositório; eles
  pertencem ao projeto do app.

## Commits

- Só commitar quando o usuário pedir explicitamente.
- Mensagens curtas e descritivas, em português, por exemplo:
  - `Ajusta landing para Android/iOS e esclarece tradução`
  - `Atualiza política de privacidade`
  - `Atualiza capturas do app`
- Não incluir mudanças não relacionadas no mesmo commit.
