---
name: cv-maker
description: Analisa descrições de vagas, checa compatibilidade ATS e cria currículos LaTeX personalizados sem inventar experiências.
---

# CV Maker Skill

## Quando usar esta Skill

Sempre que o usuário fornecer a descrição de uma vaga (ou um link) e solicitar a criação de um currículo específico para ela, ou pedir para aplicar para a vaga.

## Princípios Básicos

1. **Nunca minta:** Jamais invente experiências ou habilidades que o usuário não possui. Baseie-se estritamente no CV base. O objetivo é reenquadrar, destacar e ajustar as palavras das experiências reais para dar *match* com a vaga.
2. **LaTeX como Fonte de Verdade:** Não gere arquivos `.md` para currículos específicos. O novo currículo deve ser exclusivamente um arquivo `.tex`, que será a fonte de verdade para aquela vaga.
3. **Escrita Natural (Humanizer):** Aplique sempre as regras da skill `humanizer`. Evite jargões de IA (ex: "impulsionou", "fomentou", "mergulhou"), voz passiva e afirmações exageradas. O texto deve ser direto, profissional e factual.
4. **Tire Dúvidas:** Caso a vaga exija uma habilidade que não está no CV base, **PARE E PERGUNTE** ao usuário se ele possui aquela experiência e como a utilizou, antes de prosseguir com a criação do documento.

## Fluxo de Execução

Siga este passo a passo rigorosamente:

### 1. Análise ATS e da Vaga
- Leia o currículo base do usuário (geralmente `base/cv.md` ou o `.tex` base na pasta `base/`).
- **Extraia o nome do usuário** do cabeçalho `# <Nome>` de `base/cv.md` e use-o em conteúdos e nomes de arquivos. Nunca assuma ou hardcode o nome.
- Leia a descrição da vaga.
- Faça a análise de compatibilidade (Match Score) comparando as palavras-chave.
- Se o Match Score for **>= 80%**, avise o usuário que o CV base já atende bem à vaga e pergunte se ele ainda deseja gerar uma versão específica.
- Se o Match Score for **< 80%**, prossiga para o próximo passo.

### 2. Levantamento de Informações e Dúvidas
- Identifique os "Gaps": quais palavras-chave obrigatórias a vaga pede que o CV não tem?
- Pergunte ao usuário sobre os Gaps encontrados para confirmar se ele tem a experiência ou se devemos focar apenas nos pontos fortes existentes. (Aguarde a resposta se necessário).

### 3. Criação de Arquivos e Diretórios
- Crie uma nova pasta para a vaga: `vagas/{YYMMDD}-{EMPRESA}/` (Ex: `vagas/260907-software/`). Use a data em que o currículo é criado para `YYMMDD`.
- Crie o arquivo `.tex` dentro dessa nova pasta.
- **Nomenclatura obrigatória:** `{slug-nome}-<titulo-curto>-YYMMDD.tex`, onde `{slug-nome}` é o primeiro nome do usuário extraído de `base/cv.md`, em minúsculas e sem acentos (Ex: `Otávio` → `otavio-engenheiro-de-software-260903.tex`).

### 4. Geração do Conteúdo
- Reescreva o "Resumo Profissional" focando nos problemas que a vaga quer resolver.
- **Ordem cronológica das experiências:** Na seção "Experiências Profissionais", as experiências devem SEMPRE seguir ordem cronológica da mais recente para a mais antiga (período de maior data para menor data), independentemente da aderência à vaga.
- Reordene os tópicos dentro de cada experiência para que as conquistas mais aderentes à vaga fiquem no topo de cada lista.
- Utilize os mesmos pacotes e estrutura visual do `.tex` base do usuário.

### 5. Compilação
- Após criar o `.tex`, execute proativamente o comando `pdflatex <nome-do-arquivo>.tex` no diretório da vaga para gerar o PDF.

### 6. Revisão de Qualidade e Formatação
- Analise os logs do compilador `pdflatex` em busca de warnings graves (ex: `Overfull \hbox` que corte o texto) ou erros de sintaxe.
- Leia e revise mentalmente o conteúdo gerado em busca de trechos mal formulados ou que pareçam artificiais.
- Corrija o arquivo `.tex` caso haja erros, e recompile se necessário.

### 7. Validação Final ATS
- Com o currículo finalizado, realize uma última verificação cruzando o documento recém-criado com a descrição da vaga original.
- Calcule e informe ao usuário o novo Match Score (que deve ser alto).
- Se algum ponto importante tiver ficado de fora por falta de experiência prévia, apenas avise o usuário para alinhamento de expectativas.

### 8. Atualização do Overview
- Edite o arquivo `overview.md`.
- Se o arquivo estiver vazio, crie a estrutura de cabeçalho e a tabela.
- Insira uma nova linha preenchendo: Data, Vaga, Empresa, Arquivo, PDF, Tags (máximo de 2 a 3 tags que façam sentido para a vaga, reaproveitando termos como Backend, Fullstack, Node.js, Go) e Match (por último).

### 9. Cadastro no Hirely
- Quando o usuário pedir para adicionar a vaga no Hirely (ou logar à aplicação), registre a candidatura usando a ferramenta `hirely-backend_insert_application`.
- **Extraia e mapeie cada campo do input do usuário sempre que possível**, em vez de pedir dados que ele já forneceu:
  - `company` e `role` → obrigatórios; retire do nome da vaga/empresa informados.
  - `url` → o link da vaga fornecido.
  - `location` → cidade, remoto, híbrido etc., citados no texto da vaga.
  - `contractType` → CLT, PJ, INTERNSHIP ou OTHER, se mencionado (Home Office não é tipo de contrato; use OTHER quando não houver regime explícito).
  - `salaryRange` → faixa salarial, se informada.
  - `appliedAt` → data de hoje em RFC3339, ex: `2026-09-08T00:00:00Z`.
  - `status` → use o padrão `TO_APPLY`, a menos que o usuário indique outro.
  - `tagIds` → se já existirem tags no `hirely-backend_list_tags` que se encaixem na vaga, use-as.
- **Descrição (`description`):** envie de forma "mais crua", ou seja, reproduza o texto da vaga o mais próximo possível do original (atividades, requisitos, diferenciais), sem reescrever nem resumir. Só faça correções quando algo estiver claramente errado (ex: texto quebrado, HTML, campos invertidos).
- **Notas (`notes`):** use este campo para observações que não fazem parte da descrição crua — por exemplo, análise ATS, gaps de experiência, pontos de atenção, diferenças entre o CV e a vaga, ou avisos de alinhamento de expectativas.
- Após inserir, informe ao usuário o que foi registrado (empresa, vaga, status) e o ID da candidatura criado.

## Estrutura Padrão do `overview.md`

```markdown
# Controle de Aplicações e Currículos

| Data | Vaga | Empresa | Arquivo (.tex) | PDF | Tags | Match |
|---|---|---|---|---|---|---|
| DD/MM/AAAA | Desenvolvedor Backend | Empresa Exemplo | [{slug-nome}-backend-260903.tex](./vagas/260903-empresa-exemplo/{slug-nome}-backend-260903.tex) | [PDF](./vagas/260903-empresa-exemplo/{slug-nome}-backend-260903.pdf) | Backend, Node.js | 65% |
```
