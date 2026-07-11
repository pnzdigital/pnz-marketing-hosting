# pnz-marketing-hosting

Host de mídia da PNZ Digital. Serve os JPEG dos loops de conteúdo por URL
pública, pra o Metricool consumir na hora de agendar/publicar.

- **Domínio:** hosting.marketing.pnzdigital.com.br (Coolify, VPS netcup)
- **Deploy:** static site a partir da raiz deste repo. Auto-redeploy a cada push.
- **Fonte:** github.com/pnzdigital/pnz-marketing-hosting

## Estrutura

```
index.html                       landing interna (noindex)
<cliente>/<slug>/NN.jpg          mídia de cada post do loop
  ex: pnz/diagnostico-2026-07-11/01.jpg
```

URL final que vai pro Metricool:
`https://hosting.marketing.pnzdigital.com.br/<cliente>/<slug>/01.jpg`

## Como a mídia chega aqui (automático)

O loop de posts (`marketing/loop-kit`) renderiza os JPEG e roda o script de
push, que copia `posts/<slug>/out/*.jpg` pra `<cliente>/<slug>/` neste repo,
faz commit e `git push`. O Coolify detecta o push e publica. Nenhum passo manual.

## Configuração do Coolify (netcup)

- App tipo **Static** apontando pra este repo, branch `main`, publish dir = raiz.
- Domínio `hosting.marketing.pnzdigital.com.br` com SSL.
- Sem build (é HTML/JPEG puro).
