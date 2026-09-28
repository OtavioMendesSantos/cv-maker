# CV Maker

Um sistema para criar, revisar e adaptar currículos em LaTeX usando um agente de código. O repositório inclui um modelo inicial: quem ainda não tem currículo pode fornecer suas informações e gerar a base antes de criar versões para vagas.

## Como funciona

A configuração fica na pasta `.agents/`, que contém as skills (como a `cv-maker` e a `humanizer`) e as regras do workspace (`rules/curriculos.md`).

No primeiro uso, a skill `onboarding` prepara uma proposta a partir de texto livre, perguntas guiadas ou um PDF exportado do LinkedIn. Depois da aprovação do usuário, ela cria `base/cv.md` e o currículo LaTeX. A partir daí, `base/` é somente leitura para as skills.

Quando você fornece a descrição de uma vaga para a skill `cv-maker`, o agente:

1. Compara a vaga com o seu currículo base e calcula a compatibilidade (_Match Score_).
2. Cria um arquivo `.tex` adaptado para a vaga, utilizando apenas suas experiências reais.
3. Compila o PDF usando `pdflatex`.
4. Atualiza o arquivo `overview.md` com o histórico de candidaturas.

## Estrutura do projeto

- `.agents/`: Regras e skills que o opencode utiliza. Este diretório deve ser versionado.
- `template/`: Modelos versionados usados apenas quando o usuário ainda não tem uma base própria.
  - `cv.md`: Estrutura dos dados e fatos do currículo.
  - `cv.tex`: Layout LaTeX de uma coluna, sem tabelas ou elementos gráficos.
- `base/`: (Ignorado pelo Git). Coloque seus dados aqui.
  - `cv.md`: Suas experiências e habilidades. A primeira linha (`# Seu Nome`) define a identidade usada nos currículos e nos nomes de arquivo.
  - `pt/` e `en/`: Modelos em LaTeX (`.tex`) para a formatação visual.
- `vagas/`: (Ignorado pelo Git). Diretório onde a IA salva os currículos gerados.
- `onboarding/`: Propostas temporárias produzidas antes da criação inicial de `base/`.
- `propostas-base/`: Sugestões posteriores de atualização que o usuário pode adotar manualmente.
- `overview.md`: (Ignorado pelo Git). Histórico gerado pela IA.
- `opencode.example.json`: Modelo de configuração do opencode. Copie para `opencode.json` e preencha seus dados.

## Configuração

1. Clone o repositório.
2. Copie `opencode.example.json` para `opencode.json` e configure seu provedor de IA e, se quiser, o servidor MCP do Hirely com a sua API key. O `opencode.json` é ignorado pelo Git (não versionar chaves).
3. Se já tiver currículo, coloque o conteúdo em `base/cv.md` e o modelo visual em `base/pt/`. Se não tiver, acione `onboarding` e descreva sua trajetória, cole o conteúdo existente ou forneça o PDF exportado do LinkedIn.
4. Para uma vaga específica, acione `cv-maker` e forneça a descrição ou o link da vaga.

### O papel dos dois templates

`template/cv.md` organiza a fonte de verdade: experiências, datas, resultados, formação e competências. `template/cv.tex` controla apenas a apresentação do PDF. Essa separação permite trocar o visual sem perder os fatos e evita extrair experiências de um arquivo de layout.

O LaTeX padrão prioriza leitura humana e parsing por ATS: uma coluna, títulos convencionais, nenhum ícone, nenhuma foto e nenhum bloco em tabela. Se o usuário já tiver um modelo próprio, ele continua sendo a primeira opção.

### Fontes de verdade

`base/cv.md` é a fonte factual principal. Os arquivos de `base/pt/` definem a apresentação base e `base/originais/` preserva documentos fornecidos pelo usuário. Depois do onboarding, as skills só podem ler esses arquivos. Auditorias e sugestões são geradas fora de `base/` e nunca substituem a fonte de verdade automaticamente.

### Identidade do usuário

As regras e a skill `cv-maker` **nunca assumem ou "hardcodeam" o seu nome**: ele é extraído automaticamente do cabeçalho `# <Nome>` de `base/cv.md`. Para nomes de arquivos é usado um slug do primeiro nome (ex: `Otávio` → `otavio-engenheiro-de-software-260903.tex`).

## Compilação manual

Se precisar compilar um arquivo gerado sem o uso da IA, execute no terminal:

```bash
pdflatex nome-do-arquivo.tex
```

## Conexão com MCP (Hirely)

O servidor MCP do Hirely é configurado **por projeto** no `opencode.json`, seguindo o modelo `opencode.example.json`. Preencha o campo `Authorization` com a sua API key:

```bash
cp opencode.example.json opencode.json
# edite opencode.json e substitua <SUA_API_KEY_AQUI> pela sua chave
```
