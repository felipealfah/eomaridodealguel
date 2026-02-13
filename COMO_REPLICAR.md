# 🔄 Como Replicar Este Template Para Seus Projetos

Este guia explica como usar este template como base para criar novos projetos de SEO Local.

## 📋 Índice Rápido

1. [Copiar Estrutura](#copiar-estrutura)
2. [Customizações Essenciais](#customizações-essenciais)
3. [Adicionar Conteúdo](#adicionar-conteúdo)
4. [Deploy](#deploy)

---

## 📦 Copiar Estrutura

### Opção 1: Clone Simples (Recomendado)

```bash
# 1. Copie a pasta Template para um novo projeto
cp -r /Users/felipefull/Documents/localseo/Template /Users/felipefull/Documents/localseo/SeuProjeto

# 2. Entre na pasta
cd /Users/felipefull/Documents/localseo/SeuProjeto

# 3. Instale as dependências
npm install

# 4. Inicie o dev server
npm run dev
```

### Opção 2: Git (Para Versionamento)

```bash
# 1. Clone como novo repositório
git clone /Users/felipefull/Documents/localseo/Template /seu/novo/path

# 2. Remova histórico anterior (opcional)
cd /seu/novo/path
rm -rf .git
git init

# 3. Instalações
npm install
```

---

## 🎨 Customizações Essenciais

### 1. Atualizar `astro.config.mjs`

```javascript
// Altere a URL do site para produção
export default defineConfig({
  site: 'https://seudominio.com.br',  // ← Seu domínio aqui
  // ... resto da config
});
```

### 2. Atualizar `src/layouts/BaseLayout.astro`

Altere informações da organização que aparecem em todos os schemas:

```astro
const organizationSchema = {
  "@type": "Organization",
  "name": "Seu Nome da Empresa",  // ← Seu nome
  "url": "https://seudominio.com.br",  // ← Seu domínio
  "logo": "https://seudominio.com.br/logo.png",  // ← Seu logo
  "contactPoint": {
    "telephone": "+55-11-XXXXX-XXXX",  // ← Seu telefone
    "email": "contato@seudominio.com.br"  // ← Seu email
  },
  // ... resto
};
```

### 3. Atualizar Páginas Principais

#### `/sobre.astro`
```astro
- Altere a história da empresa
- Atualize nomes e bios do time
- Mude números de stats (clientes, anos, etc)
- Customize missão, visão e valores
```

#### `/servicos.astro`
```astro
- Adicione/remova serviços conforme necessário
- Atualize preços (ou remova se sob consulta)
- Customize descrição de cada serviço
- Ajuste features e benefícios
```

#### `/contato.astro`
```astro
- Atualize email, telefone, endereço
- Customize URL do formulário (action="/api/contact")
- Adicione links corretos das redes sociais
- Customize FAQs com suas próprias perguntas
```

### 4. Atualizar Header e Footer

**`src/components/Header.astro`:**
```astro
<a href="/" class="text-2xl font-bold text-primary">
  SEU LOGO OU TEXTO
</a>
```

**`src/components/Footer.astro`:**
- Atualize nome da empresa
- Adicione anos no copyright
- Customize links e informações

---

## 📝 Adicionar Conteúdo

### Adicionar Imagens

```bash
# 1. Crie pasta para imagens
mkdir src/assets/images

# 2. Coloque as imagens lá
# Formatos recomendados: webp, avif, png

# 3. Use no componente OptimizedImage
```

**Usar em componentes:**

```astro
import { OptimizedImage } from '@components/OptimizedImage.astro';
import minha_imagem from '@assets/images/minha-imagem.webp';

---

<OptimizedImage 
  src={minha_imagem}
  alt="Descrição da imagem"
  width={400}
  height={300}
/>
```

### Alterar Cores

Cores estão definidas em `tailwind.config.ts` e CSS:

```css
/* src/styles/global.css */
:root {
  --color-primary: #0066cc; /* Altere aqui */
}
```

Ou no Tailwind:

```javascript
// tailwind.config.ts
export default {
  theme: {
    extend: {
      colors: {
        primary: '#seu-azul', // ← Sua cor
      }
    }
  }
}
```

### Alterar Fonts

```astro
<!-- No BaseLayout.astro -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preload" href="https://fonts.googleapis.com/css2?family=SuaFont:wght@400;600;700&display=swap" as="style" />
```

---

## 🔗 Criar Novas Páginas

### Exemplo: Criar página `/blog`

```astro
// src/pages/blog.astro
---
import BaseLayout from '@layouts/BaseLayout.astro';
import Breadcrumb from '@components/Breadcrumb.astro';

const breadcrumbItems = [
  { name: 'Início', url: '/' },
  { name: 'Blog', url: '/blog' }
];
---

<BaseLayout 
  title="Blog - Seu Site"
  description="Artigos sobre SEO Local"
>
  <Breadcrumb items={breadcrumbItems} />
  
  <section class="py-20">
    <div class="container">
      <!-- Seu conteúdo aqui -->
    </div>
  </section>
</BaseLayout>
```

---

## 📱 Testar Responsividade

```bash
# Dev server já roda em localhost:4321
npm run dev

# Teste em diferentes resoluções:
# - Desktop: 1920x1080
# - Tablet: 768x1024
# - Mobile: 360x800 (teste crítico)
```

**DevTools Chrome:**
- F12 → Ctrl+Shift+M → Selecione dispositivos

---

## 🔍 Lighthouse & Performance

```bash
# Build para produção
npm run build

# Auditoria local (requer serve)
npx lighthouse http://localhost:3000 \
  --chrome-flags="--headless=new" \
  --output=json

# Scores esperados:
# - Performance: 75+
# - Accessibility: 90+
# - Best Practices: 90+
# - SEO: 100
```

---

## 🚀 Deploy

### Option 1: Vercel (Recomendado para Astro)

```bash
# 1. Instale Vercel CLI
npm i -g vercel

# 2. Faça deploy
vercel

# 3. Configure domínio
# - Siga instruções do Vercel
```

### Option 2: Netlify

```bash
# 1. Build para produção
npm run build

# 2. Deploy pasta dist/
# - Arraste pasta dist para Netlify
# - Ou use Netlify CLI
```

### Option 3: Servidor Próprio

```bash
# 1. Build
npm run build

# 2. Upload pasta dist/ via FTP/SSH
# 3. Configure .htaccess (já incluído)
# 4. Configure SSL
```

---

## 📋 Checklist de Customização

### Essencial
- [ ] Atualizar astro.config.mjs com seu domínio
- [ ] Atualizar BaseLayout.astro com dados da empresa
- [ ] Customizar /sobre com história real
- [ ] Customizar /servicos com seus serviços
- [ ] Customizar /contato com contatos reais
- [ ] Adicionar logo da empresa
- [ ] Adicionar fotos/imagens

### Recomendado
- [ ] Alterar cores para brand da empresa
- [ ] Customizar fonts
- [ ] Adicionar mais páginas se necessário
- [ ] Criar API para formulário de contato
- [ ] Integrar Google Analytics
- [ ] Setup Google Search Console

### Antes de Deploy
- [ ] Teste em mobile (360px)
- [ ] Lighthouse audit (75+ performance)
- [ ] Teste todas as páginas
- [ ] Teste formulário de contato
- [ ] Verificar links internos
- [ ] Verificar meta tags

---

## 🆘 Troubleshooting

### Dev server não inicia
```bash
# Limpe cache
rm -rf node_modules .astro dist
npm install
npm run dev
```

### Erro de build
```bash
# Verify TypeScript
npx tsc --noEmit

# Check imports
npm run build -- --verbose
```

### Performance ruim em produção
```bash
# Verifique compressão
npm run build
# Cheque tamanho em dist/

# Rode Lighthouse
npx lighthouse seu-site.com --output=json
```

---

## 📚 Recursos Úteis

- [Astro Documentation](https://docs.astro.build)
- [Tailwind CSS](https://tailwindcss.com)
- [Google SEO Starter Guide](https://developers.google.com/search/docs)
- [Core Web Vitals Guide](https://web.dev/vitals/)

---

## 🎉 Dúvidas?

Este template está pronto para produção e facilmente customizável. Siga o checklist e você terá um site profissional em poucos minutos!

**Boa sorte com seu projeto! 🚀**
