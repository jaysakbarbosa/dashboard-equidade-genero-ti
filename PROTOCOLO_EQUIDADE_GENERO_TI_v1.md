# PROTOCOLO PADRONIZADO PARA DIAGNÓSTICO DE EQUIDADE DE GÊNERO EM CURSOS DE TI

Versão 1.0 - Abril 2026

---

## SUMÁRIO EXECUTIVO

Este documento especifica protocolo padronizado para diagnóstico de equidade de gênero em cursos de Tecnologia da Informação e Computação, aplicável a qualquer instituição federal de ensino brasileira.

**Objetivo:** Permitir que qualquer instituição realize diagnóstico comparável, replicável e contínuo de sua situação de equidade de gênero usando dados públicos disponíveis.

**Diferencial:** Primeiro protocolo que resolve problema da falta de comparabilidade entre estudos institucionais através de terminologia unificada, métricas padronizadas e processo documentado.

---

## 1. INTRODUÇÃO

### 1.1 Contexto

Diversas instituições brasileiras têm documentado sub-representação feminina em cursos de TI através de estudos quantitativos. Porém, cada instituição desenvolve metodologia própria, impossibilitando comparação de resultados e replicação de processos.

### 1.2 Escopo

Este protocolo cobre:
- Diagnóstico quantitativo de equidade de gênero em cursos de graduação em TI
- Análise de cinco fases: ingresso, permanência, conclusão, docência, liderança
- Identificação de fase crítica do pipeline onde ocorre maior perda
- Geração de recomendações específicas por fase

Este protocolo NÃO cobre:
- Análise qualitativa (causas da disparidade requerem complementação com entrevistas)
- Pós-graduação (foco é graduação)
- Análise detalhada de desempenho acadêmico
- Questões interseccionais (raça, classe, etc.) - podem ser incorporadas em versões futuras

### 1.3 Público-Alvo

- Gestores institucionais (reitoria, pró-reitorias, coordenações)
- Núcleos de estudos de gênero
- Comissões de equidade
- Pesquisadores da área

Não é necessário conhecimento em programação ou análise de dados - o dashboard automatiza todo o processo técnico.

---

## 2. TERMINOLOGIA UNIFICADA

**PROBLEMA RESOLVIDO:** Cada estudo existente define conceitos básicos de forma diferente. Por exemplo, "evasão" pode significar trancamento, jubilamento, cancelamento, ou até transferência de curso, dependendo do estudo.

Esta seção estabelece definições unificadas e inequívocas.

### 2.1 Definições Básicas

**INGRESSANTE**
- Definição: Aluno que realizou matrícula inicial em curso de graduação em TI no ano de referência
- Inclui: Todos os formas de ingresso (vestibular, ENEM/SISU, transferência, reopção)
- Exclui: Reingressos (aluno que retorna após trancamento)
- Exemplo: Aluno matriculado pela primeira vez em BTI em 2024 é ingressante de 2024

**MATRICULADO / ATIVO**
- Definição: Aluno com matrícula regular ativa no curso
- Inclui: Alunos cursando disciplinas regularmente
- Exclui: Alunos em situações especiais (trancamento, formandos que já colaram grau)
- Exemplo: Aluno de 3º período com matrícula ativa em 2024 é matriculado

**EVADIDO**
- Definição: Aluno que saiu definitivamente do curso antes de concluí-lo
- Inclui: Trancamento sem retorno, cancelamento de matrícula, jubilamento
- EXCLUI: Transferência para outro curso da mesma instituição (não é evasão da instituição)
- EXCLUI: Trancamento com retorno posterior (aluno volta a ser matriculado)
- Importante: Esta é definição estrita de evasão do curso, não da instituição
- Exemplo: Aluno que cancela matrícula em CC em 2023 é evadido de 2023

**CONCLUINTE**
- Definição: Aluno que integralizou todos os créditos obrigatórios e realizou colação de grau
- Inclui: Apenas formados oficialmente
- Exclui: Alunos que integralizaram créditos mas ainda não colaram grau (ainda são matriculados)
- Exemplo: Aluno que cola grau em EC em julho/2024 é concluinte de 2024

**DOCENTE**
- Definição: Professor com vínculo efetivo ou temporário no departamento/curso de TI
- Inclui: Professores efetivos, substitutos, temporários
- Exclui: Professores de outros departamentos que apenas ministram disciplinas ocasionais
- Exemplo: Professor do DIMAp com vínculo efetivo é docente

**POSIÇÃO DE LIDERANÇA**
- Definição: Cargo de gestão ou coordenação em estrutura acadêmica/administrativa
- Inclui: Coordenação de curso, chefia de departamento, direção de centro/instituto
- Exclui: Coordenação de projeto de pesquisa/extensão (não é gestão institucional)
- Exemplo: Coordenadora do curso de BTI ocupa posição de liderança

