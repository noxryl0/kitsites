# Kitsites — sites prontos para vender

Kit com **5 templates** de site configuráveis por cliente, um **gerador** que
produz o site + a proposta comercial, e um **playbook de vendas**. Objetivo:
montar sites profissionais e vendê-los rápido (delivery, clínicas, comércio local).

## Templates
| Template | Para quem | O que faz |
|---|---|---|
| `landing` | qualquer negócio/serviço | **Landing page dark premium** de alta conversão (hero, benefícios, serviços, depoimentos, FAQ, formulário → WhatsApp) |
| `delivery` | pizzaria, lanchonete, açaí, restaurante | Cardápio digital com carrinho e **pedido no WhatsApp** |
| `profissional` | psicóloga, clínica, consultoria | Site institucional com **agendamento no WhatsApp** |
| `vitrine` | barbearia, salão, estética, serviços | One-page de conversão com contato e mapa |
| `conversao` | infoproduto, oferta única, promoção | Landing page com oferta, preço e CTA |
| `catalogo` | loja, doceria, artesanato | Catálogo com seleção e **pedido no WhatsApp** |

## Requisitos
- Node 18+ e npm

## Instalação
```bash
npm install
npm run dev        # abre o template de exemplo (cliente.json)
```

## Como o kit funciona
Todos os dados do cliente ficam em **um arquivo**: `src/config/cliente.json`.
Trocar de cliente = trocar esse arquivo. O gerador faz isso para você em lote.

### Ver todos os dados que dá pra configurar
Abra `src/config/cliente.json` (exemplo completo) e `src/config/client.ts`
(tipos e campos). Resumo:

```jsonc
{
  "template": "delivery",              // delivery | profissional | vitrine | conversao | catalogo
  "marca":  { "nome", "slogan", "logo", "simbolo", "corMarca", "corMarcaEscura", "corMarcaClara" },
  "contato":{ "whatsapp", "whatsappDisplay", "instagram", "email" },
  "local":  { "cidade", "uf", "endereco", "cep", "mapaUrl" },
  "seo":    { "titulo", "descricao" },
  "dados":  { /* varia por template: categorias, servicos, oferta, horarios... */ }
}
```

## Gerar o site de um cliente (um comando)
1. Copie o exemplo e preencha seus dados e os clientes:
   ```bash
   cp clientes/clientes.exemplo.json clientes/clientes.json
   ```
2. Rode:
   ```bash
   npm run gerar                 # todos os clientes
   npm run gerar -- --slug=x     # só um cliente
   ```
Para cada cliente o gerador:
- gera o site em `dist/<slug>/`
- cria `robots.txt` e `sitemap.xml`
- gera a **proposta** em `vendas/propostas/<slug>.html` (abra e salve em PDF)

## Prévia pronta (para vender)
Monta o site de um negócio em segundos, antes de falar com o dono:
```bash
npm run previa -- --nome="Barbearia do Zé" --whatsapp=5585999998888 \
                   --template=vitrine --cidade="Fortaleza" --uf=CE
```
Saída em `dist/previa-barbearia-do-ze/`. Publique a pasta no **Netlify Drop**
(https://app.netlify.com/drop) e mande o link/vídeo para o cliente.

## Publicar em produção (grátis)
- **Netlify Drop**: arraste a pasta `dist/<slug>/` em https://app.netlify.com/drop.
- **Vercel**: `npx vercel deploy dist/<slug>` (ou conecte o repositório).
- Domínio próprio: aponte depois (vira serviço de upsell).

## Vender
O passo a passo completo está em **[vendas/playbook.md](vendas/playbook.md)**:
oferta, preços por nicho, abordagens, follow-up, objeções, fechamento Pix,
upsell e pedido de indicação. Contrato em `vendas/contratos/contrato.md`.

## Testar (navegação, links e mobile)
Testes automatizados com Playwright na landing page, em **3 viewports**
(celular 390px, tablet 768px, desktop 1280px):
```bash
npm run test:e2e
```
Eles falham se houver link vazio/`#`/âncora inexistente, WhatsApp sem número,
scroll horizontal, ou se algum item de menu não levar à seção. Também geram
**screenshots** de cada seção em `screenshots/<viewport>/`.

## Estrutura
```
kitsites/
├── src/config/           cliente.json + client.ts (tipos e helpers)
├── src/templates/        5 templates
├── ferramentas/          gerar-cliente.cjs, gerar-previa.cjs
├── clientes/             clientes.json + leads.csv
├── vendas/               playbook.md, contratos/, propostas/
└── dist/                 sites gerados (não versionado)
```

## Dicas
- As cores da marca viram variáveis CSS automaticamente (`cliente.json`).
- Fotos: coloque em `public/` e use o caminho `/arquivo.jpg` (ex.: no `logo` ou `galeria`).
- O botão flutuante de WhatsApp aparece em todos os templates se houver `whatsapp`.
# noxryl0
# kitsites
