# Лабораторная 4 — Генерация лиц CelebA (WGAN-GP, uncond + cond)

**Цель ТЗ:** WGAN/VAE на CelebA, безусловная + условная (по полу), FID + IS, детектор лица для препроцессинга.

## Подход

**WGAN-GP** 64×64, DCGAN-style. Critic со **spectral_norm** + **GroupNorm**. Conditional: **late conditioning**.

Препроцессинг: **MTCNN** для детекции лица.

FID считается на эмбеддингах Inception V3.

## Структура

```
lab4/
├── README.md
├── results.ipynb               # графики, метрики, демо
├── output/                     # результаты demo
└── v3/kaggle/                  # артефакты с Kaggle (датасет хранится на Kaggle)
    ├── lab4-kaggle-full.ipynb  # train-ноутбук, запускался на Kaggle
    └── release/lab4/
        ├── checkpoints/        # лучшие веса каждой модели
        ├── history/            # метрики обучения
        └── manifest.json
```

## Запуск

Открыть `results.ipynb` → Run All.

## Результаты

| Модель | FID ↓ | IS ↑ |
|---|---|---|
| unconditional | 57.69 | 2.227 ± 0.052 |
| **conditional_mixed** | **52.99** | 2.127 ± 0.061 |
| conditional_female | 57.84 | 2.044 ± 0.044 |
| **conditional_male** | **53.72** | 2.177 ± 0.057 |