### 2.2 Definições de Métricas

**COORTE**
- Definição: Conjunto de alunos que ingressaram no mesmo ano
- Uso: Permite acompanhamento longitudinal (acompanhar coorte 2020 até conclusão)
- Exemplo: Coorte 2020 = todos que ingressaram em 2020

**TAXA DE EVASÃO**
- Fórmula: (Número de Evadidos da Coorte X / Número de Ingressantes da Coorte X) × 100
- Interpretação: Percentual de alunos que saiu sem concluir
- Observação: Taxa calculada por coorte, não por ano corrente
- Exemplo: Coorte 2020 com 250 ingressantes e 75 evadidos até 2024 = taxa 30%

**TAXA DE CONCLUSÃO**
- Fórmula: (Número de Concluintes da Coorte X / Número de Ingressantes da Coorte X) × 100
- Interpretação: Percentual de alunos que formou
- Observação: Idealmente calculada após tempo esperado de conclusão + margem
- Exemplo: Coorte 2018 (curso de 4 anos) analisada em 2024 (6 anos depois)

**GAP DE GÊNERO**
- Fórmula: Métrica_Feminina - Métrica_Masculina
- Interpretação: Diferença entre gêneros em pontos percentuais
- Convenção: Gap positivo indica métrica feminina maior; gap negativo indica métrica masculina maior
- Exemplo: Taxa evasão F=35%, M=28% → Gap = +7 p.p. (mulheres evadem 7 p.p. a mais)

**PIPELINE LEAKY (Funil com vazamento)**
- Conceito: Metáfora para perda progressiva de mulheres em cada fase da carreira
- Fases típicas: Ensino Médio (50%) → Ingresso TI (15%) → Docência (20%) → Liderança (10%)
- Uso: Identifica em qual fase ocorre maior perda percentual

---

## 3. REQUISITOS DE DADOS

### 3.1 Dados Mínimos Obrigatórios

Para executar diagnóstico básico, a instituição DEVE fornecer dataset contendo:

| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| id_aluno | string/int | Identificador único do aluno (pode ser anonimizado) | "A20240001" ou hash |
| genero | string | Gênero do aluno | "F", "M", "Feminino", "Masculino" |
| curso | string | Nome ou código do curso | "Bacharelado em TI", "BTI" |
| ano_ingresso | int | Ano de ingresso no curso | 2024 |
| situacao | string | Situação atual do aluno | "Ativo", "Concluído", "Evadido" |

**Observações:**
- Campo `id_aluno` pode ser hash/código anonimizado para proteção de privacidade
- Campo `genero` aceita variações de escrita (normalização é automática)
- Campo `curso` deve permitir identificação clara de cursos de TI
- Campo `ano_ingresso` deve ser ano de primeira matrícula no curso
- Campo `situacao` deve refletir status mais recente

### 3.2 Dados Complementares Opcionais

Para análises aprofundadas, recomenda-se incluir:

| Campo | Tipo | Uso | Exemplo |
|-------|------|-----|---------|
| semestre_ingresso | int | Análise semestral (não apenas anual) | 1 ou 2 |
| nota_ingresso | float | Correlação com desempenho | 7.5 |
| coeficiente_rendimento | float | Análise de desempenho acadêmico | 8.2 |
| tempo_conclusao | int | Tempo real para formar (em semestres) | 9 |
| ano_conclusao | int | Ano de formatura | 2024 |
| ano_evasao | int | Ano de saída | 2023 |
| cotista | bool | Análise interseccional (cota + gênero) | true |
| renda_familiar | cat | Análise socioeconômica | "até 1.5 SM" |

### 3.3 Dados de Docentes (para análise de progressão)

Para análise de fase docência/liderança:

| Campo | Tipo | Descrição | Exemplo |
|-------|------|-----------|---------|
| id_docente | string/int | Identificador do docente | "D001" |
| genero | string | Gênero | "F", "M" |
| departamento | string | Departamento/curso | "DIMAp", "DCA" |
| cargo | string | Tipo de vínculo | "Efetivo", "Substituto" |
| titulacao | string | Maior titulação | "Doutor", "Mestre" |
| ano_ingresso_docencia | int | Ano de entrada na instituição | 2015 |
| cargo_gestao | string | Cargo de liderança (se houver) | "Coordenador" |
| ano_inicio_gestao | int | Quando assumiu cargo | 2023 |

### 3.4 Formato dos Dados

**Formatos Aceitos:**
- CSV (vírgula ou ponto-e-vírgula como separador)
- Excel (.xlsx, .xls)
- JSON (formato plano ou aninhado simples)

**Codificação:**
- UTF-8 (obrigatório para caracteres acentuados)

