---
name: fact-check
version: 1.0.0
description: Pipeline semi-automatizado de verificação de fatos com contexto brasileiro. Use quando o usuário pedir para verificar, checar, validar informação ou analisar conteúdo suspeito. Quatro modos - padrão (11 etapas), comparação, prebunking e rápido.
license: MIT
---

# Fact-check

Pipeline de verificação de fatos combinando metodologias SIFT, CRAAP e ciência de prebunking, adaptado para o contexto brasileiro de desinformação.

> Adaptado de [fact-check-skill](https://github.com/petar-nauka/fact-check-skill) por [@petar-nauka](https://github.com/petar-nauka) — versão PT-BR com contexto brasileiro.

## Quando invocar

- "verifica isso", "checa essa informação", "é verdade que..."
- "valida esse conteúdo", "analisa essa notícia", "essa informação é confiável?"
- Conteúdo suspeito a ser validado antes de uso
- "prebunking", "quero me preparar para desinformação sobre X"
- "compara essas duas fontes", "qual dessas versões é mais confiável?"

## Modos de operação

| Modo | Quando usar | Etapas |
|---|---|---|
| **Padrão** | Análise completa de conteúdo único | Pipeline completo (11 etapas) |
| **Comparação** | Duas fontes sobre o mesmo assunto | Avaliação lado a lado com tabela de concordâncias/contradições |
| **Prebunking** | Preparação contra narrativa falsa esperada | Mapeamento de narrativas ativas + estratégias defensivas |
| **Rápido** | Pergunta sim/não simples | Etapas 1, 2, 6 e 7 apenas |

## Pipeline de 11 etapas

### Etapa 1 — Decomposição de afirmações

Separar o conteúdo em unidades verificáveis. Classificar cada afirmação:

| Tipo | Definição |
|---|---|
| Factual | Verificável com evidência |
| Opinião | Julgamento subjetivo |
| Previsão | Evento futuro incerto |
| Vaga | Imprecisa demais para verificar |
| Implícita | Não dita, mas pressuposta |
| Estatística | Número ou percentual |

### Etapa 2 — Investigação de fontes

Buscar evidências em múltiplas línguas quando relevante. Exigir triangulação de 3+ fontes independentes de Tier 1–4. Aplicar avaliação CRAAP: Currency (atualidade), Relevance (relevância), Authority (autoridade), Accuracy (precisão), Purpose (propósito).

### Etapa 3 — Avaliação profunda de fontes online (protocolo de leitura lateral)

Para cada fonte relevante:
- Auditoria do site: propriedade, missão, padrões editoriais, legitimidade do domínio
- Verificação do autor: credenciais, histórico, pessoa real
- Avaliação de evidências e citações: fontes primárias, metodologia
- Verificação cruzada: o que fontes independentes dizem sobre esse veículo

### Etapa 4 — Rastreamento de origem

Identificar primeira aparição do conteúdo, idioma original, mutações ao longo da cadeia de compartilhamento, associação com campanhas coordenadas.

### Etapa 5 — Detecção de sinais de alerta

Varrer o conteúdo contra 6 categorias de manipulação (40+ marcadores):

**A — Manipulação emocional**
- Urgência artificial ("URGENTE!!!", correntes de WhatsApp, "compartilhe antes que apaguem")
- Gatilhos de medo específicos: saúde de crianças, perda de emprego, violência, segurança financeira
- Indignação e enquadramento tribal ("eles não querem que você saiba", "a mídia esconde")
- Apelo à vaidade ou identidade grupal ("brasileiros de bem", "quem tem consciência sabe")
- Linguagem apocalíptica desproporcionada ao conteúdo

**B — Problemas de atribuição**
- Fontes anônimas ou genéricas ("médicos afirmam", "especialistas dizem", "fonte confiável")
- Especialistas reais citados fora de contexto ou com credencial distorcida
- Veículos imitados (nomes parecidos com G1, Folha, CNN Brasil)
- Print de tela sem URL, data ou contexto verificável
- Vídeo cortado que omite contexto crucial
- Tradução distorcida de conteúdo estrangeiro

**C — Falácias lógicas**
- Cherry-picking: selecionar apenas evidências favoráveis
- Falsa dicotomia: apresentar duas opções quando existem mais
- Espantalho: distorcer a posição contrária para refutá-la mais facilmente
- Post hoc ergo propter hoc: correlação apresentada como causalidade
- Apelo à natureza: "natural" = bom, "artificial" = ruim
- Falso consenso: "todo mundo sabe que...", "a maioria das pessoas concorda..."
- Slippery slope: "se X acontecer, inevitavelmente Y e Z virão"

**D — Manipulação temporal/contextual**
- Conteúdo reciclado de outro país apresentado como brasileiro
- Foto ou vídeo de outra época apresentado como atual
- Data alterada em print ou manchete
- Headline sensacionalista contradiz o corpo do texto
- Edição seletiva que omite parte relevante da declaração original
- Mistradução intencional de conteúdo em outro idioma

**E — Sinais coordenados**
- Astroturfing: movimento popular artificial com coordenação oculta
- Clickbait: título projetado para engajamento emocional, não informação
- Deepfake de áudio, vídeo ou imagem de figuras públicas
- Padrões de bot: publicação sincronizada, comentários idênticos em múltiplas plataformas
- Grupo coordenado de comentários impulsionando narrativa
- Influencer com posicionamento pago sem disclosure (#publi, #ad ausente)

**F — Saúde (específico para Brasil)**
- Curas milagrosas sem ensaio clínico (chás, protocolos, suplementos)
- Uso indevido de dados do OpenDataSUS ou registros de VAERS/Notivisa fora de contexto
- Distorção de bulas ou notas técnicas da ANVISA
- Kit covid, cloroquina, ivermectina como referências a tratamentos validados
- Médico como autoridade em área fora de sua especialidade
- "Tratamento proibido pelos médicos" como enquadramento anti-institucional

### Etapa 6 — Atribuição de veredicto

| Veredicto | Critério |
|---|---|
| CONFIRMADO | Afirmação verificada por múltiplas fontes independentes confiáveis |
| MAJORITARIAMENTE VERDADEIRO | Essencialmente correto com imprecisões menores |
| MISTO | Parte verdadeira, parte falsa ou enganosa |
| NÃO VERIFICADO | Evidência insuficiente para confirmar ou refutar |
| ENGANOSO | Tecnicamente correto mas apresentado de forma a criar impressão falsa |
| FALSO | Contradito por evidência sólida |

### Etapa 7 — Pontuação MFS (Manipulation & Falsehood Score)

Calcular score de 0–100 combinando três componentes:

- **CFS** — Índice de Falsidade das Afirmações: afirmações falsas/enganosas ÷ total (peso 50%)
- **MTS** — Índice de Técnicas de Manipulação: técnicas detectadas × severidade (peso 30%)
- **SCD** — Déficit de Credibilidade das Fontes: dependência de fontes de baixo tier (peso 20%)

Escala interpretativa: 0–20 confiável · 21–40 precaução · 41–60 problemático · 61–80 enganoso · 81–100 desinformação

### Etapa 8 — Calibração de confiança

Fatores que aumentam confiança: fontes primárias diretas, múltiplos Tier 1 independentes, consenso científico documentado, dados governamentais oficiais.

Fatores que reduzem confiança: fontes de acesso restrito, conteúdo recente sem cobertura suficiente, área com alto nível de desinformação ativa, trabalho offline com dados de treinamento.

**Modo offline:** declarar limitação explicitamente, reduzir confiança um nível, orientar para verificação manual.

### Etapa 9 — Cadeia de raciocínio

Para veredictos não óbvios (MISTO, ENGANOSO, FALSO): apresentar o raciocínio passo a passo de forma auditável.

### Etapa 10 — Análise contrafactual

Para afirmações FALSAS ou ENGANOSAS: "O que precisaria ser verdadeiro para essa afirmação ser confirmada?" Identifica qual elemento específico invalida o conteúdo.

### Etapa 11 — Componente educacional

Ensinar verificação independente:
- Técnicas de manipulação detectadas com explicação do viés cognitivo explorado
- Método de leitura lateral (protocolo Stanford): parar → sair da página → verificar o que outros dizem sobre a fonte → buscar cobertura melhor
- 5 perguntas universais de avaliação de fonte
- Alertas de narrativas conhecidas sobre o tema
- Vacina de prebunking (inoculação contra as técnicas específicas usadas)

## Hierarquia de fontes — Brasil

| Tier | Tipo | Exemplos |
|---|---|---|
| 1 | Verificadores IFCN certificados | Aos Fatos, Agência Lupa, AFP Checamos, Comprova, Agência Pública |
| 2 | Órgãos governamentais oficiais | ANVISA, Ministério da Saúde, IBGE, TSE, STF, STJ, Planalto, SENACON |
| 3 | Agências de notícias e veículos de referência | Reuters Brasil, AP, BBC Brasil, UOL Confere |
| 4 | Publicações científicas peer-reviewed | SciELO, Fiocruz, CFM, FAPESP, publicações com DOI |
| 5 | Especialistas de domínio com credenciais verificáveis | IPEA, CNPq, OAB, CFM, sociedades científicas |
| 6 | Veículos com padrões editoriais reconhecidos | Folha, Estadão, G1, O Globo, Valor Econômico |
| 7 | Blogs, sites pessoais, redes sociais | Baixa confiabilidade por padrão |
| 8 | Fontes anônimas ou sem atribuição | Muito baixa confiabilidade |

## Contexto brasileiro de desinformação

**Vetores principais:**
- WhatsApp como canal primário (grupos fechados, sem rastreabilidade de origem, alto alcance)
- Telegram para conteúdo mais extremo e coordenado
- YouTube para vídeos longos de desinformação (pseudodocumentários, "exposes")

**Narrativas recorrentes:**
- Fraude eleitoral e ataques às urnas eletrônicas / TSE
- Negacionismo científico (vacinas, COVID, clima)
- Desinformação em saúde (curas milagrosas, tratamentos sem evidência, auto-medicação)
- Narrativas anti-STF, anti-Ministério Público, anti-imprensa
- Fake news financeiras (investimentos falsos, pirâmides, golpes com criptomoedas)
- Conteúdo reciclado (fotos/vídeos de outros países ou outras épocas apresentados como atuais no Brasil)
- Deepfakes de figuras políticas e empresariais brasileiras

**Sinal de alerta específico para Brasil:** conteúdo que chega sem fonte identificável via "foi no grupo do zap" ou "vi num vídeo" — aplicar escrutínio máximo.

## Protocolo de leitura lateral

Técnica central: gastar menos tempo *dentro* da fonte, mais tempo verificando *o que outros dizem sobre* ela.

1. **PARAR** — Registrar afirmação e fonte sem leitura profunda ainda
2. **SAIR DA PÁGINA** — Pesquisar sobre a credibilidade da fonte externamente
3. **VERIFICAR O QUE FONTES INDEPENDENTES DIZEM** — Wikipedia, Media Bias/Fact Check, buscas pelo nome do veículo
4. **ENCONTRAR COBERTURA MELHOR** — Buscar a afirmação em palavras diferentes por veículos de Tier 1–3

## Saída — formato Markdown

> **Nota de adaptação:** O original ([fact-check-skill](https://github.com/petar-nauka/fact-check-skill)) gera HTML cards com CSS inline. Esta versão PT-BR gera Markdown estruturado — mais adequado para fluxos baseados em texto (Claude.ai, terminais, Obsidian). A estrutura analítica é equivalente.

> **Modo offline:** quando sem acesso a ferramentas web, declarar a limitação explicitamente, reduzir a confiança do veredicto um nível e orientar o usuário para verificação manual com as fontes de Tier 1–2 listadas em `SOURCES.md`.

Entregar inline no chat no seguinte formato:

```
## Resultado: Verificação de Fatos

**Veredicto:** [CONFIRMADO / MAJORITARIAMENTE VERDADEIRO / MISTO / NÃO VERIFICADO / ENGANOSO / FALSO]
**Confiança:** [Alta / Média / Baixa]

**Pontuação MFS:** XX/100
- Índice de Falsidade (CFS): XX/100 — peso 50%
- Técnicas de Manipulação (MTS): XX/100 — peso 30%
- Déficit de Credibilidade (SCD): XX/100 — peso 20%

---

### Afirmações identificadas

| # | Afirmação | Tipo | Veredicto |
|---|---|---|---|
| 1 | ... | Factual | ... |

### Fontes consultadas

[lista com tier e avaliação]

### Sinais de alerta detectados

[se houver — categoria + descrição]

### Rastreamento de origem

[primeira aparição identificada / origem não rastreada]

### Como verificar você mesmo

[orientações práticas de leitura lateral para este caso específico]
```

**Salvar resultado:** se solicitado, salvar em arquivo Markdown com frontmatter `tipo: verificação`.
