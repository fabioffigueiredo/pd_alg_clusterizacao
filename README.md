# Projeto de Disciplina — Algoritmos de Clusterização

Resumo do projeto, como executar localmente, estrutura de pastas, decisões técnicas e próximos passos. Este README segue boas práticas: visão geral clara, requisitos, instalação, execução, troubleshooting e roadmap. Soluções simples e reprodutíveis, considerando dev/test/prod.

## Visão Geral
- Objetivo: agrupar países a partir de dados socioeconômicos e de saúde para identificar o grupo em extrema necessidade de ajuda humanitária.
- Abordagens: K‑Means (K‑Médias) e Hierárquica (Ward), com avaliação por Silhouette/Elbow e interpretação dos centróides/perfis por cluster.
- Entregáveis principais:
  - Notebook base: `Projeto_Clusterizacao.ipynb` (com interpretação detalhada e gráficos comparativos por cluster).

## Base de Dados
- Fonte: Kaggle — `rohan0301/unsupervised-learning-on-country-data`.
- Arquivos locais (pasta `data/`):
  - `Country-data.csv`: base principal.
  - `data-dictionary.csv`: dicionário de variáveis.

## Estrutura de Pastas
```
├── Projeto_Clusterizacao.ipynb
├── README.md
├── data/
│   ├── Country-data.csv
│   └── data-dictionary.csv
├── fabioferreirafigueiredo_algoritmosdeinteligenciaartificialparaclusterizacao_pd.pdf
├── images/
│   ├── boxplots_variaveis_numericas.png
│   ├── dendrograma_ward_truncado.png
│   ├── evidenciass.png
│   ├── histogramas_variaveis_numericas.png
│   ├── logo_infnet.png
│   ├── pca_2d_clusters.png
│   └── perfil_clusters_barras.png
├── pd_algoritimos_clusterizacao/
└── requirements.txt
```

## Requisitos
- Python 3.13 (desenvolvido e testado com 3.13.5).
- Jupyter (versão usada: 5.9.1).
- Pacotes: `numpy`, `pandas`, `scikit-learn`, `scipy`, `matplotlib`, `seaborn`, `kaggle` (opcional para download).
- Navegador para visualizar os HTMLs.

## Instalação (dev/test/prod)
1) Crie e ative um ambiente virtual (recomendado):
```
python3 -m venv clusterizacao
source clusterizacao/bin/activate    # macOS/Linux
# No Windows (PowerShell):
# .\clusterizacao\Scripts\Activate.ps1
```

2) Instale as dependências:
```
pip install -r requirements.txt
```

3) Dados:
- Se usar Kaggle API, configure previamente suas credenciais. Caso prefira, copie `Country-data.csv` e `data-dictionary.csv` diretamente para `data/`.

Observações de ambiente:
- Não sobrescreva arquivos `.env` sem confirmação (não são necessários para execução padrão deste projeto).
- Padronize `random_state` e caminhos em um único bloco de configuração quando estender o projeto para múltiplos ambientes.

## Git (repositório e clonagem)
- Repositório oficial: https://github.com/fabioffigueiredo/pd_alg_clusterizacao

Como clonar e preparar o ambiente local:
```
git clone https://github.com/fabioffigueiredo/pd_alg_clusterizacao.git
cd pd_alg_clusterizacao

# (opcional) criar e ativar ambiente virtual
python3 -m venv clusterizacao
source clusterizacao/bin/activate    # macOS/Linux
# No Windows (PowerShell):
# .\clusterizacao\Scripts\Activate.ps1

# instalar dependências
pip install -r requirements.txt

# execução opcional para gerar HTML diretamente
# jupyter nbconvert --to html --execute Projeto_Clusterizacao.ipynb --output Projeto_Clusterizacao.html
```

## Quick Start (execução mínima)
```
python3 -m venv clusterizacao
source clusterizacao/bin/activate    # macOS/Linux
pip install -r requirements.txt

# Gerar HTML executando o notebook completo
jupyter nbconvert --to html --execute Projeto_Clusterizacao.ipynb --output Projeto_Clusterizacao.html

# Servir localmente
python3 -m http.server 8002
# Acesse: http://localhost:8002/Projeto_Clusterizacao.html
```
Se preferir interação, rode `jupyter notebook` e execute `Projeto_Clusterizacao.ipynb` célula a célula.

## Como Executar
### A) Rodar os notebooks no Jupyter
1) Ative o venv e inicie o Jupyter:
```
jupyter notebook
```
2) Abra e execute:
- `Projeto_Clusterizacao.ipynb` (execução interativa e reprodutível).
- Opcional: `Projeto_Clusterizacao_executado.ipynb` para referência das saídas já geradas.