**Estrutura:**
- Uma linha por aluno (dados discentes) ou por docente (dados docentes)
- Primeira linha contém nomes das colunas

**Exemplo de Arquivo CSV Válido:**
```
id_aluno,genero,curso,ano_ingresso,situacao
A001,F,Bacharelado em TI,2020,Ativo
A002,M,Ciência da Computação,2020,Evadido
A003,F,Engenharia de Computação,2021,Ativo
```

### 3.5 Qualidade dos Dados

**Checklist de Qualidade** (verificar antes de processar):

- [ ] Arquivo está em formato suportado (CSV/Excel/JSON)?
- [ ] Codificação é UTF-8?
- [ ] Primeira linha contém nomes de colunas?
- [ ] Campos obrigatórios estão presentes?
- [ ] Campo `genero` contém valores válidos (não há células vazias)?
- [ ] Campo `ano_ingresso` contém anos válidos (formato YYYY)?
- [ ] Campo `situacao` está preenchido para todos os registros?
- [ ] Não há linhas duplicadas (mesmo `id_aluno` aparece mais de uma vez)?
- [ ] Cursos de TI estão claramente identificados?

**Tratamento de Valores Ausentes:**
- Registros com `genero` ausente: EXCLUIR (impossibilita análise)
- Registros com `ano_ingresso` ausente: EXCLUIR
- Registros com `situacao` ausente: CLASSIFICAR como "Ativo" (assumir matrícula ativa)

---

## 4. MÉTRICAS PADRONIZADAS

Esta seção especifica formalmente cada métrica do protocolo.

Cada métrica segue estrutura:
- Nome formal (ID único)
- Definição conceitual
- Fórmula matemática
- Requisitos de dados
- Exemplo de cálculo
- Interpretação padronizada
- Limitações conhecidas

### 4.1 MÉTRICA M1: Percentual de Mulheres Ingressantes

**ID:** M1_PERC_INGRESSO

**Definição:** Proporção de mulheres entre todos os ingressantes em cursos de TI no ano de referência.

**Fórmula:**
```
M1 = (Mulheres Ingressantes no Ano X / Total de Ingressantes no Ano X) × 100
```

**Requisitos de Dados:**
- Campo `genero`
- Campo `ano_ingresso`
- Filtro para cursos de TI

**Exemplo de Cálculo:**

Dados de entrada (Ano 2024):
- Total de ingressantes: 250
- Mulheres ingressantes: 35
- Homens ingressantes: 215

Cálculo:
```
M1_2024 = (35 / 250) × 100 = 14%
```

**Interpretação Padronizada:**

| Valor de M1 | Classificação | Ação Recomendada |
|-------------|---------------|------------------|
| M1 < 20% | Disparidade Crítica | Priorizar ações de atração intensivas |
| 20% ≤ M1 < 30% | Disparidade Significativa | Implementar ações de atração |
| 30% ≤ M1 < 40% | Desbalanceamento Moderado | Manter e expandir ações existentes |
| 40% ≤ M1 < 50% | Aproximação da Paridade | Monitorar e consolidar ganhos |
| M1 ≥ 50% | Paridade Alcançada | Manter paridade |

**Análise de Tendência:**

Quando dados de múltiplos anos disponíveis, calcular variação:
```
Variação = M1_ano_final - M1_ano_inicial
```

Interpretação da variação:
- Variação > +5 p.p.: Tendência de crescimento significativa
- Variação entre -5 e +5 p.p.: Estabilidade
- Variação < -5 p.p.: Tendência de queda significativa

**Limitações:**
- Não identifica causas da disparidade
- Não desagrega por curso específico (se instituição tem vários cursos de TI)
- Não considera características socioeconômicas

**Apresentação no Dashboard:**
- Gráfico de linha: Evolução de M1 ao longo dos anos
- Gráfico de barras: M1 por curso (se múltiplos cursos)
- Indicador visual: Cor do alerta conforme classificação

### 4.2 MÉTRICA M2: Gap de Evasão por Gênero

**ID:** M2_GAP_EVASAO

**Definição:** Diferença entre taxa de evasão feminina e masculina em uma coorte específica.

**Fórmulas:**
```
TE_F = (Mulheres Evadidas da Coorte X / Mulheres Ingressantes da Coorte X) × 100
TE_M = (Homens Evadidos da Coorte X / Homens Ingressantes da Coorte X) × 100
M2 = TE_F - TE_M
```

Onde:
- TE_F = Taxa de Evasão Feminina
- TE_M = Taxa de Evasão Masculina
- M2 = Gap de Evasão (em pontos percentuais)

**Requisitos de Dados:**
- Campo `genero`
- Campo `ano_ingresso` (para identificar coorte)
- Campo `situacao` (para identificar evadidos)

**Exemplo de Cálculo:**

