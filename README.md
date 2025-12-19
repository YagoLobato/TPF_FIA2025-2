# 3º Trabalho — LTN / Neuro-Symbolic (FIA)

Implementação de um sistema **Neuro-Simbólico (NeSy)** usando **Logic Tensor Networks (LTN)** para raciocínio com **lógica fuzzy** sobre um **dataset estilo CLEVR simplificado** (objetos 2D com cor, forma, tamanho e relações espaciais). O repositório foi organizado para seguir o formato de entrega pedido no enunciado: **código + texto no GitHub** (via notebook) + **resultados experimentais (5 execuções)** + **ponto extra de explicações**.

---

## ✅ Entregas

No notebook final (`LTN_Tutorial_3oAssignment.ipynb`) você encontra:

1. **Texto**: introdução a **NeSy** e **LTN**
2. **Dataset**: inspiração no **CLEVR** e descrição da versão simplificada usada (vetor 11D)
3. **Satisfação**: valor de satisfação das **fórmulas específicas** no **conjunto de teste** (inclui tabela “sat por fórmula”)
4. **Experimentos**: resultados para **5 execuções** (5 datasets aleatórios distintos), com:

   * **satAgg de cada pergunta e fórmula**
   * **Acurácia, Precisão, Recall e F1**
5. **Ponto extra**: **explicação** de cada resposta (raciocínio em linguagem natural a partir das regras e scores)

---

## 🧠 Visão geral da solução

### Dataset (CLEVR simplificado)

Cada objeto é representado por um vetor **11D**:

| Campo              | Dimensão | Descrição                                      |
| ------------------ | -------- | ---------------------------------------------- |
| `pos_x`, `pos_y`   | 2        | posição no plano (normalizada)                 |
| `colors` (one-hot) | 3        | {vermelho, verde, azul}                        |
| `shapes` (one-hot) | 5        | {circulo, quadrado, cilindro, cone, triangulo} |
| `size`             | 1        | escalar em [0,1] (pequeno/grande)              |

### Predicados e regras

* Predicados **treináveis via redes neurais (MLPs)**:

  * **unários**: atributos (cor/forma/tamanho)
  * **binários**: relações (left/right/below/above/close/same_size/can_stack)
  * **ternário**: `in_between`
* Axiomas das tarefas:

  * **T1**: cobertura/exclusividade de forma + consistência pequeno/grande
  * **T2**: raciocínio horizontal (irreflexivo, assimetria, inversos, transitividade, etc.)
  * **T3**: raciocínio vertical + inverso + transitividade + `can_stack`
  * **T4**: consultas (queries) e regra de proximidade
  * Inclui também `lastOnTheLeft` e `lastOnTheRight`.

### Treinamento

O treino otimiza a satisfação de uma **KB (knowledge base)** via agregação `SatAgg`, com backprop (ex.: Adam). Os experimentos repetem o pipeline completo para **5 seeds** (5 datasets aleatórios).

---

## 📂 Arquivos

* `LTN_Tutorial_3oAssignment.ipynb`

  * ✅ Notebook final no formato exigido (seções 1–5, métricas, tabelas, explicações)

---

## 🧪 O que o notebook imprime (resultados)

### 1) Tabela com 5 execuções (5 seeds)

Inclui:

* `sat_test`, `sat_manual`
* consultas `q1/q2/q3` (teste e manual)
* `F1` das relações: `left`, `right`, `in_between`, `can_stack`
* `acc_shape`, `acc_size`

E um resumo **média ± desvio** para as métricas principais.

### 2) Satisfação por fórmula (seed 0)

Tabela com a satisfação individual dos axiomas no **teste** e no **manual**, incluindo:

* fórmulas T1, T2, T3
* `lastOnTheLeft` / `lastOnTheRight`

### 3) Ponto extra — explicações

Para as consultas (ex.: Q1 e Q2), o notebook:

* seleciona o **melhor grounding** (quais objetos maximizam o `Exists`)
* mostra **tabela de objetos** + **tabela de scores**
* gera **explicação em linguagem natural**, destacando o literal “gargalo” que mais derruba a consulta

---

## 🧭 Mapa do notebook (onde está cada item pedido)

* **1 — NeSy e LTN**
* **2 — CLEVR e dataset simplificado (11D)**
* **3 — Predicados, conectivos e axiomas**
* **4 — Entregas e experimentos**
  * 4.1 Satisfação das fórmulas no teste
  * 4.2 Métricas (acc/prec/recall/F1)
  * 4.3 5 execuções + média±desvio + sat por fórmula
* **5 — Ponto extra: explicações**
---

## ✍️ Equipe

- Yago Lobato — yagobrlobato@icomp.ufam.edu.br  
- Nathã Barbosa — NathaBarbosa@icomp.ufam.edu.br  
- Matheus Santarém — matheus.santarem@icomp.ufam.edu.br  
- Emanuel Andriola — Emanuel.moraes@icomp.ufam.edu.br  
- Daniel Trindade — daniel.trindade@icomp.ufam.edu.br  
- Cristiano Cardoso — cristiano.lima@icomp.ufam.edu.br
