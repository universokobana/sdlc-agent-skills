*[Read in English](README.md)*

> **Nota:** Este repositório é baseado no padrão [Agent Skills](http://agentskills.io) para o Claude. Contém skills de SDLC (Software Development Lifecycle) para automação de workflows de desenvolvimento.

# Skills

Skills são pastas com instruções, scripts e recursos que o Claude carrega dinamicamente para melhorar o desempenho em tarefas especializadas. Skills ensinam o Claude a completar tarefas específicas de forma repetível.

Para mais informações:
- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude)
- [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills)
- [Equipping agents for the real world with Agent Skills](https://anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

# Sobre Este Repositório

Este repositório contém skills de SDLC para automação de workflows de desenvolvimento de software com Claude — incluindo revisão de PRs, correção de CI e automação de qualidade de código.

## Skills Disponíveis

| Skill | Descrição |
|-------|-----------|
| [fix-github-pr](./skills/fix-github-pr) | Corrigir comentários de revisão de PR, sugestões do Copilot e falhas de CI |

## Aviso Legal

**Estas skills são fornecidas para fins de demonstração e educacionais.** Sempre teste as skills completamente em seu próprio ambiente antes de depender delas para tarefas críticas.

# Estrutura do Repositório

- [./skills](./skills): Skills de automação SDLC
- [./spec](./spec): Especificação do Agent Skills
- [./template](./template): Template de skill

# Use no Claude Code, Claude.ai e na API

## Claude Code

Você pode registrar este repositório como um marketplace de plugins do Claude Code executando o seguinte comando:
```
/plugin marketplace add universokobana/sdlc-agent-skills
```

Então, para instalar as skills:
1. Selecione `Browse and install plugins`
2. Selecione `sdlc-agent-skills`
3. Selecione `sdlc-agent-skills`
4. Selecione `Install now`

Alternativamente, instale diretamente via:
```
/plugin install sdlc-agent-skills@sdlc-agent-skills
```

Após instalar o plugin, você pode usar a skill apenas mencionando-a. Por exemplo:
- "Corrigir PR #42"
- "Corrigir os comentários de revisão do meu PR"
- "Corrigir falhas de CI neste PR"

## Claude.ai

Para usar qualquer skill deste repositório ou fazer upload de skills personalizadas, siga as instruções em [Using skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude#h_a4222fa77b).

## Claude API

Você pode usar skills pré-construídas e fazer upload de skills personalizadas via Claude API. Veja o [Skills API Quickstart](https://docs.claude.com/en/api/skills-guide#creating-a-skill) para mais informações.

# Criando uma Skill Básica

Skills são simples de criar - apenas uma pasta com um arquivo `SKILL.md` contendo frontmatter YAML e instruções. Você pode usar o **template** neste repositório como ponto de partida:

> **Importante:** Ao criar ou remover skills, você deve atualizar os seguintes arquivos:
> - `.claude-plugin/marketplace.json` - Registrar/desregistrar a skill no array `plugins[0].skills`
> - `README.md` e `README.pt-BR.md` - Atualizar a tabela "Skills Disponíveis"
> - `CLAUDE.md` - Atualizar as seções de estrutura do repositório e skills disponíveis

```markdown
---
name: minha-skill
description: Uma descrição clara do que esta skill faz e quando usá-la
---

# Nome da Minha Skill

[Adicione suas instruções aqui que o Claude seguirá quando esta skill estiver ativa]

## Exemplos
- Exemplo de uso 1
- Exemplo de uso 2

## Diretrizes
- Diretriz 1
- Diretriz 2
```

O frontmatter requer apenas dois campos:
- `name` - Um identificador único para sua skill (minúsculas, hífens para espaços)
- `description` - Uma descrição completa do que a skill faz e quando usá-la

O conteúdo markdown contém as instruções, exemplos e diretrizes que o Claude seguirá. Para mais detalhes, veja [How to create custom skills](https://support.claude.com/en/articles/12512198-creating-custom-skills).
