---
name: cv-audit
description: Audita e propõe uma reescrita do currículo base sem depender de uma vaga específica e sem modificar `base/`. Use para diagnosticar o CV e melhorar sua versão geral. Se `base/cv.md` não existir, use `onboarding`; para uma vaga concreta, use `cv-maker`.
---

# CV Audit

Produza um currículo base factual, claro e reutilizável. A auditoria deve separar problemas de conteúdo, estrutura e apresentação. Não use uma vaga específica como referência; use o cargo alvo informado pelo usuário.

## Regras essenciais

- Nunca invente cargo, data, ferramenta, formação, responsabilidade, resultado ou métrica.
- Consulte `historias.md`, quando existir, antes de perguntar. Registre fatos novos conforme a skill `historias`.
- Aplique a skill `humanizer` ao texto do currículo.
- Trate `base/cv.md` como fonte factual principal. Use `historias.md` como complemento. Quando houver conflito, mostre o conflito e confirme com o usuário.
- Não transforme conhecimento acadêmico ou estudo pessoal em experiência profissional.
- Não avalie senioridade apenas por tempo de carreira. Considere autonomia, escopo, complexidade e resultados comprovados.
- Não prometa compatibilidade total com ATS. Valide estrutura, texto extraível e riscos conhecidos de parsing.

## Pré-condição

`base/cv.md` precisa existir. Se estiver ausente, use a skill `onboarding` e só inicie a auditoria depois que o usuário aprovar e criar a base inicial.

Durante a auditoria, trate todo o diretório `base/` como somente leitura. Salve qualquer reescrita em `auditorias/` para comparação.

## 1. Diagnóstico

Leia o documento inteiro e apresente:

- nota geral de 0 a 10, com justificativa;
- primeira impressão em uma leitura rápida;
- pontos fortes sustentados por fatos;
- problemas que podem causar descarte;
- informações ausentes, contraditórias ou difíceis de defender;
- experiências subaproveitadas e competências sem evidência;
- clareza, ordem das seções, cronologia, português e consistência;
- adequação ao cargo alvo e termos relevantes que faltam;
- riscos de parsing ATS, incluindo colunas, tabelas, caixas de texto, cabeçalho/rodapé, imagens, ícones e PDF sem texto extraível;
- conteúdo que deve sair, como foto, documentos, estado civil e endereço completo.

Não confunda aparência com qualidade do conteúdo. Um layout limpo não compensa bullets vagos, e um bom histórico pode perder força em um documento difícil de ler.

## 2. Perguntas de alto impacto

Antes da reescrita, faça perguntas específicas para cada experiência. Pergunte somente quando a resposta puder mudar o currículo. Exemplos:

- Qual era o produto, problema e responsabilidade direta?
- Qual era a escala: usuários, pedidos, receita, equipe, projetos ou volume processado?
- O que melhorou e como foi medido?
- Quais ferramentas foram usadas de fato naquele contexto?
- Houve promoção, liderança, decisão técnica ou contato com clientes?
- Como explicar sobreposições, lacunas ou passagens curtas?
- Qual é o nível real do idioma e em que contexto ele foi usado?

Ajude o usuário a localizar uma medida verificável, mas não converta uma estimativa em fato. Marque estimativas e pontos ainda não confirmados. Aguarde respostas que sejam necessárias para a versão final.

## 3. Reescrita

Crie uma proposta completa com, quando aplicável: cabeçalho e contatos, título profissional, resumo, experiência em ordem cronológica inversa, projetos, formação, competências, certificações e idiomas.

- Use uma coluna, seções convencionais e ordem ajustada ao momento de carreira.
- Omita seções sem conteúdo. Liderança, projetos e certificações não são obrigatórios.
- Use bullets curtos com ação, contexto e resultado comprovável. Evite rótulos repetitivos dentro de cada bullet.
- Use presente para atividades atuais e passado para experiências encerradas, sem pronomes pessoais.
- Mantenha entre uma e duas páginas, salvo trajetória que justifique mais.
- Use palavras-chave de modo natural. Não repita listas para simular aderência.
- Preserve lacunas e limites reais da experiência; explique-os com clareza quando necessário.

## 4. Artefatos da auditoria

Crie `auditorias/{YYMMDDHHMM}/` e use o mesmo carimbo em todos os nomes:

- `{slug-nome}-auditoria-CV-{YYMMDDHHMM}.md`: diagnóstico, perguntas respondidas, mudanças, pendências e parecer;
- `{slug-nome}-auditoria-CV-{YYMMDDHHMM}.tex`: proposta de currículo;
- `{slug-nome}-auditoria-CV-{YYMMDDHHMM}.pdf`: compilação da proposta.

Use como base visual, nesta ordem: o LaTeX existente em `base/pt/`, um template fornecido pelo usuário ou `template/cv.tex`. Se houver uma razão técnica ou editorial para escolher outra opção, registre a justificativa. Não crie arquivos em `vagas/` e não substitua `base/` durante a auditoria.

O arquivo Markdown da auditoria deve conter uma seção obrigatória chamada `Template utilizado`, informando:

- caminho ou origem exata do template;
- posição dele na ordem de preferência acima;
- motivo da escolha e de qualquer desvio da ordem padrão;
- se foi usado sem alterações ou adaptado;
- alterações visuais ou técnicas relevantes feitas na cópia da auditoria;
- atribuição e licença, quando o template vier de uma fonte externa.

Compile com `pdflatex`. Corrija erros, texto cortado e avisos `Overfull \\hbox` relevantes. Extraia o texto do PDF e confirme que nome, contatos, seções, empresas, cargos e datas aparecem em ordem compreensível.

## 5. Entrega

Informe:

1. nota anterior e nota da proposta;
2. principais correções e por que melhoram o documento;
3. afirmações que ainda precisam ser comprovadas;
4. cargos que o histórico sustenta e cargos que ainda não sustenta;
5. maior diferencial e principal fragilidade;
6. arquivos gerados e quais arquivos o usuário pode adotar manualmente como nova base.

Nunca aplique a proposta diretamente em `base/`, mesmo quando o usuário pedir uma atualização. Copie a versão aprovada para `propostas-base/{YYMMDDHHMM}/` e deixe a adoção final para o usuário.
