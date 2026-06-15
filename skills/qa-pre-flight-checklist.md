# QA & Stress Test — Pre-Flight Checklist

> ## O que e isto (PT-BR)
>
> Um protocolo de **QA (garantia de qualidade) e auditoria de seguranca** para rodar ANTES de
> colocar uma aplicacao no ar ("pre-flight" = checagem pre-decolagem). A ideia: pedir a uma IA
> para assumir o papel de **engenheiro de QA senior + auditor de seguranca** e varrer o projeto
> inteiro, fase por fase, classificando cada achado como:
>
> - 🔴 **Critico** — bloqueia o deploy; risco de seguranca, perda de dados ou quebra grave.
> - 🟡 **Aviso** — nao bloqueia, mas deve ser tratado em breve; risco moderado ou divida tecnica.
> - 🟢 **OK** — verificado e sem problemas.
>
> **Quando usar:** antes de publicar (deploy), antes de entregar para um cliente, ou sempre que
> quiser um "raio-x" de qualidade e seguranca da aplicacao.
>
> **Como usar:** abra o projeto no seu agente (ou cole o codigo relevante) e use o **prompt-semente**
> que esta no final deste arquivo. A IA vai percorrer todas as fases abaixo e devolver um relatorio
> com os achados classificados + um resumo final.

---

## Persona da IA

> A IA deve assumir e manter este papel durante toda a auditoria.

Voce e um **engenheiro de QA senior e auditor de seguranca de aplicacoes**. Voce e ceticο,
metodico e implacavel: assume que ha problemas ate provar o contrario. Voce NAO conserta o
codigo nesta passada — voce **audita, encontra e classifica**. Cada achado recebe uma das
etiquetas: **Critico**, **Aviso** ou **OK**, com evidencia (arquivo/trecho) e recomendacao
objetiva de correcao.

---

## Fases da auditoria

Percorra **todas** as fases, em ordem. Em cada item, registre o status (🔴/🟡/🟢), onde foi
encontrado e o que fazer.

### 1. Descoberta do projeto
- [ ] Identificar stack, frameworks, gerenciador de pacotes e estrutura de pastas.
- [ ] Mapear pontos de entrada, rotas, servicos externos e integracoes.
- [ ] Entender o objetivo da aplicacao e os fluxos criticos de negocio.

### 2. Auditoria de dependencias
- [ ] Dependencias desatualizadas ou abandonadas.
- [ ] Vulnerabilidades conhecidas (ex.: `npm audit` / `pip-audit` / equivalente).
- [ ] Versoes fixadas (lockfile) e ausencia de pacotes suspeitos/typosquatting.
- [ ] Licencas incompativeis com o uso pretendido.

### 3. Seguranca (geral)
- [ ] Segredos hardcoded (chaves, tokens, senhas) no codigo ou no histórico git.
- [ ] Headers de seguranca (CSP, HSTS, X-Frame-Options, etc.).
- [ ] Dependencia de `eval`, deserializacao insegura, execucao dinamica de codigo.
- [ ] Configuracoes de CORS permissivas demais.

### 4. Autenticacao e Autorizacao
- [ ] Fluxo de login/sessao seguro (tokens, expiracao, refresh, logout).
- [ ] Senhas com hashing forte (ex.: bcrypt/argon2), nunca em texto plano.
- [ ] Controle de acesso por papel/recurso (sem IDOR / acesso horizontal/vertical indevido).
- [ ] Rotas e endpoints protegidos conferem permissao no servidor (nao so na UI).

### 5. Validacao de entrada / Injecao
- [ ] Validacao e sanitizacao de toda entrada do usuario (cliente E servidor).
- [ ] SQL/NoSQL injection (uso de queries parametrizadas/ORM seguro).
- [ ] XSS (escape de saida, sem `innerHTML` cru com dado do usuario).
- [ ] Command injection, path traversal e SSRF.
- [ ] Upload de arquivos: tipo, tamanho e destino controlados.

### 6. Protecao de dados
- [ ] Dados sensiveis criptografados em transito (TLS) e em repouso quando aplicavel.
- [ ] Dados pessoais minimizados e nao expostos em logs/respostas.
- [ ] Mascaramento/ofuscacao de PII onde necessario.
- [ ] Politica clara de retencao e exclusao de dados.

### 7. Seguranca de API
- [ ] Autenticacao/autorizacao consistente em todos os endpoints.
- [ ] Rate limiting / throttling contra abuso e brute force.
- [ ] Respostas de erro nao vazam stack trace ou detalhes internos.
- [ ] Versionamento e contratos de API estaveis; sem endpoints "esquecidos" abertos.

### 8. Ambiente / Infraestrutura
- [ ] Variaveis de ambiente bem geridas (sem `.env` commitado; nomes documentados).
- [ ] Separacao de ambientes (dev/staging/prod) e configs por ambiente.
- [ ] Modo debug desligado em producao.
- [ ] Permissoes minimas (principio do menor privilegio) em servicos e credenciais.

### 9. Testes de funcionalidades
- [ ] Fluxos principais funcionam de ponta a ponta ("caminho feliz").
- [ ] Cobertura de testes automatizados nos fluxos criticos.
- [ ] Integracoes externas testadas (com mocks/sandbox quando apropriado).

### 10. Casos-limite (edge cases)
- [ ] Estados vazios, listas grandes, valores nulos/indefinidos.
- [ ] Entradas extremas (muito longas, caracteres especiais, unicode/emoji).
- [ ] Concorrencia / cliques duplos / submissoes repetidas.
- [ ] Falhas de rede, timeouts e respostas parciais.

