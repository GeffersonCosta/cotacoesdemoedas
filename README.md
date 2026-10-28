# cotacoesdemoedas.com

Site em português com cotações de moeda para quem envia dinheiro entre Portugal e Brasil. Online em [cotacoesdemoedas.com](https://cotacoesdemoedas.com).

> O código-fonte é privado e está disponível a pedido. Este repositório contém apenas a documentação do projeto.

## Porquê

A primeira versão mostrava as cotações só no navegador, por isso os crawlers viam "A carregar..." em vez de dados, e o site foi rejeitado pelo Google AdSense por conteúdo de baixo valor. Este projeto é a reconstrução:

- cotações renderizadas em build, já presentes no HTML que o crawler recebe;
- cada página é uma URL real com um único endereço canónico;
- conteúdo em primeira mão (recibos de transferências próprias, análise de taxas do BCE ao longo de vários anos);
- tudo verificado automaticamente antes de publicar.

## O que tem de interessante

- **Build sem dependências:** scripts Node 20 em ES modules, `fetch` nativo, sem `package.json`.
- **Quality gate:** um verificador falha o build se houver regressões de SEO ou de políticas: metadados obrigatórios e únicos, JSON-LD válido, links internos, sitemap e robots coerentes, anúncios dentro da política, consentimento único, mínimo de palavras nos guias.
- **Publicação agendada:** PRs com a label `publicar:AAAA-MM-DD` são fundidos na data certa (hora de Lisboa), com rebuild e verificação antes do push.
- **Cotações atualizadas por CI:** GitHub Actions corre após a publicação do BCE e só faz commit se as taxas mudarem; se a API falhar, o site mantém a última taxa válida.
- **Painel de operações no Telegram:** Netlify Functions que avisam de previews, deploys, novas páginas e falhas, com estado idempotente e auto-recuperável.

## Stack

| Área | Escolha |
|---|---|
| Site | HTML/CSS/JS puro, gerado em build |
| Build | Node 20, ES modules, sem dependências |
| Dados | Frankfurter API (taxas de referência do BCE) |
| Hosting | Netlify, com Cloudflare à frente |
| CI/CD | GitHub Actions |
| Operações | Netlify Functions, Netlify Blobs, Telegram Bot API, GitHub API |

Desenvolvido com Claude Code no VS Code, por fases e com pontos de aprovação.

## Roadmap

- Fase 2 do bot do Telegram: botões e mensagens por webhook, para submeter conteúdo a partir do Telegram.
- Mais páginas de pares de moedas, cada uma com conteúdo editorial próprio.
- Novo pedido de revisão do AdSense após concluir o trabalho de conteúdo.
