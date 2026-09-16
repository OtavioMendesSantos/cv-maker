---
name: cv-audit
description: Audita e reescreve o currículo base do usuário de forma crítica e independente de uma vaga específica. Use quando o usuário pedir para analisar, criticar, avaliar, auditar, diagnosticar ou reescrever o próprio currículo, identificar pontos fracos, gaps, aderência a cargos, ou melhorar a versão geral do CV (não para criar uma versão tailorada para uma vaga — isso é o cv-maker). Não use para vagas específicas.
---

# CV Audit Skill

## Quando usar esta Skill

Use quando o usuário quiser **melhorar o currículo base** (não o de uma vaga específica): pedir uma análise crítica, avaliação, auditoria, diagnóstico, nota, reescrita, ou parecer sincero sobre o perfil. Difere do `cv-maker`, que cria um currículo tailorado para uma vaga.

## Princípios Básicos

1. **Nunca minta:** Jamais invente informações, resultados, competências, cargos, datas, ferramentas, formações ou experiências. Sempre diferencie experiência comprovada de conhecimento básico ou acadêmico.
2. **Seja sincero, não gentil:** Seja criterioso e direto. Diga claramente quando algo prejudica o candidato ou quando o perfil não está qualificado para um cargo. O objetivo não é elogiar, é aumentar as chances reais de contratação.
3. **Fonte de verdade:** Trabalhe sobre o CV base do usuário (geralmente `base/cv.md` ou o `.tex` base em `base/`). Modifique esses arquivos-base quando reescrever — **não crie arquivos por vaga** (isso é do `cv-maker`).
4. **Escrita Natural (Humanizer):** Aplique sempre as regras da skill `humanizer`. Evite jargões de IA, clichês e voz passiva.
5. **Não invente na reescrita:** Antes de reescrever, pergunte sobre informações que podem valorizar o currículo (resultados, escalas, equipes). Aguarde respostas quando precisar.

## Fluxo de Execução

Siga rigorosamente as etapas abaixo.

### ETAPA 1 — Diagnóstico Crítico

Leia o CV base do usuário e apresente uma avaliação completa:

- **Nota geral** de 0 a 10.
- **Primeira impressão** causada no recrutador.
- **Pontos fortes reais.**
- **Pontos fracos** e problemas que podem gerar reprovação.
- **Informações importantes faltando.**
- **Trechos genéricos, vagos ou pouco confiáveis.**
- **Experiências mal explicadas ou subaproveitadas.**
- **Problemas de organização, clareza, português, datas ou formatação.**
- **Competências sem evidências práticas.**
- **Conteúdos que devem ser excluídos** (ex: CPF, RG, estado civil, foto, endereço completo).
- **Possíveis incoerências ou sinais de alerta.**
- **Aderência ao cargo/vaga pretendida.**
- **Compatibilidade com ATS** e palavras-chave ausentes.

Não suavize problemas importantes; diga claramente o que está prejudicando o currículo.

### ETAPA 2 — Perguntas Estratégicas

Antes de reescrever, pergunte tudo o que for necessário para valorizar o currículo, com perguntas **específicas para cada experiência** (evite perguntas genéricas):

- Tamanho das equipes lideradas.
- Metas e resultados alcançados.
- Crescimento de vendas ou produtividade.
- Redução de custos, erros ou prazos.
- Volume de atendimentos, projetos, clientes ou processos.
- Sistemas, ferramentas e tecnologias utilizadas.
- Principais responsabilidades.
- Promoções ou evolução de carreira.
- Projetos relevantes.
- Indicadores acompanhados.
- Nível real de conhecimento em cada competência.
- Motivo de experiências muito curtas.
- Disponibilidade para viagens ou mudança.
- Cursos em andamento.
- Idiomas e nível verdadeiro de domínio.
- Diferenciais que não aparecem no currículo.

**Base de fatos (`historias.md`):** Antes de perguntar, consulte `historias.md` (ver skill `historias`) para recuperar números, conquistas e experiências já relatados em interações anteriores; não repita perguntas já respondidas. Ao longo da auditoria, registre em `historias.md` toda informação nova revelada pelo usuário, marcando o que ainda precisa ser confirmado.

