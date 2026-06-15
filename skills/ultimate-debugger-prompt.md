# Ultimate Debugger Prompt

> ## O que e isto (PT-BR)
>
> O **Ultimate Debugger Prompt** e um prompt-esqueleto, fortemente estruturado, para fazer a IA
> depurar (debugar) seu codigo de forma metodica. Em vez de jogar o erro no chat e torcer, voce
> preenche um template em XML com: o codigo do projeto, o caso de uso da aplicacao, o erro e o
> que voce estava fazendo quando ele aconteceu. A IA entao gera previsoes de causa, investiga o
> codigo, isola o trecho problematico, raciocina passo a passo e entrega instrucoes de correcao.
>
> **Fonte open-source:** este prompt vem do repositorio publico
> **NeuraCerebra-AI / Ultimate-Debugger-Prompt** no GitHub. Credite a fonte original ao
> reutilizar/redistribuir.
>
> ### Como preencher
>
> Existem dois tipos de variaveis no template:
>
> - **Variaveis de ENTRADA (voce preenche):**
>   - `ATTACHED_PROJECT_CODE` — seus arquivos de codigo. Cada arquivo entra dentro de uma tag XML
>     com o nome do arquivo (ex.: `<app.py> ... </app.py>`). Se os arquivos forem pequenos, cole o
>     conteudo dentro; se forem grandes, anexe-os a conversa. (Dica: tirar um print da arvore de
>     pastas e pedir a outra IA para gerar as tags XML acelera muito esse passo.)
>   - `APP_USE_CASE` — descricao curta do que a aplicacao faz.
>   - `USER_TASK` — o que voce (ou o programa) estava fazendo quando o erro/crash ocorreu.
>   - `ERROR` — a mensagem de erro do terminal ou a excecao.
>   - (Opcional) `script_explanations` — explique cada arquivo anexado.
>
> - **Variaveis de SAIDA (a IA preenche — deixe os placeholders como estao):**
>   `PREDICTIONS`, `SCRATCHPAD`, `PROBLEMATIC_CODE`, `STEP_BY_STEP_REASONING`, `EXPLANATION`,
>   `DEBUG_INSTRUCTIONS`. Voce nao escreve nada nelas; sao os campos onde a IA vai trabalhar.
>
> ### Como usar
> 1. Copie o template abaixo.
> 2. Preencha as variaveis de ENTRADA (codigo, caso de uso, tarefa, erro).
> 3. Cole na sua IA de preferencia. Ela vai percorrer o fluxo: avaliacao do erro -> previsoes ->
>    investigacao do codigo -> eliminacao -> causa-raiz -> instrucoes de correcao com snippets.

---

## Template do prompt

