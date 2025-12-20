# Caixaverso
# 🛡️ Detecção de Fraude em Cartões de Crédito

> **Status do Projeto:** ✅ Concluído (Aprovado com Excelência)

Este projeto apresenta uma solução completa de Machine Learning para identificar transações financeiras fraudulentas. O foco central foi resolver o problema do **desbalanceamento extremo de classes** maximizando a detecção de fraudes (Recall) sem prejudicar a experiência de clientes legítimos.

---

## 💼 1. O Problema de Negócio
A fraude em cartões de crédito gera prejuízos bilionários anuais. Para uma instituição financeira, o desafio é duplo:
1.  **Detectar a Fraude (Evitar Prejuízo):** Bloquear compras ilegítimas.
2.  **Evitar Fricção (Experiência do Cliente):** Não bloquear compras legítimas (Falsos Positivos).

**O Desafio dos Dados:**
O dataset utilizado contém transações onde **menos de 1% são fraudes**. Modelos tradicionais falham nesse cenário, pois tendem a alcançar 99% de acurácia apenas dizendo que "tudo é legítimo", ignorando o crime.

---

## 🛠️ 2. Estratégia da Solução
A solução foi desenvolvida em Python seguindo um pipeline rigoroso de Ciência de Dados:

### 🔹 Pipeline e Prevenção de Data Leakage
Utilizamos `IMBLEARN Pipelines` para garantir que o pré-processamento (OneHotEncoding, Scaling) e as técnicas de balanceamento fossem aplicadas corretamente dentro da validação cruzada, evitando vazamento de dados do treino para o teste.

### 🔹 Modelagem e Comparação
Testamos diferentes arquiteturas para entender qual se adaptava melhor à complexidade dos dados:
* **KNN (K-Nearest Neighbors):** Baseline baseada em distância.
* **Random Forest:** Modelo de *Bagging* robusto.
* **XGBoost (Campeão):** Modelo de *Gradient Boosting* otimizado.

### 🔹 Estratégia de Balanceamento
Evoluímos de uma abordagem de **Undersampling** (rápida para testes) para o uso de **Class Weights (scale_pos_weight)** no modelo final. Isso permitiu treinar o modelo com **todos os dados disponíveis**, penalizando erros na classe minoritária (fraude) sem descartar informações valiosas.

---

## 📊 3. Resultados Obtidos
O modelo final (XGBoost Otimizado) apresentou performance superior, validada via **RandomizedSearchCV**:

| Métrica | Resultado | Interpretação |
| :--- | :--- | :--- |
| **AUC-ROC** | **~0.98** | Excelente capacidade de separação entre fraude e não-fraude. |
| **Otimização** | `max_depth=6` | Profundidade controlada para evitar *Overfitting*. |

> **Nota:** Optamos pela métrica AUC-ROC ao invés da Acurácia, pois em dados desbalanceados a acurácia é uma métrica enganosa.

---

## 🧠 4. Explicabilidade (SHAP Values)
Não basta prever, é preciso explicar. Utilizamos **SHAP (SHapley Additive exPlanations)** para abrir a "caixa preta" do modelo.
* **Insight:** O modelo identificou que o valor da transação (`amt`) e a categoria de compra são os maiores preditores de risco, alinhando-se com a intuição de negócio.

<img width="780" height="940" alt="image" src="https://github.com/user-attachments/assets/a239f1ac-c2f6-407b-97ca-ac7e6c80e4bb" />


---

## 🚀 5. Como Executar o Projeto

### Pré-requisitos
* Python 3.8+
* Jupyter Notebook

### Passo a Passo
1. Clone o repositório:
   ```bash
   git clone [https://github.com/SEU_USUARIO/NOME_DO_REPO.git](https://github.com/SEU_USUARIO/NOME_DO_REPO.git)
