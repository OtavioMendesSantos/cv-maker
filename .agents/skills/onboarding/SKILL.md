---
name: onboarding
description: Cria a base inicial do currículo a partir de informações coladas pelo usuário, respostas guiadas ou um PDF exportado do LinkedIn. Use somente quando `base/cv.md` ainda não existe. Depois da criação, nunca altera arquivos em `base/`.
---

# Onboarding do currículo

Crie uma fonte de verdade inicial, verificável e protegida. Esta skill pode criar arquivos em `base/` uma única vez. Se `base/cv.md` já existir, leia-o e encerre o onboarding sem modificá-lo.

## Proteção da base

- Nunca sobrescreva, complete ou corrija um arquivo existente em `base/`.
- Faça todo o trabalho preparatório em `onboarding/{YYMMDDHHMM}/`.
- Antes da criação final, apresente os arquivos de proposta e as pendências factuais ao usuário.
- Só depois da aprovação explícita, crie os arquivos ausentes em `base/`.
- Mudanças futuras devem ser propostas em `propostas-base/{YYMMDDHHMM}/` para adoção manual pelo usuário.

## Formas de entrada

Aceite uma combinação destas fontes:

1. **Texto livre:** o usuário descreve sua trajetória ou cola um currículo, perfil, bio ou histórico profissional.
2. **Entrevista guiada:** pergunte apenas pelos campos que ainda faltam.
3. **PDF do LinkedIn:** leia o PDF exportado com `pdftotext`; preserve o arquivo original na proposta e, após aprovação, copie-o para `base/originais/` sem modificá-lo.

Consulte `historias.md` se existir, mas trate informações conflitantes como pendentes. Não assuma que o PDF do LinkedIn contém métricas, contexto técnico ou resultados suficientes.

## Informações mínimas

Reúna, quando aplicável:

- nome completo, cidade/estado e ao menos um contato;
- cargo ou área alvo;
- experiências com empresa, cargo, local e datas;
- responsabilidades, projetos, ferramentas, escala e resultados comprováveis;
- formação, certificações e idiomas;
- links profissionais úteis.

Omita campos que não se aplicam. Não invente conteúdo para completar o template.

## Proposta para revisão

1. Extraia e organize os fatos disponíveis.
2. Faça perguntas específicas somente sobre lacunas que alterem materialmente o currículo.
3. Preencha `template/cv.md` como `onboarding/{YYMMDDHHMM}/cv-base-proposta.md`.
4. Preencha `template/cv.tex` como `onboarding/{YYMMDDHHMM}/curriculo-base-proposta.tex`, removendo seções vazias.
5. Compile o PDF com `pdflatex` e confira o texto com `pdftotext`.
6. Entregue uma lista curta de fatos confirmados, pendências e possíveis conflitos.
7. Solicite aprovação para criar a base. A aprovação deve se referir a esses arquivos concretos.

## Criação única da base

Depois da aprovação, confirme novamente que os destinos não existem e crie:

- `base/cv.md`, a partir da proposta factual aprovada;
- `base/pt/{slug-nome}-curriculo-base.tex` e o PDF correspondente;
- `base/originais/{nome-do-arquivo}.pdf`, quando houver uma fonte original fornecida pelo usuário.

Se qualquer destino já existir, não o substitua. Informe o conflito e mantenha a proposta em `onboarding/`.

Ao concluir, informe que `base/` passa a ser somente leitura para as demais skills.