Dados de entrada (Coorte 2020, analisada em 2024):
- Mulheres ingressantes em 2020: 40
- Mulheres evadidas até 2024: 15
- Homens ingressantes em 2020: 210
- Homens evadidos até 2024: 63

Cálculo:
```
TE_F = (15 / 40) × 100 = 37.5%
TE_M = (63 / 210) × 100 = 30.0%
M2 = 37.5 - 30.0 = +7.5 pontos percentuais
```

**Interpretação Padronizada:**

| Valor de M2 | Classificação | Ação Recomendada |
|-------------|---------------|------------------|
| M2 < -15 p.p. | Evasão Masculina Crítica | Investigar causas de evasão masculina |
| -15 ≤ M2 < -5 | Evasão Masculina Moderada | Monitorar tendência masculina |
| -5 ≤ M2 ≤ +5 | Paridade Aceitável | Manter políticas atuais |
| +5 < M2 ≤ +15 | Evasão Feminina Moderada | Implementar programas de retenção feminina |
| M2 > +15 p.p. | Evasão Feminina Crítica | Intervenção urgente necessária |

**Análise Temporal:**

Calcular M2 para múltiplas coortes e analisar tendência:
```
Tendência = M2_coorte_recente - M2_coorte_antiga
```

**Limitações:**
- Não identifica CAUSAS da evasão (requer análise qualitativa complementar)
- Coortes pequenas (< 30 mulheres) têm alta variação estatística
- Recomenda-se analisar pelo menos 3 coortes consecutivas
- Tempo de análise: coorte deve ter pelo menos 2 anos desde ingresso

**Apresentação no Dashboard:**
- Gráfico de barras duplas: TE_F vs TE_M por coorte
- Gráfico de linha: Evolução do Gap ao longo das coortes
- Alertas visuais: Verde |M2| < 5, Amarelo 5-15, Vermelho > 15

### 4.3 MÉTRICA M3: Percentual de Mulheres Concluintes

**ID:** M3_PERC_CONCLUSAO

**Definição:** Proporção de mulheres entre concluintes de cursos de TI no ano de referência.

**Fórmula:**
```
M3 = (Mulheres Concluintes no Ano X / Total de Concluintes no Ano X) × 100
```

**Requisitos de Dados:**
- Campo `genero`
- Campo `situacao` (filtrar por "Concluído")
- Campo `ano_conclusao` OU inferir por `situacao` + ano atual

**Exemplo de Cálculo:**

Dados de entrada (Ano 2024):
- Total de concluintes: 180
- Mulheres concluintes: 24
- Homens concluintes: 156

Cálculo:
```
M3_2024 = (24 / 180) × 100 = 13.3%
```

**Interpretação Padronizada:**

Comparar M3 com M1 do mesmo período:
- Se M3 ≈ M1: Paridade mantida ao longo do curso
- Se M3 < M1: Perda adicional durante o curso (além do ingresso)
- Se M3 > M1: Recuperação parcial (mulheres formam em proporção maior que ingressam)

**Limitações:**
- Não considera tempo para conclusão (algumas podem levar mais tempo)
- Ideal é analisar por coorte (comparar ingressantes 2020 com concluintes 2024)

**Apresentação no Dashboard:**
- Gráfico de linha: M3 ao longo dos anos
- Gráfico comparativo: M1 vs M3 lado a lado

### 4.4 MÉTRICA M4: Percentual de Mulheres Docentes - NÂO IMPLEMENTADO

**ID:** M4_PERC_DOCENTES

**Definição:** Proporção de mulheres no corpo docente de cursos/departamentos de TI.

**Fórmula:**
```
M4 = (Mulheres Docentes / Total de Docentes) × 100
```

**Requisitos de Dados:**
- Dataset de docentes com campo `genero`
- Filtro para departamento/curso de TI

**Exemplo de Cálculo:**

Dados de entrada (2024):
- Total de docentes em TI: 45
- Mulheres docentes: 9
- Homens docentes: 36

Cálculo:
```
M4_2024 = (9 / 45) × 100 = 20%
```

**Interpretação Padronizada:**

| Valor de M4 | Classificação | Observação |
|-------------|---------------|------------|
| M4 < 15% | Muito Baixa Representação | Abaixo da média de ingressantes |
| 15% ≤ M4 < 25% | Baixa Representação | Próximo à média de ingressantes |
| 25% ≤ M4 < 35% | Representação Moderada | Acima da média de ingressantes |
| M4 ≥ 35% | Representação Significativa | Avanço em relação ao pipeline |

**Limitações:**
- Não considera nível de titulação (professores adjuntos vs titulares)
- Não considera tempo de casa (novatos vs veteranos)

**Apresentação no Dashboard:**
- Gráfico de pizza: Distribuição por gênero
- Comparação: M4 vs M3 (concluintes) vs M1 (ingressantes)

