# Classificação do Sonar Dataset - Trabalho de Tópicos Especiais em Computação

Este projeto implementa uma análise comparativa entre algoritmos Multilayer Perceptron (MLP) e Support Vector Machine (SVM) para classificação do Sonar Dataset, considerando cenários com e sem Principal Component Analysis (PCA).

## Estrutura do Projeto

```
Trabalho_Topicos_7/
├── main.ipynb              # Notebook principal com implementação completa
├── relatorio.tex           # Relatório científico em LaTeX (template SBC)
├── sbc-template.sty        # Template LaTeX da SBC
├── README.md              # Este arquivo
└── dataset/               # Diretório dos dados (criado automaticamente)
    ├── sonar.all-data     # Dataset principal
    ├── sonar.mines        # Dados apenas de minas
    ├── sonar.rocks        # Dados apenas de rochas
    └── sonar.names        # Descrição do dataset
```

## Requisitos

### Software Necessário
- Python 3.8+
- Jupyter Notebook ou VS Code com extensão Python
- LaTeX (para compilar o relatório)

### Dependências Python
As dependências são instaladas automaticamente pelo notebook:
- pandas
- scikit-learn  
- numpy
- matplotlib
- seaborn

## Como Executar

### 1. Executar o Notebook

1. Abra o arquivo `main.ipynb` no VS Code ou Jupyter Notebook
2. Execute as células sequencialmente (Ctrl+Shift+P → "Run All Cells")
3. O notebook automaticamente:
   - Baixa e carrega o dataset do UCI
   - Processa e normaliza os dados
   - Executa busca de hiperparâmetros
   - Treina e avalia os modelos
   - Gera visualizações e comparações

### 2. Compilar o Relatório

Para compilar o relatório em LaTeX:

```bash
# Windows (PowerShell)
pdflatex relatorio.tex
bibtex relatorio
pdflatex relatorio.tex
pdflatex relatorio.tex

# Linux/macOS
pdflatex relatorio.tex && bibtex relatorio && pdflatex relatorio.tex && pdflatex relatorio.tex
```

## Metodologia Implementada

### Dataset
- **Origem**: UCI Machine Learning Repository
- **Tamanho**: 208 amostras, 60 atributos
- **Classes**: M (mina) e R (rocha)
- **Tipo**: Classificação binária

### Algoritmos Testados

#### 1. Multilayer Perceptron (MLP)
- Hiperparâmetros otimizados via Grid Search:
  - `hidden_layer_sizes`: (50,), (100,), (60,), (50,30), (100,50)
  - `alpha`: 0.0001, 0.001, 0.01, 0.1
  - `learning_rate_init`: 0.001, 0.01

#### 2. Support Vector Machine (SVM)
- Kernel RBF
- Hiperparâmetros otimizados:
  - `C`: 0.1, 1, 10, 100
  - `gamma`: 'scale', 'auto', 0.001, 0.01, 0.1, 1

### Cenários de Teste

1. **Sem PCA**: Usando todos os 60 atributos originais
2. **Com PCA**: Redução de dimensionalidade mantendo 95% da variância

### Validação

- **Divisão**: 80% treino/validação, 20% teste
- **Cross-validation**: Estratificada com k=5
- **Repetições**: 10 execuções independentes
- **Métricas**: Accuracy, Precision, Recall, F1-Score, Cohen's Kappa

## Resultados Esperados

O notebook produz:

1. **Análise exploratória** dos dados
2. **Visualizações do PCA** (variância explicada)
3. **Busca de hiperparâmetros** para cada algoritmo
4. **Tabela comparativa** de resultados
5. **Gráficos de desempenho** (boxplots)
6. **Análise estatística** dos melhores métodos

## Arquivos de Saída

Após a execução, você terá:
- Todos os resultados no notebook `main.ipynb`
- Relatório científico em `relatorio.pdf` (após compilação)
- Dataset baixado automaticamente em `dataset/`

## Interpretação dos Resultados

O projeto compara:
- **MLP vs SVM**: Qual algoritmo performa melhor
- **Com vs Sem PCA**: Impacto da redução de dimensionalidade
- **Estabilidade**: Variabilidade dos resultados (desvio padrão)
- **Significância**: Diferenças estatisticamente relevantes

## Troubleshooting

### Problemas Comuns

1. **Erro de importação**: Execute a primeira célula para instalar dependências
2. **Dataset não encontrado**: Verifique conexão com internet para download
3. **Memória insuficiente**: Reduza o número de experimentos (`NUM_TEST`)
4. **Compilação LaTeX**: Instale distribuição LaTeX completa (MiKTeX/TeX Live)

### Configurações Alternativas

Para executar mais rapidamente (desenvolvimento):
- Reduza `NUM_TEST` de 10 para 3
- Limite os parâmetros do Grid Search
- Use menos componentes PCA

## Contribuição

Este projeto foi desenvolvido como parte da disciplina Tópicos Especiais em Computação, implementando as melhores práticas de:
- Experimentação em Machine Learning
- Validação estatística robusta
- Documentação científica
- Reprodutibilidade

## Referências

- Gorman, R.P. and Sejnowski, T.J. (1988). Analysis of hidden units in a layered network trained to classify sonar targets.
- UCI Machine Learning Repository: Connectionist Bench (Sonar, Mines vs. Rocks)
- Scikit-learn documentation