Se a pessoa não souber números exatos, ajude a estimar resultados de forma responsável, deixando claro que nada pode ser inventado. **Aguarde as respostas antes de produzir a versão final.**

### ETAPA 3 — Reescrita Completa

Após receber as respostas, reescreva o CV base completo, contendo quando aplicável:

- Nome completo.
- Cidade e estado.
- Telefone, e-mail e LinkedIn.
- Título profissional alinhado ao objetivo.
- Resumo profissional estratégico.
- Competências técnicas.
- Experiências profissionais em ordem cronológica inversa.
- Principais atividades e entregas de cada experiência.
- Resultados mensuráveis e conquistas comprováveis.
- Formação acadêmica.
- Cursos e certificações relevantes.
- Idiomas.
- Informações complementares relevantes.

#### Regras para a reescrita

- Use linguagem profissional, clara, humana e convincente.
- Não use clichês como "proativo", "dinâmico", "perfeccionista", "trabalho bem em equipe" ou "em busca de novos desafios" sem evidências.
- Não escreva em primeira pessoa.
- Não transforme o resumo profissional em lista de adjetivos.
- Comece as atividades com verbos fortes e variados.
- Destaque responsabilidades, contexto, complexidade, autonomia e resultados.
- Dê prioridade ao que for relevante para a vaga/cargo pretendido.
- Reduza ou elimine informações antigas e pouco relacionadas ao objetivo atual.
- Não inclua CPF, RG, estado civil, número de filhos, foto ou endereço completo.
- Não use tabelas, colunas, gráficos, barras de nível, ícones ou elementos que prejudiquem a leitura pelo ATS.
- Use palavras-chave naturalmente, sem copiar descrições de forma artificial.
- Organize para que o mais importante seja percebido rapidamente.
- Busque manter entre uma e duas páginas (exceto quando a trajetória justificar mais).
- Não exagere a senioridade nem esconda lacunas; apresente a melhor forma ética de tratá-las.

#### Diretório de saída

- Crie o diretório `auditorias/` na raiz do projeto (se não existir).
- Para cada auditoria, crie uma subpasta única com carimbo de data e hora no momento da criação, no formato `auditorias/{YYMMDDHHMM}/` (ex: `auditorias/2609161205/`).
- Salve o resultado da auditoria dentro dessa subpasta, usando o mesmo carimbo na nomenclatura:
  `{slug-nome}-auditoria-CV-{YYMMDDHHMM}.md` (ex: `auditorias/2609161205/otavio-auditoria-CV-2609161205.md`).
- Use o mesmo carimbo `{YYMMDDHHMM}` também nos arquivos auxiliares (`.tex`, `.pdf`), mantendo tudo na mesma subpasta.
- **Não modifique os arquivos-base** (`base/cv.md`, `.tex` base) nem crie arquivos em `vagas/` (isso é do `cv-maker`).
- Se for feita uma reescrita em LaTeX, salve também nessa subpasta e recompile com `pdflatex`, revisando os logs em busca de avisos graves ou erros.

### ETAPA 4 — Parecer Final

Entregue ao usuário:

1. **Currículo reescrito** — versão completa.
2. **Principais melhorias realizadas** — o que foi corrigido e por que a nova versão é mais forte.
3. **Pontos que ainda precisam ser comprovados** — o que validar/detalhar numa entrevista.
4. **Orientações para personalização** — quais partes adaptar para cada vaga.
5. **Nota final** — nova nota de 0 a 10, comparada com a nota original.
6. **Parecer sincero:**
   - Este currículo tem força para gerar entrevistas?
   - Para quais cargos o perfil está realmente preparado?
   - Para quais ainda não está preparado?
   - Qual é o maior diferencial do candidato?
   - Qual é a principal fragilidade?
   - O que ainda precisa melhorar para competir com os melhores?
   - Se o perfil não for qualificado para o cargo desejado, diga claramente e recomende cargos mais compatíveis.
