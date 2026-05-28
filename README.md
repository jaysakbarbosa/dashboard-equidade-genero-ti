# Dashboard de Equidade de Gênero em TI

> Protocolo padronizado para diagnóstico da equidade de gênero em cursos de Tecnologia da Informação em instituições de ensino superior brasileiras.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jaysakbarbosa/dashboard-equidade-genero-ti/blob/main/dashboard_equidade_ti.ipynb)

---

## O que é

Este repositório contém o notebook interativo que implementa o **Protocolo Padronizado para Diagnóstico de Equidade de Gênero em Cursos de TI (v1.0)**, permitindo que qualquer instituição de ensino superior realize um diagnóstico comparável, replicável e contínuo da sua situação de equidade de gênero.

O dashboard calcula automaticamente as três primeiras métricas do modelo *Leaky Pipeline*, que cobrem o percurso estudantil completo:

| Métrica | O que mede | Fonte de dados |
|---------|------------|----------------|
| **M1 — Ingresso** | % de mulheres entre os ingressantes em TI | Arquivo de ingressantes (ex.: SISU, vestibular) |
| **M2 — Evasão** | Gap de evasão entre gêneros (TEF − TEM) | Arquivo de coorte com situação acadêmica |
| **M3 — Conclusão** | % de mulheres entre os concluintes em TI | Arquivo de egressos ou coorte |

A **fase crítica** (Ingresso, Permanência ou Conclusão) é identificada automaticamente com recomendações específicas de ação.

> **Escopo do dashboard:** cobre M1, M2 e M3 (percurso estudantil). O protocolo completo prevê também M4 (% de docentes mulheres) e M5 (% de mulheres em liderança), que requerem dados de RH/gestão e estão fora do escopo deste dashboard.

---

## Estrutura do repositório

```
.
├── dashboard_equidade_ti.ipynb        # Notebook principal — rode no Google Colab
├── PROTOCOLO_EQUIDADE_GENERO_TI_v1.md # Especificação completa do protocolo
├── requirements.txt                   # Dependências Python (para execução local)
└── README.md
```

---

## Como usar (Google Colab — recomendado)

### 1. Prepare a pasta no Google Drive

Crie uma pasta chamada **`equidade_ti`** no seu Google Drive e coloque dentro dela:

- Este notebook (`dashboard_equidade_ti.ipynb`)
- Os arquivos de dados da sua instituição (veja os formatos aceitos abaixo)

### 2. Abra o notebook no Colab

- No Google Drive: clique com o botão direito no notebook → **Abrir com → Google Colaboratory**
- Ou clique no badge **"Abrir no Colab"** acima

### 3. Execute todas as células

**Ambiente de execução → Executar tudo**

Na primeira execução, o Colab pedirá permissão para acessar o Drive — clique em **Permitir**.

### 4. Acesse o dashboard

No output da última célula aparecerá um link público. Clique nele para abrir o dashboard interativo.

---

## Quais arquivos de dados colocar na pasta

O notebook detecta e classifica automaticamente qualquer arquivo CSV, Excel ou JSON encontrado na pasta do Drive.

### Opção A — Arquivo de coorte completa (recomendado)

Um único arquivo contendo **todos os alunos** com sua situação acadêmica atual. Permite calcular M1, M2 e M3 de uma só vez.

Exemplos de origem:
- SIGAA → Relatório de discentes (exportar com coluna de situação)
- SIG → Exportação de alunos ativos e inativos
- INEP → Microdados do Censo da Educação Superior

### Opção B — Arquivos separados

| Arquivo | Métrica | Conteúdo |
|---------|---------|----------|
| Ingressantes (ex.: dados do SISU) | M1 | Apenas quem entrou |
| Egressos/concluintes | M3 | Apenas quem concluiu |
| Coorte com situação acadêmica | M2 | Todos os alunos com status |

---

## Arquivos de dados aceitos

O notebook aceita dados de **qualquer sistema acadêmico** (SIGAA, SIG, INEP, SISU, etc.) nos formatos **CSV**, **Excel (.xlsx)** ou **JSON**. A normalização de colunas e status é automática.

