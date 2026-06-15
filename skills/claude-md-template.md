# Template de `claude.md` (framework CODA)

> **O que e:** um modelo limpo de arquivo de contexto para o seu projeto. Ele da ao agente de IA
> (Claude Code, AntiGravity, etc.) o "mapa mental" do repositorio: como o projeto e montado,
> onde as coisas ficam, como rodar, como testar e o que conta como "pronto".
>
> **Onde salvar:** na raiz do projeto, como `claude.md` (ou `CLAUDE.md`). O mesmo conteudo
> funciona como **`Gemini.md`** se voce usa o Gemini/Antigravity — basta copiar o arquivo com o
> outro nome. Muitos agentes leem automaticamente esse arquivo no inicio da sessao.
>
> **Como usar:** copie tudo abaixo da linha divisoria, cole no seu `claude.md` e preencha os
> campos entre `<...>`. Apague o que nao se aplica. Quanto mais especifico e curto, melhor: o
> objetivo e orientar, nao escrever um livro.
>
> **Framework CODA** (a espinha do template):
> - **C — Contexto:** stack, diretorios e o que o projeto faz.
> - **O — Operacao:** comandos para rodar, buildar e testar.
> - **D — Definicao de pronto:** criterios de sucesso (o checklist).
> - **A — Acordos:** regras do projeto que o agente deve sempre respeitar.

---

# <NOME DO PROJETO> — Contexto para a IA

> Resumo em uma linha: <o que este projeto faz, para quem>.

## Tech Stack

- **Linguagem(ns):** <ex.: TypeScript, Python 3.12>
- **Framework / runtime:** <ex.: Next.js 14 (App Router), Node 20>
- **UI / estilo:** <ex.: React + Tailwind CSS>
- **Banco / storage:** <ex.: Supabase (Postgres), ou "nenhum">
- **Hospedagem / deploy:** <ex.: Vercel>
- **Gerenciador de pacotes:** <ex.: npm / pnpm / uv>
- **Outras libs relevantes:** <ex.: Zod, Prisma, Framer Motion>

## Diretorios-chave

> So o que importa para navegar. Nao liste o repositorio inteiro.

```
src/            <codigo da aplicacao>
src/app/        <rotas / paginas>
src/components/ <componentes de UI reutilizaveis>
src/lib/        <utilidades, clients, helpers>
tests/          <testes automatizados>
public/         <assets estaticos>
```

- **Ponto de entrada:** <ex.: `src/app/page.tsx` / `src/main.py`>
- **Configuracao:** <ex.: `.env.local`, `config/*.ts`>
- **Onde NAO mexer:** <ex.: `src/generated/` e gerado por codegen — nao editar a mao>

## Comandos

| Acao | Comando |
|------|---------|
| Instalar dependencias | `<npm install>` |
| Rodar em desenvolvimento | `<npm run dev>` |
| Build de producao | `<npm run build>` |
| Rodar os testes | `<npm test>` |
| Lint / formatacao | `<npm run lint>` |
| Type-check | `<npm run typecheck>` |

> Se um comando precisar de variaveis de ambiente, indique aqui quais (sem expor segredos).

## Criterios de sucesso (Definicao de Pronto)

Uma mudanca so esta concluida quando TODOS estes itens passam:

- [ ] **Roda sem erros** — a aplicacao sobe e a funcionalidade funciona de ponta a ponta.
- [ ] **Testes passam** — a suite de testes esta verde (`<comando de teste>`).
- [ ] **Sem warnings de lint** — `<comando de lint>` nao aponta problemas novos.
- [ ] **Faz o que foi pedido** — atende exatamente ao pedido original, nem mais nem menos.
- [ ] **Mudancas explicaveis** — da para descrever, em linguagem simples, o que mudou e por que.

> Se algum criterio nao puder ser satisfeito, pare e relate em vez de "forcar" a entrega.

## Como testar

> Diga a IA como verificar de verdade — nao apenas "rode os testes".

1. **Automatizado:** `<comando>` — cobre <o que cobre>.
2. **Manual (smoke test):** suba com `<npm run dev>`, abra `<URL/rota>` e confirme que
   <comportamento esperado>.
3. **Casos a checar sempre:** <ex.: estado vazio, erro de rede, input invalido, mobile>.
4. **Antes de concluir:** rode lint + type-check e revise o `git diff`.

## Regras do projeto (Acordos)

> Restricoes que o agente deve respeitar SEMPRE, mesmo sem ser lembrado.

- **Escopo cirurgico:** faca a menor mudanca que resolve o problema. Nao refatore o que nao
  foi pedido.
- **Nao crie arquivos desnecessarios.** Prefira editar o existente a criar novo. Nada de
  documentacao/README sem pedido explicito.
- **Segredos:** nunca commitar chaves, tokens ou `.env`. Para variaveis de ambiente, declare o
  nome e peca a chave ao usuario — nao invente valores.
- **Padroes de codigo:** siga o estilo ja presente no repositorio (nomes, formatacao, padroes).
- **Dependencias:** nao adicione bibliotecas novas sem necessidade clara; prefira o que ja existe.
- **Commits:** <convencao do projeto, ex.: Conventional Commits>. So commitar/pushar quando pedido.
- **Antes de mudancas grandes:** explique o plano e espere confirmacao.
- **Em caso de duvida:** pergunte em vez de assumir. Liste suposicoes quando precisar seguir.

---

> **Dica:** mantenha este arquivo curto e atualizado. Quando o projeto mudar (nova stack, novo
> comando, nova regra), atualize aqui — e o agente atualiza junto. Para o Gemini/Antigravity,
> copie este arquivo como `Gemini.md`.