### 4.5 MÉTRICA M5: Percentual de Mulheres em Liderança - NÂO IMPLEMENTADO

**ID:** M5_PERC_LIDERANCA

**Definição:** Proporção de mulheres em cargos de coordenação e gestão em TI.

**Fórmula:**
```
M5 = (Mulheres em Cargos de Liderança / Total de Cargos de Liderança) × 100
```

**Requisitos de Dados:**
- Dataset de docentes com campo `cargo_gestao`
- Filtro para cargos de liderança em TI

**Cargos Considerados:**
- Coordenação de curso de graduação em TI
- Coordenação de programa de pós-graduação em TI
- Chefia de departamento de TI/Computação
- Direção de centro/instituto que inclui TI

**Exemplo de Cálculo:**

Dados de entrada (2024):
- Total de cargos de liderança: 6
  * Coordenação BTI: 1
  * Coordenação CC: 1
  * Coordenação EC: 1
  * Coordenação PPgSC: 1
  * Chefia DIMAp: 1
  * Subchefia DIMAp: 1
- Mulheres em liderança: 1 (Coordenação EC)
- Homens em liderança: 5

Cálculo:
```
M5_2024 = (1 / 6) × 100 = 16.7%
```

**Interpretação Padronizada:**

| Valor de M5 | Classificação | Observação |
|-------------|---------------|------------|
| M5 = 0% | Ausência Total | Nenhuma mulher em liderança |
| 0% < M5 < 20% | Representação Simbólica | Muito abaixo da proporção de docentes |
| 20% ≤ M5 < 40% | Representação Limitada | Abaixo da paridade |
| M5 ≥ 40% | Aproximação da Paridade | Representa avanço significativo |

**Limitações:**
- Número pequeno de cargos (alta variação estatística)
- Não considera duração no cargo (recém-assumiu vs veterano)
- Não considera nível hierárquico (coordenação vs direção)

**Apresentação no Dashboard:**
- Lista de cargos com indicação de gênero
- Comparação: M5 vs M4 (docentes) vs M3 (concluintes)

---

## 5. PROCESSO DE DIAGNÓSTICO

Este capítulo detalha passo a passo como executar diagnóstico completo.

### 5.1 Visão Geral do Processo

```
[1. Obter Dados] → [2. Preparar Arquivo] → [3. Upload] → 
[4. Validação] → [5. Processamento] → [6. Análise] → [7. Relatório]
```

Tempo estimado: 30 minutos a 2 horas (dependendo de familiaridade e disponibilidade dos dados)

### 5.2 Passo 1: Obtenção dos Dados

**Opção A: Portal de Dados Abertos da Instituição**

A maioria das universidades federais mantém portal de dados abertos.

Exemplo UFRN: http://dados.ufrn.br
- Acessar portal
- Procurar por "discentes" ou "alunos"
- Baixar dataset completo ou filtrar por período

**Opção B: Solicitação ao Setor de TI/Gestão Acadêmica**

Se portal não disponível ou dados não atualizados:
- Entrar em contato com Superintendência de Informática ou Pró-Reitoria de Graduação
- Solicitar exportação de dados de alunos de cursos de TI
- Especificar campos necessários (ver Seção 3)
- Pedir formato CSV ou Excel

**Opção C: Sistema Integrado de Gestão (SIG)**

Se possui acesso direto ao SIG:
- Acessar módulo acadêmico
- Gerar relatório de alunos
- Exportar para CSV/Excel

**Dados de Docentes:**

- Portal de Transparência (docentes ativos)
- Departamento de Gestão de Pessoas
- Site do departamento/curso (lista de docentes)

### 5.3 Passo 2: Preparação do Arquivo

**Checklist de Preparação:**

1. **Abrir arquivo no Excel ou editor de planilhas**
   - Verificar se primeira linha contém nomes de colunas
   - Verificar se dados estão organizados (uma linha por aluno)

2. **Identificar cursos de TI**
   - Localizar coluna de curso
   - Identificar quais cursos são de TI (Ciência da Computação, BTI, Engenharia de Computação, etc.)
   - Anotar nomes EXATOS dos cursos

3. **Verificar campos obrigatórios**
   - Gênero: coluna existe e está preenchida?
   - Ano de ingresso: coluna existe?
   - Situação: coluna existe?

4. **Limpeza básica (se necessário)**
   - Remover linhas completamente vazias
   - Verificar se não há caracteres especiais estranhos nos nomes de colunas
   - Salvar como CSV UTF-8 ou manter Excel

5. **Anonimização (opcional)**
   - Se arquivo será compartilhado publicamente, substituir nomes/CPFs por códigos
   - Manter apenas identificador único anonimizado

