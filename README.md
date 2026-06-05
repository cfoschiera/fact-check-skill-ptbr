# fact-check-skill (PT-BR)

Pipeline semi-automatizado de verificação de fatos adaptado para o contexto brasileiro de desinformação e para o português do Brasil.

Skill para uso com [Claude Code](https://claude.ai/code) e [OpenCode](https://opencode.ai/).

## O que faz

Verifica afirmações e conteúdo suspeito em 4 modos:

| Modo | Uso |
|---|---|
| **Padrão** | Pipeline completo de 11 etapas com pontuação MFS |
| **Comparação** | Duas fontes sobre o mesmo assunto, lado a lado |
| **Prebunking** | Preparação contra narrativa falsa esperada |
| **Rápido** | Pergunta sim/não — apenas etapas essenciais |

Retorna: veredicto estruturado, pontuação MFS (Manipulation & Falsehood Score) e orientações para verificação independente.

**Formato de saída:** Markdown estruturado. O original ([fact-check-skill](https://github.com/petar-nauka/fact-check-skill)) gera HTML cards — escolha intencional desta adaptação para compatibilidade com fluxos baseados em texto.

**Modo offline:** quando sem acesso a ferramentas web, a skill declara a limitação explicitamente, reduz a confiança do veredicto um nível e orienta para verificação manual com as fontes do `SOURCES.md`.

## Adaptações para PT-BR

- **Hierarquia de fontes brasileira** — verificadores IFCN (Aos Fatos, Agência Lupa, AFP Checamos, Comprova), órgãos governamentais (TSE, STF, ANVISA, IBGE), veículos de referência
- **40+ marcadores de red flags** contextualizados para o Brasil: linguagem de WhatsApp, prints sem contexto, deepfakes de políticos, kit covid, uso indevido de VAERS/Notivisa/OpenDataSUS
- **Narrativas mapeadas** — urnas eletrônicas, negacionismo científico, deepfakes, desinformação financeira, conteúdo reciclado de outro país/época
- **Vetores específicos** — WhatsApp grupos, Telegram, YouTube (pseudodocumentários)
- **Terminologia e veredictos** inteiramente em português brasileiro
- **SOURCES.md** — diretório de fontes brasileiras com links por tier

## Instalação

**Via gh CLI** (requer [GitHub CLI](https://cli.github.com/) 2.90.0+):

```bash
gh skill install [usuario]/fact-check-skill-ptbr fact-check
```

**Manual:**

```bash
mkdir -p ~/.claude/skills/fact-check
curl -o ~/.claude/skills/fact-check/SKILL.md \
  https://raw.githubusercontent.com/[usuario]/fact-check-skill-ptbr/main/SKILL.md
```

## Uso

Gatilhos no chat com Claude Code:

```
verifica isso
checa essa informação
é verdade que [afirmação]
prebunking sobre [tema]
compara essas duas fontes
```

## Fontes de referência

O arquivo [`SOURCES.md`](SOURCES.md) contém o diretório completo de fontes por tier com links, além de ferramentas de verificação (busca reversa de imagens, Wayback Machine, análise de vídeos, etc.).

## Atribuição

Adaptado de [fact-check-skill](https://github.com/petar-nauka/fact-check-skill) por [@petar-nauka](https://github.com/petar-nauka).

Metodologias base: [SIFT](https://cor.inquirygroup.org/curriculum/sift), [CRAAP Test](https://library.csuchico.edu/help/source-or-information-good), [Stanford Lateral Reading Protocol](https://stacks.stanford.edu/file/druid:fv751yt5934/SHEG%20Evaluating%20Information%20Online.pdf).

## Histórico de versões

- **v1.0.0** — Lançamento inicial. Adaptação PT-BR com hierarquia de fontes brasileira, 40+ red flags contextualizados, narrativas e vetores específicos do Brasil, saída em Markdown, SOURCES.md com fontes e ferramentas.

## Licença

MIT — veja [LICENSE](LICENSE).
