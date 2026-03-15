# HidroLog Amazônia — GitHub Pages Edition

## Estrutura de Arquivos

```
hidrolog-ghpages/
├── index.html                      ← Página principal (SPA)
├── 404.html                        ← Redireciona URLs diretas para index
├── .nojekyll                       ← Desabilita Jekyll (obrigatório)
├── _config.yml                     ← Configuração GitHub Pages
├── robots.txt                      ← SEO
├── sitemap.xml                     ← Mapa do site
├── css/styles.css                  ← Todos os estilos
├── js/main.js                      ← Navegação + History API + SPA routing
├── js/pages.js                     ← Conteúdo das páginas internas
├── img/                            ← Pasta para imagens futuras
└── .github/workflows/deploy.yml   ← Deploy automático via GitHub Actions
```

---

## Publicar no GitHub Pages — Passo a Passo

### Método 1 — Upload pelo site (mais simples)

1. Acesse https://github.com/new e crie um repositório **Public**
2. Clique em **"uploading an existing file"**
3. Arraste todos os arquivos desta pasta (incluindo `.nojekyll`, `_config.yml`, `.github/`)
4. Commit: `Initial deploy HidroLog Amazônia`
5. Vá em **Settings → Pages → Source: GitHub Actions**
6. Deploy automático em ~1 minuto
7. URL: `https://SEU-USUARIO.github.io/NOME-DO-REPO/`

### Método 2 — Via Git (para atualizações frequentes)

```bash
git clone https://github.com/SEU-USUARIO/REPO.git
cd REPO
# copie todos os arquivos desta pasta para cá
git add .
git commit -m "Deploy HidroLog v1.0"
git push origin main
```

---

## Domínio Personalizado

Para usar `hidrolog.com.br`:

1. GitHub → Settings → Pages → Custom domain: `hidrolog.com.br` → Save
2. Marque **Enforce HTTPS**
3. No registrador de domínio, adicione DNS:

| Tipo  | Nome | Valor                   |
|-------|------|-------------------------|
| A     | @    | `185.199.108.153`       |
| A     | @    | `185.199.109.153`       |
| A     | @    | `185.199.110.153`       |
| A     | @    | `185.199.111.153`       |
| CNAME | www  | `SEU-USUARIO.github.io` |

---

## Como Funciona o Roteamento SPA

O site usa uma técnica padrão para SPAs no GitHub Pages:

```
URL /servicos acessada diretamente
  → GitHub Pages: "arquivo não existe" → serve 404.html
  → 404.html: grava "servicos" no sessionStorage → redireciona para /
  → index.html: main.js lê sessionStorage → showPage('servicos')
  → Usuário vê Serviços, URL atualizada para /servicos ✅
```

O botão Voltar do navegador também funciona corretamente via History API.

---

## Ativar o Formulário de Contato (Formspree — gratuito)

1. Cadastre-se em https://formspree.io
2. Crie um formulário e copie o endpoint (ex: `https://formspree.io/f/xabcdefg`)
3. Em `js/main.js`, localize o comentário `Para ativar Formspree`
4. Descomente o bloco `fetch()` e substitua `SEU_ID`
5. Delete o `setTimeout` abaixo

---

## Atualizar o Site

```bash
git add .
git commit -m "Atualização: descrição"
git push origin main
# GitHub Actions publica em ~1 minuto
```

Acompanhe o deploy em: github.com/SEU-USUARIO/REPO → aba **Actions**
