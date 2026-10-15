🇧🇷 Português · 🇺🇸 [English summary](#english-summary)

# Edge AI no Raspberry Pi Zero 2 W — Classificação de Imagens & Detecção de Objetos

Projeto da disciplina **IESTI05 – Machine Learning System Engineering** (UNIFEI), sob
orientação do Prof. Marcelo Rovai ([@Mjrovai](https://github.com/Mjrovai)). Dois pipelines de
Edge AI, dda coleta do dataset à inferência em um **Raspberry Pi Zero 2 W** (~415 MB de RAM
utilizável), com modelos treinados no Edge Impulse e executados com `ai_edge_litert`.

## Estrutura

```
IMG_CLASS/                                  # classificação de imagens
├── 30_Image_Classification_edge_impulse.ipynb   # inferência e comparação INT8 vs. Float32
├── get_img_data.py                         # app Flask para capturar o dataset com a câmera
└── models/                                 # modelos exportados: float32 e INT8
OBJ_DETECT/                                 # detecção de objetos
├── EI-SSD-MobileNetV2.ipynb                # inferência do modelo próprio (mugs e glasses) com NMS
├── get_img_data.py                         # app Flask para capturar o dataset com a câmera
├── images/                                 # imagens de teste
└── models/                                 # modelos exportados: float32 e INT8
```

## Classificação de Imagens (`IMG_CLASS/`)

Modelo de 3 classes (folha, óculos, background), transfer learning sobre **MobileNetV2**
(α=1.0, entrada 160×160) no Edge Impulse. O dataset (200 amostras) foi capturado com a câmera
da própria Pi por um app Flask (`get_img_data.py`). Os modelos exportados para TensorFlow Lite
foram executados na Pi Zero 2 W com `ai_edge_litert`, comparando **INT8 Quantized** vs.
**Float32 Unoptimized**. Acurácia do modelo float32: 96,9% na validação e 90,0% no teste.

| Modelo | Tamanho | Inferência na Pi Zero 2 W |
|---|---|---|
| Float32 | 8,8 MB | ~94 ms |
| INT8 | 2,7 MB | ~65 ms |

A quantização INT8 deixou o modelo ~3× menor e a inferência ~30% mais rápida, mantendo as
mesmas previsões do float32 nas imagens testadas no notebook.

🔗 Projeto no Edge Impulse: https://studio.edgeimpulse.com/public/1108983/live

## Detecção de Objetos (`OBJ_DETECT/`)

Modelo próprio para as classes **mugs** e **glasses**: 190 imagens capturadas e anotadas manualmente no
Roboflow, split 80/10/10 e augmentation (3x no treino). Modelo  **MobileNetV2 SSD FPN-Lite** (entrada 320×320)
treinado no Edge Impulse  e
exportado em float32 e INT8, com Non-Maximum Suppression implementado no pós-processamento das detecções. Acurácia de 72% no teste (float32).

| Modelo | Tamanho | Inferência na Pi Zero 2 W |
|---|---|---|
| Float32 | 11 MB | — |
| INT8 | 3,3 MB | ~370–390 ms |

O INT8 ficou ~3,3× menor que o float32 e roda na Pi Zero 2 W em ~370–390 ms por imagem. A
classe `glasses` foi mais desafiadora que `mugs`, provavelmente pela transparência das lentes.

🔗 Projeto no Edge Impulse: https://studio.edgeimpulse.com/public/1118984/live

## Ambiente

Raspberry Pi Zero 2 W + câmera · Python (`ai-edge-litert`, `opencv-python`, `picamera2`,`matplotlib`,
`pillow`, `numpy`) · Jupyter Notebook

## Créditos

Material didático e templates de código-base do Prof. Marcelo Rovai
([@Mjrovai](https://github.com/Mjrovai)), disciplina IESTI05 — UNIFEI.

## Autora

Mel Cabral Fiore Brito — Engenharia de Computação, UNIFEI

---

<a name="english-summary"></a>

## English summary

Edge AI project for **IESTI05 – Machine Learning System Engineering** (UNIFEI), under Prof.
Marcelo Rovai ([@Mjrovai](https://github.com/Mjrovai)). Two pipelines running on a
**Raspberry Pi Zero 2 W**, trained on Edge Impulse and deployed with `ai_edge_litert`:

- **Image Classification** (`IMG_CLASS/`): 3-class model (leaf, glasses, background) via Edge Impulse, comparing INT8 vs. Float32.
  🔗 https://studio.edgeimpulse.com/public/1108983/live
- **Object Detection** (`OBJ_DETECT/`): custom mugs/glasses detector (Roboflow annotation + Edge Impulse, MobileNetV2 SSD FPN-Lite) with a custom NMS.
  🔗 https://studio.edgeimpulse.com/public/1118984/live

Course materials and base code templates by Prof. Marcelo Rovai
([@Mjrovai](https://github.com/Mjrovai)).
