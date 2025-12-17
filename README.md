# Trabalho Final FIA – LTNtorch (Raciocínio Espacial Neuro-Simbólico)

Implementação das Tarefas 1–4 do enunciado de FIA usando LTN em PyTorch, com cenário CLEVR simplificado (vetores 11-D). Notebook principal: `LTN_Tutorial_3oAssignment.ipynb`.

## O que foi feito
- Gerador de cenas CLEVR-like (25 objetos) com cores/formas/tamanho (small/medium/big) e relações espaciais (left/right, below/above, close, in_between, can_stack).
- Predicados neurais (MLPs) e conectivos/quantificadores fuzzy; axiomas de unicidade/cobertura, regras horizontais e verticais, consultas compostas e opcionais.
- Pipeline de treino maximizando satAgg, métricas (acc/prec/recall/F1) e explicações (nota extra).
- Célula de avaliação da imagem do grupo para testar a cena usada pelo professor.

## Dependências principais
- Python 3.13+, PyTorch CPU, TensorFlow (via `ltn`), pandas, scikit-learn, matplotlib, numpy.

## Como rodar
1. Abra `LTN_Tutorial_3oAssignment.ipynb` em Jupyter/Lab.
2. Rode as células na ordem:
   - Geração/plot de cena.
   - Treino e métricas (seed exemplo).
   - Experimentos 5× (seeds 0–4).
3. Para avaliar a imagem do grupo, use a seção “Avaliação da imagem do grupo” no final:
   - Edite `objects_manual` com `(id, x_grid, y_grid, cor, forma, size_scalar)` no grid 0–20.
   - Execute a célula: ela recalcula relações, treina e mostra satAgg, métricas, queries e explicações.

## Estrutura
- `LTN_Tutorial_3oAssignment.ipynb`: notebook completo com geração, axiomas, treino, métricas, consultas e avaliação de imagem.

## Observações
- Tamanho tratado em 3 classes: small (<1/3), medium (entre), big (>2/3), com `size_scalar` contínuo para regras de estabilidade/igualdade de tamanho.
- Ajuste `epochs` e `THRESH` no notebook conforme tempo/threshold desejados.

## Integrantes
- (preencher nomes dos alunos do grupo)