**Exemplo de Arquivo Pronto:**
```
id,sexo,curso,ano_ingresso,situacao
001,F,CIÊNCIA DA COMPUTAÇÃO,2020,ATIVO
002,M,BTI,2020,CONCLUÍDO
003,F,ENGENHARIA DE COMPUTAÇÃO,2021,EVADIDO
```

### 5.4 Passo 3: Upload no Dashboard

1. **Acessar dashboard**
   - URL: [será especificada quando dashboard estiver hospedado]
   - Não requer login (versão pública)

2. **Clicar em "Fazer Upload de Dados"**
   - Arrastar arquivo ou clicar para selecionar
   - Aguardar upload (barra de progresso)

3. **Confirmar formato**
   - Sistema detecta automaticamente se CSV ou Excel
   - Se CSV, detecta separador (vírgula vs ponto-e-vírgula)

### 5.5 Passo 4: Validação e Mapeamento

1. **Mapeamento Automático de Colunas**

Sistema apresenta tela:
```
Detectamos as seguintes colunas:

Gênero:    [sexo          ▼]  ✓ Confiança: 98%
Curso:     [curso         ▼]  ✓ Confiança: 95%
Ano:       [ano_ingresso  ▼]  ✓ Confiança: 100%
Situação:  [situacao      ▼]  ⚠ Confiança: 75%

[Confirmar] [Ajustar Manualmente]
```

2. **Correção Manual (se necessário)**

Se sistema não detectou alguma coluna corretamente:
- Clicar em dropdown
- Selecionar coluna correta manualmente
- Clicar em "Confirmar"

3. **Seleção de Cursos**

Sistema lista todos os cursos encontrados:
```
Quais cursos de TI deseja analisar?

☑ BACHARELADO EM TECNOLOGIA DA INFORMAÇÃO
☑ CIÊNCIA DA COMPUTAÇÃO
☑ ENGENHARIA DE COMPUTAÇÃO
☐ ENGENHARIA ELÉTRICA (não é TI)
☐ MATEMÁTICA (não é TI)

[Continuar]
```

4. **Validação de Dados**

Sistema verifica:
- Quantidade de registros encontrados
- Quantidade de valores inválidos (gênero vazio, ano inválido, etc.)
- Apresenta estatísticas básicas

Se problemas encontrados:
```
⚠ Encontrados 5 registros com gênero vazio
⚠ Encontrados 2 registros com ano de ingresso inválido (ano 999)

[Excluir Registros Inválidos e Continuar]
[Cancelar e Revisar Arquivo]
```

### 5.6 Passo 5: Processamento

Sistema executa automaticamente (sem intervenção do usuário):

1. **Normalização**
   - Padroniza valores de gênero (F/Feminino/FEMININO → F)
   - Padroniza valores de situação (Ativo/ATIVO/Matriculado → ATIVO)

2. **Cálculo de Métricas**
   - M1: Percentual de ingressantes por ano
   - M2: Gap de evasão por coorte
   - M3: Percentual de concluintes
   - M4 e M5: Se dados de docentes disponíveis

3. **Geração de Visualizações**
   - Gráficos interativos
   - Tabelas resumo
   - Indicadores visuais

Tempo estimado: 10-30 segundos

### 5.7 Passo 6: Análise dos Resultados

Dashboard apresenta resultados em abas:

**ABA 1: RESUMO EXECUTIVO**
```
DIAGNÓSTICO DE EQUIDADE DE GÊNERO - UFRN

Período Analisado: 2010-2025
Total de Registros: 3.847
Cursos: BTI, Ciência da Computação, Engenharia de Computação

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 FASE CRÍTICA IDENTIFICADA: INGRESSO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Mulheres representam apenas 11% dos ingressantes em 2025,
uma queda de 5 pontos percentuais desde 2010.

A maior perda ocorre ANTES do ingresso na universidade.

RECOMENDAÇÃO PRIORITÁRIA:
Focar esforços em ações de atração (ensino médio, divulgação)
em vez de concentrar apenas em retenção de alunas.

[Ver Análise Detalhada] [Baixar Relatório PDF]
```

**ABA 2: INGRESSO (Métrica M1)**
- Gráfico de linha: Evolução anual do percentual de mulheres
- Gráfico de barras: Comparação por curso
- Tabela: Dados numéricos por ano

**ABA 3: PERMANÊNCIA (Métrica M2)**
- Gráfico de barras duplas: Taxa de evasão F vs M
- Gráfico de linha: Evolução do gap
- Análise por coorte

**ABA 4: CONCLUSÃO (Métrica M3)**
- Comparação: Ingresso vs Conclusão
- Identificação de perda no pipeline

**ABA 5: DOCÊNCIA E LIDERANÇA (Métricas M4 e M5)**
- Se dados disponíveis
- Pipeline completo visualizado