```
Variables:  {{'ATTACHED_PROJECT_CODE', 'APP_USE_CASE', 'STEP_BY_STEP_REASONING', 'USER_TASK', 'ERROR', 'DEBUG_INSTRUCTIONS', 'PROBLEMATIC_CODE', 'PREDICTIONS', 'EXPLANATION', 'SCRATCHPAD'}}

************************

Role:  You are an intelligent, thorough, and helpful software developer debugging AI. Your task is to  Conduct a thorough analysis of a specific 'ERROR' encountered when performing the 'USER_TASK' when running the program/script displayed in the 'ATTACHED_PROJECT_CODE'.

Generate 'PREDICTIONS' for possible causes for the error.

Perform a meticulous investigation of the 'ATTACHED_PROJECT_CODE' to find the 'PROBLEMATIC_CODE', with the goal of narrowing the predictions to the most likely one.

You will show your work in the 'SCRATCHPAD'.  Brainstorm and develop the plan to identify and correct the error through 'STEP_BY_STEP_REASONING'. Then provide a detailed 'EXPLANATION' with comprehensive step-by-step 'DEBUG_INSTRUCTIONS'.

Remember to focus on providing a clear, well-explained solution and debugging guide, ensuring the error is not only resolved but also understood in the context of the app's operation and development. Then write corrected code snippets and then the code you are replacing with that. You must ensure there are paragraph breaks after each XML tags and numbered lists have proper formatting in your response.  Ensure response is around 8000 tokens and are comprehensive and detailed.

<attached_project_code>

<YOUR_FILE_1.py>
{{Attached to convo}}
</YOUR_FILE_1.py>

<YOUR_FILE_2.py>
{{Attached to convo}}
</YOUR_FILE_2.py>

<YOUR_FILE_3.log>
{{Attached to convo}}
</YOUR_FILE_3.log>

</attached_project_code>

<app_use_case>
{{WRITE YOUR APP/PROGRAM USE CASE}}
</app_use_case>

<script_explanations>
{{EXPLAIN ALL OF YOUR ATTACHED SCRIPTS/FILES}}
</script_explanations>

Here is the error:

<error>
{{INPUT TERMINAL ERROR OR ERROR MESSAGE}}
</error>

The error occurred while the user was performing the following task:

<user_task>
{{EXPLAIN WHAT YOU OR THE PROGRAM WAS DOING WHEN ERROR/CRASH HAPPENED}}
</user_task>

Begin by examining the error code and user task. Research common causes for this type of error and relate these to the specific user task where the error occurs.  Based on your initial assessment, generate five educated predictions regarding potential causes of the error. These predictions should consider various aspects, such as coding mistakes, dependency issues, or resource constraints.

<predictions>
{{PREDICTIONS}}
</predictions>

Dive into the 'ATTACHED_PROJECT_CODE' with your predictions in mind. Methodically review the code segments related to the user task where the 'ERROR' was reported. Pay special attention to recent changes or updates that might have introduced the error.  Analyze the code in the context of each prediction. Use a process of elimination to narrow down the predictions by verifying or disproving each based on code inspection and logical reasoning. Document your rationale behind retaining or discarding each prediction in the scratchpad.

<scratchpad>
{{SCRATCHPAD}}
</scratchpad>

Here is the problematic code segment:

<problematic_code>
{{PROBLEMATIC_CODE}}
</problematic_code>

Document your entire thought process from initial error assessment through prediction formulation, code analysis, and debugging strategy. This narrative should highlight logical deductions, investigative methods, and the rationale for key decisions.

<step_by_step_reasoning>
{{STEP_BY_STEP_REASONING}}
</step_by_step_reasoning>

Select the most likely cause of the error from your remaining predictions. Provide a detailed explanation of why this particular issue is the root cause, referencing specific aspects of the problematic code and how they relate to the error manifestation.

<explanation>
{{EXPLANATION}}
</explanation>

Develop comprehensive, step-by-step instructions for resolving the identified issue. These instructions should be clear and actionable, suitable for a developer with knowledge of software development but possibly unfamiliar with the specific project.

<debug_instructions>
{{DEBUG_INSTRUCTIONS}}
</debug_instructions>

Remember to focus on providing a clear, well-explained solution and debugging guide, ensuring the error is not only resolved but also understood in the context of the app's operation and development. Then write corrected code snippets and then the code you are replacing with that.
```

---

## Tabela de variaveis (referencia rapida)

### Entradas (voce preenche)

| Variavel | Descricao | Formato |
|----------|-----------|---------|
| `ATTACHED_PROJECT_CODE` | Os blocos de codigo dos arquivos do seu projeto. Se forem pequenos, cole dentro das tags; se forem grandes, anexe a conversa. | Tags XML por arquivo: `<YOUR_FILE_1.py>`, `<YOUR_FILE_2.py>`, `<YOUR_FILE_3.log>`, etc. |
| `APP_USE_CASE` | Descricao breve do proposito e da funcionalidade da aplicacao. | Texto simples |
| `USER_TASK` | O que voce/o programa estava fazendo quando o erro ocorreu. | Texto simples |
| `ERROR` | A mensagem de erro / excecao encontrada. | Texto simples ou trecho de codigo |

### Saidas (a IA preenche — nao mexer)

| Variavel | Descricao |
|----------|-----------|
| `PREDICTIONS` | Hipoteses educadas da IA para as causas do erro. |
| `SCRATCHPAD` | Area onde a IA documenta raciocinio e analise durante a depuracao. |
| `PROBLEMATIC_CODE` | O trecho de codigo identificado como causa-raiz. |
| `STEP_BY_STEP_REASONING` | Explicacao detalhada do processo de depuracao, da avaliacao inicial a causa-raiz. |
| `EXPLANATION` | Por que aquele trecho e a causa provavel do erro. |
| `DEBUG_INSTRUCTIONS` | Passo a passo para corrigir o problema. |

---

## Como a IA raciocina (fluxo)

1. **Avaliacao do erro** — examina a mensagem de erro e a tarefa do usuario.
2. **Geracao de previsoes** — cria hipoteses (cinco) de causa.
3. **Investigacao do codigo** — revisa os trechos ligados a tarefa e ao erro.
4. **Estreitamento** — por eliminacao, valida ou descarta cada hipotese.
5. **Causa-raiz** — escolhe a mais provavel e explica o porque.
6. **Instrucoes de correcao** — passo a passo acionavel, com snippets corrigidos e o codigo
   que esta sendo substituido.

---

> **Credito:** prompt original de **NeuraCerebra-AI / Ultimate-Debugger-Prompt** (GitHub),
> projeto open-source. Este arquivo transcreve o template fielmente e adiciona um guia em PT-BR;
> mantenha o credito a fonte ao redistribuir.
