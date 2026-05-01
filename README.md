# 🐾 Classificação de Imagens com CNN — Cachorros vs. Gatos

Este projeto foi desenvolvido como atividade extra da disciplina de Inteligência Artificial / Deep Learning. O objetivo é construir e treinar uma **Rede Neural Convolucional (CNN)** capaz de classificar imagens de cachorros e gatos utilizando Python, TensorFlow/Keras e Google Colab.

---

## 📌 Descrição do Projeto

O modelo recebe como entrada imagens de cachorros ou gatos e retorna a classe prevista junto com o grau de confiança da predição. Todo o pipeline — desde a preparação dos dados até a avaliação final — está implementado no notebook `Deep_learning.ipynb`.

---

## 🗂️ Estrutura do Notebook

| Etapa | Descrição |
|-------|-----------|
| **Etapa 0** | Importação de bibliotecas e seleção das imagens válidas |
| **Etapa 1** | Pré-processamento e Data Augmentation |
| **Etapa 2** | Construção, compilação e treinamento da CNN |
| **Etapa 3** | Avaliação do modelo no conjunto de teste |
| **Testes**  | Predição em imagens individuais |

---

## 📦 Dataset

- **Fonte:** [Microsoft Cats vs Dogs Dataset](https://www.microsoft.com/en-us/download/details.aspx?id=54765)
- **Seleção:** 1 000 imagens válidas de gatos + 1 000 de cachorros (total de 2 000 imagens)
- **Divisão:**
  - 70% → Treinamento
  - 15% → Validação
  - 15% → Teste

> Imagens corrompidas são automaticamente descartadas durante a seleção.

---

## ⚙️ Pré-processamento

- Redimensionamento para **150 × 150** pixels
- Normalização dos valores dos pixels para o intervalo **[0, 1]**
- **Data Augmentation** (apenas no treino):
  - Rotação aleatória (até 20°)
  - Zoom aleatório (até 20%)
  - Espelhamento horizontal

---

## 🧠 Arquitetura da CNN

```
Input (150, 150, 3)
│
├── Conv2D(32, 3×3, ReLU) → MaxPooling2D(2×2)
├── Conv2D(64, 3×3, ReLU) → MaxPooling2D(2×2)
├── Conv2D(128, 3×3, ReLU) → MaxPooling2D(2×2)
│
├── Flatten
├── Dense(128, ReLU) → Dropout
└── Dense(1, Sigmoid)   ← saída binária
```

- **Otimizador:** Adam (lr = 0,0001)
- **Função de perda:** Binary Crossentropy
- **Métrica:** Acurácia

---

## 🏋️ Treinamento

- Até **20 épocas**
- **EarlyStopping** com `patience=5` monitorando a `val_loss`
  - Interrompe o treinamento antecipadamente se não houver melhora
  - Restaura automaticamente os melhores pesos

---

## 📊 Avaliação

O modelo é avaliado no conjunto de teste com as seguintes métricas:

- **Acurácia**
- **Precisão (Precision)**
- **Revocação (Recall)**
- **F1-Score**

Gráficos de acurácia e perda ao longo das épocas são gerados para análise do comportamento durante o treinamento.

---

## 🔍 Exemplo de Predição

```python
predict_image("meu_cachorro.jpg")
# → Predição: Dog (97.43%)

predict_image("meu_gato.jpg")
# → Predição: Cat (94.11%)
```

---

## 🛠️ Tecnologias Utilizadas

- Python 3
- TensorFlow / Keras
- NumPy
- Pillow (PIL)
- scikit-learn
- Matplotlib
- Google Colab + Google Drive

---

## 🚀 Como Executar

1. Faça o upload do notebook `Deep_learning.ipynb` no [Google Colab](https://colab.research.google.com/).
2. Monte seu Google Drive e certifique-se de que o dataset está disponível em:
   ```
   /content/drive/MyDrive/datasets/Pet_Images/
   ├── Cats/
   └── Dogs/
   ```
3. Execute as células em ordem sequencial.

---

## 👤 Autor

Desenvolvido por **Vitor Rodrigues Dan** como atividade extra da disciplina de IA / Deep Learning.
