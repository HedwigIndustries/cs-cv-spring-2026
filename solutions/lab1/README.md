# Лабораторная 1 — Классификация цвета автомобиля (DVM)

**Цель ТЗ:** F1_macro > 0.8 на тесте DVM (11 цветов).

## Подход

Сравнение трёх моделей при IMG_SIZE=64 (гипотеза: для классификации цвета высокое разрешение не нужно):

1. **MyResNet** — свой ResNet с нуля
2. **ResNet18** — pretrained ImageNet, frozen backbone
3. **MobileNetV3-Small** — pretrained ImageNet, frozen backbone

Класс-баланс DVM сильно неравномерен (black/silver/white в десятки раз чаще orange/yellow) — обучение использует **WeightedRandomSampler** для равномерной частоты классов в батче.

## Структура

```
lab1/
├── README.md
├── results.ipynb               # графики, метрики, демо
├── input/                      # реальные данные для демо
└── v3/kaggle/                  # артефакты с Kaggle (датасет хранится на Kaggle)
    ├── lab1-kaggle-full.ipynb  # train-ноутбук, запускался на Kaggle
    └── release/lab1/
        ├── checkpoints/        # лучшие веса каждой модели
        ├── history/            # метрики обучения
        └── manifest.json
```

## Запуск

Положить данные в `input/` → открыть `results.ipynb` → Run All.

## Результаты


| Модель                     | Best F1_macro | Precision | Recall |
| -------------------------- | ------------- | --------- | ------ |
| **MyResNet** (scratch)     | **0.814**     | 0.831     | 0.804  |
| ResNet18 (frozen)          | 0.519         | 0.502     | 0.584  |
| MobileNetV3-Small (frozen) | 0.416         | 0.402     | 0.488  |