### B) Gerar HTML a partir dos notebooks
Execute os comandos na raiz do projeto:
```
jupyter nbconvert --to html --execute Projeto_Clusterizacao.ipynb --output Projeto_Clusterizacao.html
jupyter nbconvert --to html --execute Projeto_Clusterizacao_executado.ipynb --output Projeto_Clusterizacao_executado.html
```

### C) Visualizar localmente os HTMLs
Inicie um servidor simples e abra no navegador:
```
python3 -m http.server 8002
# Navegue para:
# http://localhost:8002/Projeto_Clusterizacao.html
# http://localhost:8002/Projeto_Clusterizacao_executado.html
```
Se a porta estiver ocupada, altere para 8001/8003.

### D) Gerar PDF
Você pode exportar o notebook para PDF:
```
jupyter nbconvert --to pdf Projeto_Clusterizacao.ipynb
```
Ou imprimir o HTML em PDF via navegador.

## Metodologia (resumo)
1) EDA: estatísticas descritivas, histogramas, boxplots, verificação de outliers.
2) Pré-processamento: padronização com `StandardScaler`.
3) Redução de dimensionalidade: `PCA` para visualização (2D) e análise de variância explicada.
4) Clusterização:
   - K‑Means (variação com centróides). Seleção de `k` com Elbow/Silhouette.
   - Hierárquica (Ward) com dendrograma truncado para inspeção dos agrupamentos.
5) Interpretação: perfis por cluster com médias normalizadas e gráficos de barras comparativos.
6) Discussão: robustez, sensibilidade a outliers e variantes (ex.: medóides, DBSCAN).

## Resultados e Evidências
- Gráficos e imagens em `images/` (PCA em 2D, dendrograma, perfil dos clusters, histogramas e boxplots).
- Interpretação detalhada dos clusters no corpo dos notebooks.
- HTMLs e PDF para consulta rápida.

## Troubleshooting
- Aviso de acessibilidade (alt text):
  - Nbconvert pode sinalizar imagens sem `alt`. A logo e os principais gráficos possuem/descrevem `alt`, mas se o aviso persistir, adicione `alt` às imagens renderizadas manualmente.
- Porta ocupada no servidor local:
  - Use outra porta: `python3 -m http.server 8001`.
- Pacotes faltando:
  - Reinstale: `pip install -r requirements.txt` e confira se o venv está ativo.
- Kaggle API:
  - Sem credenciais, copie os CSVs para `data/` e execute.
 - Logo grande/desproporcional:
   - O cabeçalho foi ajustado para não herdar estilos de H1. No primeiro bloco markdown do notebook, a imagem está fora do título e usa estilo inline:
     - `style="height: 100px; width: auto; vertical-align: middle;"`
     - Para alterar, ajuste apenas o `height` (ex.: 80px/120px) mantendo `width: auto` para preservar a proporção.

## Boas Práticas adotadas
- Preferência por soluções simples e sem duplicação de código.
- Consideração de ambientes (dev/test/prod); recomendação de centralizar configurações.
- Notebooks com interpretação clara e gráficos gerados de forma reprodutível.

## Roadmap e Próximos Passos
- Extrair rotinas de visualização para um módulo Python (ex.: `clusterizacao/viz.py`) e importar nos notebooks para reduzir duplicação e facilitar testes.
- Padronizar bloco de configuração (parâmetros de `k`, `random_state`, caminhos de saída) e permitir override por variável de ambiente (sem sobrescrever `.env`).
- Automatizar conversões (HTML/PDF) via `make html`/`make pdf` ou script `tasks.py`.
- Adicionar testes simples (ex.: validação de existência de colunas, shapes esperados e cálculo de médias por cluster).
- Incluir CI (ex.: GitHub Actions) para validar execução do notebook e geração de artefatos.

## Checklist de Submissão
- venv criado e ativado; dependências instaladas via `requirements.txt`.
- Notebook executado sem erros; gráficos gerados em `images/`.
- HTML gerado com `nbconvert` e validado no navegador.
- PDFs gerados (`Projeto_Clusterizacao.pdf` e/ou `Projeto_Clusterizacao2.pdf`) quando necessário.
- Avisos de acessibilidade (alt text) revisados; adicionar `alt` se aplicável.
- Commit das alterações com mensagem clara e organização da estrutura.

## Autor
- Fabio Ferreira Figueiredo — Repositório: `pd_algoritimos_clusterizacao`

---
Se precisar, eu ajusto o README para um template específico (acadêmico, empresarial, projeto de curso, etc.) ou crio um guia rápido separado (Quick Start) em `docs/`.