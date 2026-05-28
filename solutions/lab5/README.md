# Лабораторная 5 — LoRA DreamBooth для Stable Diffusion 1.5

**Цель ТЗ:** дообучить SD1.5 на своих фото через LoRA, сгенерировать 5 креативных портретов, оценить **CLIP-T / CLIP-I / Sharpness** (НЕ FID/IS).

## Подход

**SD1.5 + LoRA r=16, alpha=16** на attention-слоях UNet:

- Instance prompt: `a photo of ohwx man`
- **Class prior preservation:** параллельно instance loss считаем class loss на generic `a photo of a man`

Стек — diffusers + peft + transformers. VAE и CLIP text-encoder из SD1.5 заморожены, обучается только LoRA-адаптер на UNet.

15 промптов: 4 ohwx + 4 control + 2 name-test + **5 креативных**.

## Структура

```
lab5/
├── README.md
├── results.ipynb               # графики, метрики, демо
├── input/                      # реальные данные для демо
├── output/                     # результаты demo
└── v3/kaggle/                  # артефакты с Kaggle (датасет хранится на Kaggle)
    ├── lab5-kaggle-full.ipynb  # train-ноутбук, запускался на Kaggle
    └── release/lab5/
        ├── checkpoints/        # лучшие веса каждой модели
        ├── history/            # метрики обучения
        └── manifest.json
```

## Запуск

Положить данные в `input/` → открыть `results.ipynb` → Run All.

## Результаты


| Группа                | CLIP-T | CLIP-I    | Sharpness |
| --------------------- | ------ | --------- | --------- |
| **ohwx**              | 0.316  | **0.615** | 318       |
| control               | 0.301  | 0.472     | 981       |
| name (Rustam Kadyrov) | 0.371  | 0.545     | 2675      |
| creative              | 0.339  | 0.529     | 1104      |


**Δ CLIP-I (ohwx − control) = +0.143**