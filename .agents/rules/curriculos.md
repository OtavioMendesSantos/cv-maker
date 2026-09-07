# Regras do Workspace: Gestão de Currículos

Este workspace é dedicado à criação, otimização e gestão dos currículos do usuário. Sempre que atuar neste diretório, siga rigorosamente as instruções abaixo:

## Identidade do Usuário (Configuração)

1. O nome e os dados de contato do usuário estão definidos em `base/cv.md` (nome na primeira linha, ex: `# Otávio Mendes Santos`, seguido de contato, experiências, etc.). Ele é a fonte de verdade.
2. **NUNCA hardcode ou assuma o nome do usuário** em conteúdo, nomes de arquivo ou seções. SEMPRE leia o cabeçalho `# <Nome>` de `base/cv.md` para obtê-lo.
3. Para nomenclatura de arquivos, gere um slug a partir do nome: primeiro nome em minúsculas e sem acentos (ex: `Otávio` → `otavio`). Use-o no padrão `{slug-nome}-<titulo-curto>-YYMMDD.tex`.

## Diretrizes Gerais

1. **Fluxo de Geração (Skill):** Para qualquer solicitação de adequação de currículo a uma vaga específica, **SEMPRE** utilize a skill `cv-maker` (localizada em `.agents/skills/cv-maker/SKILL.md`). Siga o passo a passo da skill fielmente.
2. **Formato Exclusivo (LaTeX):** O formato oficial de saída e "fonte de verdade" para aplicações é o LaTeX (`.tex`). Não entregue currículos adaptados em `.md` ou texto plano para o usuário.
3. **Compilação Obrigatória:** Sempre que você criar ou editar um arquivo `.tex`, é sua obrigação acionar o terminal e executar o comando `pdflatex <nome-do-arquivo>.tex` dentro do diretório correspondente para gerar o PDF atualizado de forma proativa.
4. **Base de Referência:**
   - Utilize o currículo `.tex` base que estiver em `base/pt/` (o modelo mais recente) como referência para estrutura visual e pacotes LaTeX.
   - Utilize o `cv.md` ou o próprio `.tex` base para extrair a verdade sobre as experiências do usuário.
5. **Rastreabilidade:** Todas as aplicações e novos currículos gerados devem ser obrigatoriamente registrados no arquivo `overview.md` seguindo o formato da tabela existente.
6. **Polícia da Verdade:** Jamais invente experiências ou assuma conhecimento em tecnologias que o usuário não possui. Na ausência de um requisito de vaga, faça perguntas claras ao usuário antes de redigir o documento.
7. **Proteção da Base (`base/`):** NUNCA edite, altere ou modifique nenhum arquivo dentro de `./base` (como `cv.md` ou `.tex` base), a menos que o usuário solicite expressamente (ex: correção de escrita, nova experiência). Currículos adaptados a vagas específicas devem ser criados em novas pastas em `vagas/`, nunca sobrescrevendo a base.
