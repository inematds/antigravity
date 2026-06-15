# Biblioteca de Prompts

> Coletanea de prompts prontos para usar no dia a dia com agentes de IA de programacao
> (Claude Code, AntiGravity, Cursor, etc.). Cada prompt tem: **titulo**, **quando usar** e o
> **prompt** em bloco — copie, adapte os campos entre `<...>` e cole no chat do agente.
>
> Dica geral: seja especifico sobre o objetivo, peca perguntas clarificadoras quando o pedido
> for grande, e prefira mudancas pequenas e verificaveis.

---

## a) Definir o problema → SOP

**Quando usar:** no inicio de uma tarefa, quando voce sabe o problema mas ainda nao tem um
procedimento claro. Transforma um problema solto em um SOP (procedimento operacional padrao)
reutilizavel.

```
Quero transformar o problema abaixo em um SOP (procedimento operacional padrao) claro,
passo a passo, que eu (ou a IA) possa seguir e repetir depois.

Problema / objetivo:
<descreva o problema, o resultado esperado e qualquer restricao>

Faca:
1. Reformule o problema em uma frase precisa (o que e "pronto").
2. Liste os pre-requisitos e insumos necessarios.
3. Escreva o SOP como uma lista numerada de passos acionaveis, cada um com um criterio de
   verificacao ("como sei que este passo deu certo").
4. Aponte os riscos/pontos de falha mais provaveis e como evita-los.
Se faltar informacao essencial, pergunte antes de escrever o SOP.
```

---

## b) Plan Mode / Outline (specs antes de codar)

**Quando usar:** antes de escrever qualquer codigo de uma tarefa nao-trivial. Forca a IA a
planejar e a fazer perguntas clarificadoras antes de implementar. NAO deixe a IA codar ainda.

```
NAO escreva codigo ainda. Primeiro vamos planejar.

Tarefa:
<descreva a funcionalidade/mudanca que voce quer>

Faca, nesta ordem:
1. Liste TODAS as perguntas clarificadoras que voce tem antes de comecar (suposicoes,
   escopo, casos-limite, dependencias). Espere minhas respostas.
2. Depois das respostas, produza uma SPEC/OUTLINE: objetivo, arquivos a criar/alterar,
   abordagem tecnica, passos de implementacao em ordem, e como testar.
3. Aponte trade-offs e a opcao mais simples que resolve.

ultrathink — pense profundamente antes de responder. So comece a implementar quando eu
aprovar o plano.
```

---

## c) Pesquisa → research.md

**Quando usar:** quando a tarefa exige entender algo antes de agir (uma lib nova, uma API, uma
abordagem). Concentra a pesquisa em um arquivo de referencia.

```
Antes de implementar, faca uma pesquisa focada e salve o resultado em um arquivo `research.md`.

Tema da pesquisa:
<o que precisa ser investigado e por que>

No `research.md`, inclua:
1. Resumo executivo (o que descobriu, em poucas linhas).
2. Opcoes/abordagens encontradas, com pros e contras de cada.
3. Trechos de codigo ou exemplos relevantes (com a fonte).
4. Recomendacao final + proximos passos.
5. Links/fontes consultadas.
Seja objetivo e cite de onde veio cada afirmacao importante. Nao implemente nada ainda.
```

---

## d) Design inspiration (referencia visual)

**Quando usar:** ao construir UI e voce quer que a IA siga uma direcao visual especifica (um
site, um print, um estilo) em vez do "visual generico de IA".

```
Vou te dar uma referencia visual para guiar o design desta interface.

Referencia:
<cole o link do site, descreva o estilo, ou anexe um print/imagem>

Faca:
1. Descreva o que define essa referencia: paleta de cores, tipografia, espacamento,
   densidade, formas, sombras, tom (minimalista? ousado? editorial?).
2. Extraia um pequeno "design system" (cores, fontes, raios, espacos) a partir dela.
3. Aplique essa direcao ao componente/pagina abaixo, mantendo coerencia e acessibilidade.

Alvo:
<o que construir / qual tela>

Nao copie a referencia pixel a pixel; capture a ESSENCIA e adapte. Evite o visual generico.
```

---

## e) Review & verify (persona "dev senior cetico")

**Quando usar:** depois que a IA (ou voce) escreveu codigo, antes de considerar pronto. Pega
bugs e simplificacoes que passam batido.

