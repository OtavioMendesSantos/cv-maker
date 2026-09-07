# CV Maker

Um sistema para gerenciar e gerar currículos em LaTeX usando o opencode. O repositório funciona como um template: você insere seus dados e a IA gera versões específicas para cada vaga.

## Como funciona

A configuração fica na pasta `.agents/`, que contém as skills (como a `cv-maker` e a `humanizer`) e as regras do workspace (`rules/curriculos.md`).

Quando você fornece a descrição de uma vaga para a skill `cv-maker`, a IA:

1. Compara a vaga com o seu currículo base e calcula a compatibilidade (_Match Score_).
2. Cria um arquivo `.tex` adaptado para a vaga, utilizando apenas suas experiências reais.
3. Compila o PDF usando `pdflatex`.
4. Atualiza o arquivo `overview.md` com o histórico de candidaturas.

## Estrutura do projeto

- `.agents/`: Regras e skills que o opencode utiliza. Este diretório deve ser versionado.
- `base/`: (Ignorado pelo Git). Coloque seus dados aqui.
  - `cv.md`: Suas experiências e habilidades. A primeira linha (`# Seu Nome`) define a identidade usada nos currículos e nos nomes de arquivo.
  - `pt/` e `en/`: Modelos em LaTeX (`.tex`) para a formatação visual.
- `vagas/`: (Ignorado pelo Git). Diretório onde a IA salva os currículos gerados.
- `overview.md`: (Ignorado pelo Git). Histórico gerado pela IA.
- `opencode.example.json`: Modelo de configuração do opencode. Copie para `opencode.json` e preencha seus dados.

## Configuração

1. Clone o repositório e crie a pasta `base/` com o arquivo `cv.md` (começando por `# Seu Nome`) e seus modelos `.tex`.
2. Copie `opencode.example.json` para `opencode.json` e configure seu provedor de IA e, se quiser, o servidor MCP do Hirely com a sua API key. O `opencode.json` é ignorado pelo Git (não versionar chaves).
3. Mantenha a pasta `.agents/` no repositório.
4. Execute o opencode, acione a skill `cv-maker` e cole a descrição da vaga.

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