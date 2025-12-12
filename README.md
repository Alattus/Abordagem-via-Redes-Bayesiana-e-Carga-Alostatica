Modelagem Preditiva de Comorbidades em Saude
Mental: Uma Abordagem via Redes Bayesianas e
Carga Alostatica
[README.md](https://github.com/user-attachments/files/24135993/README.md)

Leia o artigo completo [aqui](https://github.com/Alattus/AnaliseSobreUsoArvoresProbabilisticasnaSaudeMentalPreditiva./blob/main/main/Modelagem%20Preditiva%20de%20Comorbidades%20em%20Saude.pdf).


# Modelagem Preditiva de Comorbidades em Saúde Mental (MR-P)

Este repositório contém a implementação computacional do algoritmo de Mapeamento de Risco Preditivo (MR-P).  
O sistema utiliza Redes Bayesianas e a teoria da Carga Alostática para simular trajetórias de saúde mental, prevendo como condições neurobiológicas ("Raízes") interagem com estressores ambientais para gerar comorbidades secundárias ("Frutos").

O projeto fundamenta-se no Modelo Biopsicossocial (MBS), utilizando simulação estocástica para identificar vias de risco individualizadas.

---

## Estrutura do Projeto

O sistema é composto por três módulos principais:

### 1. main.py (Motor de Inferência Principal)
Contém:
- Bases de conhecimento embutidas (JSONs de Raízes, Fatores, Frutos e Dados Etários).
- Lógica de inferência Bayesiana para atualização de crenças.
- Cálculo do Fator de Influência da Idade (FIA).
- Algoritmo do Funil de Carga Alostática para predição de comorbidades.

Função:  
Simula um único sujeito, gera o cálculo probabilístico completo e exporta a estrutura da árvore resultante para `arvore.csv`.

### 2. visualizar_arvore.py (Gerador de Grafos)
Responsável pela representação gráfica dos dados.

Função:  
Lê o arquivo `arvore.csv` gerado pela main.py e plota a Árvore Probabilística destacando visualmente o Caminho Selecionado (a trajetória de maior risco).

### 3. gerar_coorte.py (Simulação Populacional)
Módulo para geração de dados em massa.

Função:  
Executa a lógica da main.py repetidamente para criar uma população sintética (por exemplo, N=700).  
Gera um dataset tabular `dataset_coorte.csv` utilizado para análises estatísticas e validação do modelo.

---

## Como Executar

### Pré-requisitos
- Python 3
- Dependências adicionais para visualização e análise de dados:

```
pip install matplotlib networkx pandas
```

---

### 1. Executar a Simulação Individual (main.py)

Ajuste as constantes no topo do arquivo:

```python
NIVEL_VULNERABILIDADE_FIXO = 3  # Escala 1-5
IDADE_SUJEITO_FIXA = 12
```

Execute:

```
python main.py
```

Saída:  
O terminal exibirá o log da simulação e o arquivo `arvore.csv` será criado.

---

### 2. Visualizar a Árvore (visualizar_arvore.py)

Após gerar o CSV:

```
python visualizar_arvore.py
```

Uma janela será aberta exibindo o grafo da árvore probabilística.

---

### 3. Gerar Dados para Estudo (gerar_coorte.py)

```
python gerar_coorte.py
```

---

## Estrutura do Arquivo arvore.csv

O arquivo contém colunas:

- **Nó_Principal**: origem da conexão  
- **Nome_Nó**: destino da conexão  
- **Valor**: peso da aresta (probabilidade ou score)  
- **Tipo**: categoria do nó  
- **Prior_Mod_Idade**: valor do ajuste temporal (FIA)  
- **Detalhes**: informações descritivas  

Inclui também uma linha especial de metadado onde `Nó_Principal = CAMINHO_SELECIONADO`, usada para destacar automaticamente a trajetória de maior risco.

---

## Lógica Teórica do Algoritmo

### Modulação Temporal (FIA)
Diagnósticos são ajustados conforme a idade do sujeito, penalizando combinações biologicamente improváveis.

### Carga Alostática
O risco é calculado de maneira não linear, somando desgaste de fatores biológicos e ambientais até ultrapassar um limiar de homeostase.

### Abordagem Híbrida
Combina inferência Bayesiana para diagnosticar a condição base com um modelo de score ponderado para predição de comorbidades futuras.

---

## Autoria

Desenvolvido no contexto de pesquisa acadêmica sobre Saúde Mental Preditiva, baseado no Modelo Biopsicossocial de George L. Engel e no conceito de Carga Alostática de Bruce McEwen.