**ABA 6: COMPARAÇÃO**
- Se houver dados de outras instituições
- Benchmarking

### 5.8 Passo 7: Geração do Relatório

1. **Clicar em "Baixar Relatório PDF"**

2. **Relatório contém:**
   - Resumo executivo
   - Todas as métricas calculadas
   - Todos os gráficos gerados
   - Tabelas de dados
   - Recomendações específicas por fase
   - Metodologia utilizada

3. **Exportar Dados (opcional)**
   - Baixar dados processados em CSV
   - Útil para análises customizadas

---

## 6. INTERPRETAÇÃO E RECOMENDAÇÕES

### 6.1 Identificação da Fase Crítica

O dashboard identifica automaticamente qual fase do pipeline apresenta maior problema.

**CRITÉRIOS DE IDENTIFICAÇÃO:**

**FASE: INGRESSO**
- Condição: M1 < 30% E M3 ≈ M1
- Diagnóstico: Perda ocorre principalmente antes do ingresso
- Recomendação prioritária: Ações de atração

**FASE: PERMANÊNCIA**
- Condição: M2 > +10 p.p.
- Diagnóstico: Evasão feminina significativamente maior que masculina
- Recomendação prioritária: Programas de retenção

**FASE: CONCLUSÃO**
- Condição: M3 < M1 - 5 p.p.
- Diagnóstico: Perda adicional durante o curso
- Recomendação prioritária: Apoio à conclusão

**FASE: PROGRESSÃO**
- Condição: M4 < M3 - 5 p.p.
- Diagnóstico: Pipeline perde mulheres na transição graduação → docência
- Recomendação prioritária: Incentivo à carreira acadêmica

### 6.2 Recomendações por Fase

**SE FASE CRÍTICA = INGRESSO:**

Ações de Atração (curto prazo):
1. Palestras em escolas de ensino médio apresentando mulheres na TI
2. Olimpíadas e competições de programação para meninas
3. Oficinas de introdução à computação exclusivas para meninas
4. Material de divulgação destacando modelos femininos de referência

Ações de Atração (médio prazo):
5. Parcerias com escolas para projetos de computação com recorte de gênero
6. Programa de mentoria reversa (universitárias visitam escolas)
7. Dia de imersão: alunas do ensino médio passam dia no curso

Ações de Atração (longo prazo):
8. Parceria com Secretaria de Educação para currículo de computação no ensino médio
9. Produção de conteúdo audiovisual desconstruindo estereótipos

**SE FASE CRÍTICA = PERMANÊNCIA:**

Ações de Retenção (curto prazo):
1. Criar grupo de apoio/acolhimento para alunas (encontros mensais)
2. Programa de mentoria: alunas veteranas acompanham calouros
3. Monitoramento proativo: coordenação entra em contato com alunas em risco
4. Flexibilização de prazos para alunas com filhos

Ações de Retenção (médio prazo):
5. Revisão de metodologias pedagógicas com olhar de gênero
6. Capacitação docente sobre viés inconsciente
7. Política institucional contra assédio e discriminação
8. Bolsas específicas para mulheres em TI

Ações de Retenção (longo prazo):
9. Reformulação curricular considerando diversidade
10. Criação de disciplinas optativas com temas de gênero e tecnologia

**SE FASE CRÍTICA = DOCÊNCIA/LIDERANÇA:**

Ações de Progressão (curto prazo):
1. Incentivo para alunas seguirem pós-graduação (divulgar oportunidades)
2. Apoio financeiro para participação em conferências
3. Grupos de pesquisa com lideranças femininas

Ações de Progressão (médio prazo):
4. Política de composição paritária de bancas e comissões
5. Programas de capacitação para liderança
6. Transparência nos processos de seleção para cargos

Ações de Progressão (longo prazo):
7. Revisão de critérios de progressão (considerar licenças-maternidade)
8. Cotas para mulheres em concursos docentes

### 6.3 Monitoramento Contínuo

**FREQUÊNCIA RECOMENDADA:**

Análise Completa: Anual
- Ideal: Sempre no mesmo mês (ex: março de cada ano)
- Permite comparação temporal consistente

Análise Parcial: Semestral
- Apenas métricas M1 e M2 (mais fáceis de calcular)
- Acompanhar tendências em tempo real

**INDICADORES DE SUCESSO:**

Curto Prazo (1-2 anos):
- M1 aumentou em pelo menos 2 p.p.
- M2 reduziu (gap de evasão diminuiu)

Médio Prazo (3-5 anos):
- M1 atingiu 25-30%
- M2 está entre -5 e +5 (paridade na evasão)
- M3 aproximou-se de M1

Longo Prazo (5-10 anos):
- M1 atingiu 40% (aproximação da paridade)
- M4 atingiu 30% (docentes)
- M5 atingiu 30% (liderança)

