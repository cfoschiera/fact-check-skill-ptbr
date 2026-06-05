# AGENTS.md

Orientações para agentes de IA (Claude Code, Codex, Warp, etc.) trabalhando neste repositório.

## O que este repo é

Uma skill para Claude Code / OpenCode implementada inteiramente em Markdown. O artefato de runtime é `SKILL.md`: o agente lê o frontmatter YAML (metadados) seguido das instruções da skill. Sem build, sem código a executar.

## Arquivos principais

- `SKILL.md` — a skill. Frontmatter YAML (`name`, `version`, `description`, `license`) seguido do pipeline de 11 etapas. **Esta é a fonte de verdade.**
- `README.md` — para humanos: instalação, uso, descrição das adaptações PT-BR, histórico de versões.
- `SOURCES.md` — diretório de fontes brasileiras por tier de confiabilidade, com links. Referenciado dentro do SKILL.md.

## Contrato de manutenção

`SKILL.md`, `README.md` e `SOURCES.md` devem permanecer sincronizados.

- **Hierarquia de fontes:** se atualizar a tabela de tiers no SKILL.md, atualizar também o SOURCES.md com os links correspondentes.
- **Red flags:** a Etapa 5 lista 40+ marcadores em 6 categorias. Se adicionar sinais ou categorias, manter a estrutura de seções bold por categoria.
- **Versão:** o campo `version:` no frontmatter do SKILL.md e a seção "Histórico de versões" no README devem ser atualizados juntos.
- **Contexto brasileiro:** este repo é uma adaptação focada no Brasil. Novas adições devem priorizar relevância para o cenário de desinformação brasileiro.

## Editar SKILL.md

- Preservar YAML frontmatter válido (formatação e indentação).
- O prompt abaixo do frontmatter é o produto. Editar como documento de instrução cuidadoso, não como código.
- Não restaurar referências a caminhos de vault pessoal (ex: `99 - Sistema do Cofre/`, `00 - Entrada/`) — este é um repositório público genérico.
