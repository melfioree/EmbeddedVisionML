🇧🇷 Português · 🇺🇸 [English summary](#english-summary)

# Edge AI no Raspberry Pi Zero 2 W — Classificação de Imagens & Detecção de Objetos

Projeto da disciplina **IESTI05 – Machine Learning System Engineering** (UNIFEI), sob
orientação do Prof. Marcelo Rovai ([@Mjrovai](https://github.com/Mjrovai)). Dois pipelines de
Edge AI, do dataset ao deploy em tempo real, rodando em um **Raspberry Pi Zero 2 W**.

## Estrutura

```
IMG_CLASS/      # classificação de imagens
OBJ_DETECT/     # detecção de objetos
```

## Classificação de Imagens (`IMG_CLASS/`)

Modelo de 3 classes (folha, óculos, background), transfer learning via Edge Impulse, comparando
INT8 Quantized vs. Float32 Unoptimized. Acurácia de 90%; a quantização INT8 reduziu o tempo de
inferência em ~30% (65 ms vs. 94 ms) sem perda relevante de precisão.

🔗 Projeto no Edge Impulse: https://studio.edgeimpulse.com/public/1108983/live

## Detecção de Objetos (`OBJ_DETECT/`)

Exploração inicial com um SSD-MobileNet V1 pré-treinado (COCO), seguida de um modelo próprio
para as classes **mugs** e **glasses**: 190 imagens capturadas e anotadas manualmente no
Roboflow, split 80/10/10 e augmentation (3x no treino). Modelo MobileNetV2 SSD FPN-Lite
treinado no Edge Impulse, com Non-Maximum Suppression implementado no pós-processamento das
detecções. A classe `glasses` foi mais desafiadora que `mugs`, provavelmente pela transparência
das lentes.

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
Marcelo Rovai ([@Mjrovai](https://github.com/Mjrovai)). Two pipelines deployed in real time on a
**Raspberry Pi Zero 2 W**:

- **Image Classification** (`IMG_CLASS/`): 3-class model (leaf, glasses, background) via Edge
  Impulse, comparing INT8 vs. Float32.
  🔗 https://studio.edgeimpulse.com/public/1108983/live
- **Object Detection** (`OBJ_DETECT/`): custom mugs/glasses detector (Roboflow annotation +
  Edge Impulse, MobileNetV2 SSD FPN-Lite) with a custom NMS implementation.
  🔗 https://studio.edgeimpulse.com/public/1118984/live

Course materials and base code templates by Prof. Marcelo Rovai
([@Mjrovai](https://github.com/Mjrovai)).