---

## 7. VALIDAÇÃO E ESTUDO DE CASO

### 7.1 Aplicação na UFRN

**CONTEXTO:**
- Instituição: Universidade Federal do Rio Grande do Norte
- Cursos analisados: BTI, Ciência da Computação, Engenharia de Computação
- Período: 2010-2025
- Total de registros: 3.847 alunos

**RESULTADOS:**

Métrica M1 (Ingresso):
- 2010: 16% mulheres
- 2025: 11% mulheres
- Variação: -5 p.p. (TENDÊNCIA DE QUEDA)

Métrica M2 (Gap de Evasão):
- Coorte 2018: +4 p.p. (paridade aceitável)
- Coorte 2020: +8 p.p. (disparidade moderada)
- Coorte 2022: +12 p.p. (disparidade moderada a crítica)

Métrica M3 (Conclusão):
- 2010-2014: 14% mulheres concluintes
- 2020-2024: 12% mulheres concluintes

**FASE CRÍTICA IDENTIFICADA: INGRESSO**

Diagnóstico: A maior perda ocorre ANTES do ingresso.
Mulheres não estão escolhendo cursos de TI em quantidade significativa.

**RECOMENDAÇÃO:**
Priorizar ações de atração no ensino médio.

---

## 8. LIMITAÇÕES DO PROTOCOLO

1. **Escopo Quantitativo**
   - Protocolo identifica ONDE está o problema, não POR QUE
   - Análise qualitativa (entrevistas, grupos focais) é complemento necessário

2. **Definição Binária de Gênero**
   - Versão atual considera apenas categorias Feminino/Masculino
   - Versões futuras devem incorporar identidades não-binárias

3. **Ausência de Análise Interseccional**
   - Não cruza gênero com raça, classe, deficiência
   - Versões futuras devem incorporar

4. **Dependência de Qualidade dos Dados**
   - Resultados são tão bons quanto os dados fornecidos
   - Dados incompletos ou imprecisos geram diagnósticos imprecisos

5. **Contexto Institucional**
   - Protocolo não considera contexto específico de cada instituição
   - Interpretação deve considerar particularidades locais

---

## 9. TRABALHOS FUTUROS

### 9.1 Versão 2.0 do Protocolo

- Incorporar análise interseccional (gênero + raça + renda)
- Incluir identidades não-binárias
- Adicionar métricas de desempenho acadêmico
- Incorporar dados de mercado de trabalho (pós-formação)

### 9.2 Expansão da Ferramenta

- Versão mobile (app)
- Integração direta com sistemas acadêmicos (SIG, SIGAA)
- Exportação para Power BI / Tableau
- API pública para integração

### 9.3 Rede de Instituições

- Criar consórcio de instituições usando o protocolo
- Dashboard comparativo nacional
- Compartilhamento de boas práticas
- Pesquisa longitudinal agregada

---

## 10. REFERÊNCIAS

[Preencher]

---

## APÊNDICES

### APÊNDICE A: Template de Arquivo CSV

```csv
id_aluno,genero,curso,ano_ingresso,situacao
A001,F,Bacharelado em TI,2020,Ativo
A002,M,Ciência da Computação,2020,Concluído
A003,F,Engenharia de Computação,2021,Evadido
A004,M,Bacharelado em TI,2021,Ativo
```

### APÊNDICE B: Checklist de Qualidade dos Dados

- [ ] Arquivo em formato CSV, Excel ou JSON
- [ ] Codificação UTF-8
- [ ] Primeira linha com nomes de colunas
- [ ] Campos obrigatórios presentes (id, gênero, curso, ano_ingresso, situacao)
- [ ] Sem linhas duplicadas
- [ ] Sem valores vazios em campos críticos (gênero, ano_ingresso)
- [ ] Anos de ingresso válidos (entre 1990 e ano atual)
- [ ] Cursos de TI claramente identificados
- [ ] Situação dos alunos preenchida

### APÊNDICE C: Glossário Completo

**API:** Application Programming Interface - interface para integração entre sistemas

**CSV:** Comma-Separated Values - formato de arquivo texto com valores separados por vírgula

**Dashboard:** Painel interativo de visualização de dados

**Dataset:** Conjunto de dados estruturados

**Gap:** Diferença (em pontos percentuais) entre duas métricas

**Pipeline:** Sequência de fases (metáfora para trajetória acadêmica)

**Ponto Percentual (p.p.):** Unidade de diferença entre percentuais (não confundir com "percentual")
  Exemplo: Subir de 10% para 15% = aumento de 5 p.p. (não 5%)

**UTF-8:** Codificação de caracteres que suporta acentuação

---

**FIM DO DOCUMENTO**

Versão 1.0 - Abril 2026
Licença: Creative Commons BY-SA 4.0
