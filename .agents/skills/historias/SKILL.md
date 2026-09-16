---
name: historias
description: Mantém e consulta a base de fatos e histórias ("achados") que o usuário conta nas interações, salva em `historias.md`. Use sempre que o usuário relatar experiências, conquistas, números, ferramentas, projetos, preferências, limitações, disponibilidade ou detalhes de carreira novos ou diferentes dos que estão em `base/cv.md`, para registrá-los; e use ao gerar currículos, auditorias ou perfis, para recuperar fatos já contados em sessões anteriores.
---

# Historias — Fatos e Achados do Usuário

## Quando usar esta Skill

1. **Registrar:** O usuário conta algo novo sobre a trajetória (experiência, resultado, número, ferramenta, projeto, preferência, limitação, disponibilidade, formação) que não está ou está diferente de `base/cv.md`. Adicione uma seção ao final de `historias.md`.
2. **Consultar:** Antes de criar/ajustar currículos (`cv-maker`), auditar (`cv-audit`) ou otimizar perfis, leia `historias.md` para aproveitar fatos já relatados e não repetir perguntas.

## Princípios Básicos

1. **Registre como foi contado:** reproduza o fato no tom e com os detalhes que o usuário usou.
2. **Marque o que não está confirmado:** diferencie "Confirmada", "Não confirmada" e "Estimativa".
3. **Dedupe antes de criar:** pesquise em `historias.md` se o fato já existe. Se existir, atualize. Só adicione seção nova quando for fato novo.
4. **Não apague:** fatos registrados não devem ser removidos. Se algo mudou, adicione nova versão marcando a anterior.
5. **Vincule ao contexto:** relacione o fato à vaga, auditoria ou conversa que o gerou.

## Arquivo

- Localização: `historias.md` na raiz do projeto (ao lado de `base/`).
- Um único arquivo markdown crescente.
- Cada fato é uma seção com `##` no formato `## DD/MM/AAAA — Descrição curta do fato`.
- Separe cada seção com uma linha `---`.

### Template de seção

```markdown
## DD/MM/AAAA — Descrição curta

| Campo | Valor |
|---|---|
| **Data** | DD/MM/AAAA (quando o usuário contou) |
| **Fonte** | Contexto da interação (ex: "conversa sobre vaga Comolatti") |
| **Categoria** | Experiência / Conquista / Número / Ferramenta / Projeto / Preferência / Limitação / Disponibilidade / Formação |
| **Status** | Confirmada / Não confirmada / Estimativa |
| **Relacionada** | referência a `base/cv.md` ou outras seções de `historias.md` ou `vagas/` |

(narração do fato no tom do usuário)

**Uso potencial:** como esse fato pode aparecer no CV, auditoria ou perfil — só sugestão, sem inventar nada.
```

## Integração com outras skills

- **`cv-maker`**: consulte antes do Levantamento de Informações; registre respostas novas do usuário sobre gaps.
- **`cv-audit`**: consulte antes das Perguntas Estratégicas; registre números/resultados revelados durante a auditoria.
- Ao final de uma sessão em que houver registro novo, informe ao usuário o que foi arquivado.