```
Assuma o papel de um DESENVOLVEDOR SENIOR CETICO revisando este codigo. Seu trabalho NAO e
elogiar — e encontrar o que esta errado, fragil ou complicado demais.

Codigo / diff a revisar:
<cole o codigo, o diff, ou aponte os arquivos>

Avalie contra estes criterios e seja direto:
1. Corretude: ha bugs, casos-limite ignorados, condicoes de corrida, nulos nao tratados?
2. Faz o que foi pedido — nem mais (over-engineering) nem menos?
3. Simplicidade: da para fazer mais simples/menor? Ha duplicacao a reaproveitar?
4. Seguranca e tratamento de erro.
5. Legibilidade e consistencia com o resto do projeto.

Para cada problema: descreva, diga ONDE esta e proponha a correcao. Liste do mais grave ao
menos grave. Se algo estiver realmente bom, diga em uma linha — sem enrolacao.
```

---

## f) Troubleshooting por screenshot

**Quando usar:** quando algo esta visualmente quebrado ou dando erro na tela, e e mais facil
mostrar do que descrever. Anexe o print.

```
Estou te enviando um screenshot do problema. Vamos depurar a partir dele.

Anexo: <print da tela/erro>
Contexto: <o que voce estava fazendo; em qual pagina/fluxo; o que esperava ver>

Faca:
1. Descreva o que voce observa no screenshot (erro, layout quebrado, estado inesperado).
2. Liste de 3 a 5 causas provaveis, da mais para a menos provavel.
3. Diga onde olhar no codigo para confirmar cada hipotese.
4. Proponha a correcao mais provavel e como eu verifico que funcionou.
Se precisar de mais algum arquivo ou print para confirmar, peca.
```

---

## g) Conectar MCP (Supabase / GitHub / Vercel)

**Quando usar:** quando voce quer que o agente use um MCP (servidor de ferramentas) ja
configurado — por exemplo, ler o banco no Supabase, abrir um PR no GitHub, ou checar um deploy
na Vercel.

```
Use o MCP do <Supabase | GitHub | Vercel> que ja esta conectado para realizar a tarefa abaixo.

Tarefa:
<o que voce quer que ele faca — ex.: "liste as tabelas e me mostre o schema da tabela users",
 "abra um PR com estas mudancas", "verifique o status do ultimo deploy de producao">

Antes de agir:
1. Confirme que consegue acessar o MCP (faca uma chamada de leitura simples primeiro).
2. Para qualquer acao que ESCREVE/ALTERA (criar PR, mudar dados, disparar deploy), me mostre
   o que pretende fazer e espere meu "ok".
Use o MCP de fato — nao invente os resultados.
```

---

## h) Env var ("nomeie a variavel, eu forneco a chave")

**Quando usar:** quando o codigo precisa de uma chave/segredo. A IA NUNCA deve inventar o valor
nem commitar o segredo — ela so define o nome da variavel e voce fornece a chave.

```
Esta funcionalidade precisa de uma credencial/segredo. NUNCA invente o valor e NUNCA escreva a
chave no codigo ou no repositorio.

Faca:
1. Defina o NOME da variavel de ambiente (ex.: `<SERVICO>_API_KEY`) seguindo o padrao do projeto.
2. Use-a a partir do ambiente (ex.: `process.env.NOME` / `os.environ["NOME"]`), nunca hardcoded.
3. Adicione a entrada no `.env.example` (sem valor) e garanta que `.env` esta no `.gitignore`.
4. Me diga exatamente qual variavel criar e onde — EU vou fornecer a chave.
Resuma no final quais variaveis preciso preencher.
```

---

## i) "Menos e mais"

**Quando usar:** quando a IA esta exagerando — codigo grande demais, abstracoes a mais, mudancas
alem do pedido. Puxa o freio em direcao a simplicidade.

```
Menos e mais. Quero a solucao MAIS SIMPLES que resolve o problema — nada de over-engineering.

Regras:
1. Faca a menor mudanca possivel que atende ao pedido. Nao refatore o que nao foi pedido.
2. Sem abstracoes, camadas ou dependencias novas a menos que sejam realmente necessarias.
3. Prefira reusar o que ja existe no projeto.
4. Se voce ja escreveu algo complexo, simplifique: remova o que nao agrega.

Tarefa / codigo:
<descreva ou cole>

No final, explique em 1-2 frases por que essa versao e suficiente e o que voce deixou de fora
de proposito.
```
