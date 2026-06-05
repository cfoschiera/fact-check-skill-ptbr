# fact-check-skill (PT-BR)

Pipeline semi-automatizado de verificação de fatos adaptado para o contexto brasileiro de desinformação e para o português do Brasil.

Skill para uso com [Claude Code](https://claude.ai/code).

## O que faz

Verifica afirmações e conteúdo suspeito em 4 modos:

| Modo | Uso |
|---|---|
| **Padrão** | Pipeline completo de 11 etapas com pontuação MFS |
| **Comparação** | Duas fontes sobre o mesmo assunto, lado a lado |
| **Prebunking** | Preparação contra narrativa falsa esperada |
| **Rápido** | Pergunta sim/não — apenas etapas essenciais |

Retorna: veredicto estruturado, pontuação MFS (Manipulation & Falsehood Score) e orientações para verificação independente.

## Adaptações para PT-BR

- **Hierarquia de fontes brasileira** — verificadores IFCN (Aos Fatos, Agência Lupa, AFP Checamos, Comprova), órgãos governamentais (TSE, STF, ANVISA, IBGE), veículos de referência
- **Narrativas mapeadas** — urnas eletrônicas, negacionismo científico, deepfakes de políticos, desinformação financeira, conteúdo reciclado
- **Vetores específicos** — WhatsApp grupos, Telegram, YouTube (pseudodocumentários)
- **Terminologia e veredictos** inteiramente em português brasileiro

## Instalação

```bash
mkdir -p ~/.claude/skills/fact-check
curl -o ~/.claude/skills/fact-check/SKILL.md \
  https://raw.githubusercontent.com/[seu-usuario]/fact-check-skill-ptbr/main/SKILL.md
```

Ou manualmente: baixe `SKILL.md` e coloque em `~/.claude/skills/fact-check/SKILL.md`.

## Uso

Gatilhos no chat com Claude Code:

```
verifica isso
checa essa informação
é verdade que [afirmação]
prebunking sobre [tema]
compara essas duas fontes
```

## Atribuição

Adaptado de [fact-check-skill](https://github.com/petar-nauka/fact-check-skill) por [@petar-nauka](https://github.com/petar-nauka).

Metodologias base: [SIFT](https://cor.inquirygroup.org/curriculum/sift), [CRAAP Test](https://library.csuchico.edu/help/source-or-information-good), [Stanford Lateral Reading Protocol](https://stacks.stanford.edu/file/druid:fv751yt5934/SHEG%20Evaluating%20Information%20Online.pdf).

## Licença

MIT — veja [LICENSE](LICENSE).