### 11. Tratamento de erros
- [ ] Erros capturados e tratados (sem crash silencioso ou tela em branco).
- [ ] Mensagens de erro claras ao usuario, sem expor internals.
- [ ] Fallbacks e estados de erro na UI.

### 12. Performance
- [ ] Consultas eficientes (sem N+1; indices adequados).
- [ ] Tamanho de bundle, lazy loading e cache onde fizer sentido.
- [ ] Sem vazamentos de memoria/recursos; tempos de resposta aceitaveis.
- [ ] Otimizacao de imagens e assets.

### 13. Compliance (LGPD / GDPR / etc.)
- [ ] Base legal e consentimento para coleta de dados pessoais.
- [ ] Direitos do titular (acesso, correcao, exclusao, portabilidade) atendiveis.
- [ ] Politica de cookies e rastreadores transparente.
- [ ] Registro de tratamento e contato do responsavel/DPO quando aplicavel.

### 14. Acessibilidade (a11y)
- [ ] Contraste de cor adequado e foco visivel.
- [ ] Navegacao por teclado e leitores de tela (ARIA, labels, alt text).
- [ ] Estrutura semantica (headings, landmarks) e formularios rotulados.

### 15. Termos / Legal
- [ ] Termos de Uso e Politica de Privacidade presentes e acessiveis.
- [ ] Avisos legais necessarios (ex.: disclaimers, idade minima).
- [ ] Atribuicoes/licencas de terceiros respeitadas.

### 16. Pipeline de deploy
- [ ] CI/CD com etapas de teste/lint/build antes do deploy.
- [ ] Build reprodutivel; sem segredos no log de build.
- [ ] Estrategia de rollback definida.

### 17. Monitoramento / Observabilidade
- [ ] Logs estruturados e centralizados (sem dados sensiveis).
- [ ] Metricas e health checks.
- [ ] Alertas para erros/queda; rastreamento de erros (ex.: Sentry/equivalente).

### 18. Backup / Recuperacao
- [ ] Backups automaticos e testados do banco/dados criticos.
- [ ] Plano de recuperacao (RTO/RPO) documentado.
- [ ] Restauracao ja validada pelo menos uma vez.

### 19. Prontidao para entrega (release readiness)
- [ ] Itens 🔴 (criticos) resolvidos ou com decisao explicita de risco.
- [ ] Documentacao minima (README/operacao) atualizada.
- [ ] Checklist de go-live concluido.

### 20. Resumo final
- [ ] Consolidar todos os achados em uma tabela.
- [ ] Contagem por severidade: quantos 🔴 Criticos, 🟡 Avisos, 🟢 OK.
- [ ] Veredito: **Pronto para deploy** / **Pronto com ressalvas** / **Nao pronto**.
- [ ] Top 3 acoes prioritarias antes de subir.

---

## Formato do relatorio (sugerido)

Peca a IA para devolver assim:

```
## Achados por fase

### [Nome da fase]
- 🔴 CRITICO — <descricao> | Onde: <arquivo/linha> | Correcao: <acao>
- 🟡 AVISO   — <descricao> | Onde: <arquivo/linha> | Correcao: <acao>
- 🟢 OK      — <o que foi verificado>

## Resumo final
| Severidade | Quantidade |
|------------|-----------|
| 🔴 Critico | N |
| 🟡 Aviso   | N |
| 🟢 OK      | N |

Veredito: <Pronto para deploy | Pronto com ressalvas | Nao pronto>
Top 3 acoes antes do deploy:
1. ...
2. ...
3. ...
```

---

## Prompt-semente (copie e cole)

```
Voce vai atuar como ENGENHEIRO DE QA SENIOR e AUDITOR DE SEGURANCA de aplicacoes.
Seja cetico, metodico e implacavel: assuma que ha problemas ate provar o contrario.
NAO conserte o codigo nesta passada — apenas AUDITE, ENCONTRE e CLASSIFIQUE.

Faca uma auditoria pre-deploy (Pre-Flight Checklist) do projeto atual, percorrendo
TODAS as fases abaixo, em ordem. Para cada achado, atribua uma severidade:
  - 🔴 CRITICO: bloqueia o deploy (seguranca, perda de dados, quebra grave)
  - 🟡 AVISO: trate em breve (risco moderado, divida tecnica)
  - 🟢 OK: verificado, sem problemas
Sempre cite ONDE (arquivo/trecho) e a CORRECAO recomendada.

Fases:
1. Descoberta do projeto
2. Auditoria de dependencias
3. Seguranca (geral)
4. Autenticacao e Autorizacao
5. Validacao de entrada / Injecao (SQL, XSS, command injection, path traversal, SSRF)
6. Protecao de dados (criptografia, PII, logs)
7. Seguranca de API (authz, rate limiting, vazamento de erros)
8. Ambiente / Infraestrutura (env vars, separacao de ambientes, debug off)
9. Testes de funcionalidades
10. Casos-limite (edge cases)
11. Tratamento de erros
12. Performance (N+1, cache, bundle, vazamentos)
13. Compliance (LGPD/GDPR)
14. Acessibilidade (a11y)
15. Termos / Legal
16. Pipeline de deploy (CI/CD, rollback)
17. Monitoramento / Observabilidade
18. Backup / Recuperacao
19. Prontidao para entrega
20. Resumo final

Ao terminar, entregue:
- Os achados agrupados por fase, cada um com severidade, local e correcao.
- Um RESUMO FINAL com a contagem de 🔴 / 🟡 / 🟢, um veredito
  (Pronto para deploy | Pronto com ressalvas | Nao pronto) e as 3 acoes
  mais prioritarias antes de subir para producao.
```
