# Regras para agentes

## Fontes de verdade protegidas

- Trate todo o conteúdo de `base/` como somente leitura.
- Nunca edite, substitua, renomeie ou remova um arquivo existente em `base/`, mesmo quando uma skill produzir uma versão melhor.
- A única exceção é a criação inicial feita pela skill `onboarding`: ela pode criar arquivos ausentes em `base/` depois que o usuário aprovar uma proposta concreta. Ela nunca pode sobrescrever um arquivo existente.
- Currículos para vagas pertencem a `vagas/`. Auditorias pertencem a `auditorias/`. Sugestões de alteração da base pertencem a `propostas-base/`.
- Se o usuário pedir uma atualização da base, gere a proposta fora de `base/` e indique o arquivo que ele deve adotar manualmente.
- Arquivos em `base/originais/`, como PDFs exportados do LinkedIn, são evidências fornecidas pelo usuário e também são somente leitura.

`base/cv.md` é a fonte factual principal. `historias.md` é uma memória complementar administrada pelas skills e nunca prevalece sobre a base em caso de conflito.