- **CSV**: separador `,` ou `;` detectado automaticamente; encoding UTF-8 ou latin-1
- **Excel (.xlsx / .xls)**: primeira aba lida automaticamente
- **JSON**: array de objetos `[{"coluna": "valor", ...}, ...]`

### Tipos de arquivo reconhecidos automaticamente por conteúdo

| Tipo | Quando usar | Colunas esperadas (qualquer variação) |
|------|-------------|---------------------------------------|
| **INGRESSO** | Apenas ingressantes | `genero`/`sexo`, `curso`, `ano` |
| **CONCLUSAO** | Apenas egressos | `genero`/`sexo`, `curso`, `ano_conclusao` |
| **COORTE** | Todos com situação | `genero`/`sexo`, `curso`, `ano_ingresso`, `status`/`situacao` |

> **Dica:** Prefira o arquivo de coorte completa — ele permite calcular as três métricas de uma só vez.

### Colunas aceitas (o nome exato não importa, o notebook normaliza)

| Informação | Nomes aceitos |
|------------|---------------|
| Gênero | `sexo`, `genero`, `tp_sexo`, `gender` |
| Nome do curso | `curso`, `nome_curso`, `ds_curso`, `course` |
| Ano de ingresso | `ano_ingresso`, `ano_entrada`, `cohort`, `year` |
| Situação acadêmica | `status`, `situacao`, `ds_situacao`, `tp_situacao` |
| Nível de ensino | `nivel_ensino`, `nivel`, `tp_nivel_academico` |

### Mapeamento de status acadêmico (automático)

| Termos originais (exemplos) | Categoria canônica |
|-----------------------------|--------------------|
| CANCELADO, DESLIGADO, JUBILADO, DESISTÊNCIA | `EVADIDO` |
| CONCLUÍDO, FORMADO, EGRESSO | `CONCLUINTE` |
| MATRICULADO, EM CURSO, ATIVO, TRANCADO | `ATIVO` |

Se o seu sistema usar outro termo, basta adicioná-lo ao dicionário `STATUS_MAP` na célula 6 do notebook.

---

## Personalização dos cursos de TI

Na **célula 4** do notebook você encontrará a lista `CONFIG_TI` com os termos usados para identificar cursos de TI:

```python
CONFIG_TI = {
    "incluir": ["ciencia da computacao", "sistemas de informacao",
                "engenharia de computacao", "redes", "bti",
                "tecnologia da informacao", "engenharia de software", ...],
    "excluir": ["computacao musical", "licenciatura em computacao"]
}
```

Você também pode editar essas listas **ao vivo** no painel ⚙️ do dashboard sem precisar reiniciar o notebook.

---

## Privacidade

> **Atenção:** Os arquivos de dados contêm informações pessoais de estudantes. Não faça upload deles para repositórios públicos. O `.gitignore` deste repositório já está configurado para ignorar arquivos CSV e Excel. Se quiser versionar dados de exemplo, use dados agregados ou anonimizados.

---

## Execução local (sem Colab)

```bash
# 1. Clone o repositório
git clone https://github.com/jaysakbarbosa/dashboard-equidade-genero-ti.git
cd dashboard-equidade-genero-ti

# 2. Instale as dependências
pip install -r requirements.txt

# 3. Coloque seus arquivos de dados em qualquer pasta e ajuste
#    a variável PASTA na célula 2 do notebook

# 4. Abra o notebook
jupyter notebook dashboard_equidade_ti.ipynb
```

---

## Requisitos

- Python 3.9+
- Bibliotecas: `pandas`, `plotly`, `panel`, `openpyxl` (ver `requirements.txt`)
- Para execução no Colab: conta Google (gratuita)

---

## Protocolo

A metodologia completa está documentada em [`PROTOCOLO_EQUIDADE_GENERO_TI_v1.md`](PROTOCOLO_EQUIDADE_GENERO_TI_v1.md), incluindo:

- Definições unificadas de terminologia (ingressante, evasão, concluinte)
- Fórmulas de M1, M2 e M3
- Critérios de classificação por fase crítica
- Recomendações de intervenção por fase
- Diretrizes para comparabilidade entre instituições

---

## Licença

MIT — livre para uso, adaptação e redistribuição com atribuição.
