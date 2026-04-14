# CV Improvements Design — 2026-04-14

## Objetivo

Melhorar o CV de Lucas Sigrist com revisão completa de conteúdo, estrutura e adição de toggle de idioma PT/EN em arquivo único.

## Abordagem Escolhida

**Arquivo único com toggle PT/EN** — um `index.html` com todo o conteúdo em PT e EN embutido, com botão para alternar entre idiomas.

## Arquitetura

### Mecanismo de Toggle
- Botão "🌐 EN" / "🌐 PT" fixo no canto superior direito, ao lado do botão "Salvar PDF"
- Ao clicar, troca classe no `<body>` entre `lang-pt` e `lang-en`
- CSS oculta elementos do idioma inativo com `display: none`
- Preferência salva em `localStorage` para persistir entre visitas
- Impressão captura o idioma ativo automaticamente

### Estrutura do Conteúdo Bilíngue
```html
<span class="pt">Texto em português</span>
<span class="en">English text</span>
```
Pares de elementos com classes `.pt` e `.en`. Elementos que não mudam entre idiomas (tags de skills, datas, ícones) não são duplicados.

### CSS de Idioma
```css
body.lang-pt .en { display: none; }
body.lang-en .pt { display: none; }
```

## Conteúdo

### Resumo
- Reescrever para ser direto e orientado a impacto
- Remover frases genéricas
- Versão EN com tom assertivo em primeira pessoa

### Bullets de Experiência
- Reescrever com foco em resultado, não apenas em atividade
- Usar linguagem de escala onde não houver métricas exatas
- Exemplo de padrão: `[Ação] + [contexto/escala] + [resultado/impacto]`

### Certificação LinuxTips
- Adicionar na sidebar em Formação:
  - PT: **DevOps Professional** — LinuxTips *(em andamento, 2025)*
  - EN: **DevOps Professional Certification** — LinuxTips *(in progress, 2025)*

### LinkedIn Highlights
- Visível apenas na versão PT
- Oculto automaticamente na versão EN via CSS de idioma
- Continua `no-print`

## Visual e UX

- Layout, paleta, tipografia e sidebar permanecem iguais
- Toggle com mesma estética do botão de imprimir (azul, rounded, fixed)
- Transição suave com `transition: opacity 0.2s`
- Botão de toggle oculto no print via `.no-print`

## Entregáveis

1. `index.html` com toggle PT/EN funcional
2. Todo o conteúdo reescrito em PT e EN — bullets com impacto, resumo direto
3. Certificação LinuxTips adicionada na sidebar
4. LinkedIn Highlights oculto na versão EN
