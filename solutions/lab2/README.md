# Лабораторная 2 — Детекция номеров (SVHN + NumberDetection pretrain)

**Цель ТЗ:** mAP@50 ≥ 0.6 на SVHN test + прогон на 5-10 собственных уличных фото.

## Подход

Требуется детектировать номер как целое, а не отдельные цифры — поэтому многобоксовая разметка SVHN мерджится в один общий bbox на изображение, и задача сводится к single-class детекции.

Весь пайплайн построен на Ultralytics.

3-стадийный pipeline на **YOLOv8n**:

1. **baseline:** yolov8n.pt (COCO) → SVHN
2. **pretrain:** yolov8n.pt (COCO) → NumberDetection
3. **with_pretrain:** pretrain best → SVHN

## Структура

```
lab2/
├── README.md
├── results.ipynb               # графики, метрики, демо
├── input/                      # реальные данные для демо
└── v3/kaggle/                  # артефакты с Kaggle (датасет хранится на Kaggle)
    ├── lab2-kaggle-full.ipynb  # train-ноутбук, запускался на Kaggle
    └── release/lab2/
        ├── checkpoints/        # лучшие веса каждой модели
        ├── history/            # метрики обучения
        └── manifest.json
```

## Запуск

Положить данные в `input/` → открыть `results.ipynb` → Run All.

## Результаты

| Стадия | mAP@50 | Precision | Recall |
|---|---|---|---|
| baseline | 0.863 | 0.800 | 0.833 |
| **with_pretrain** | **0.877** | 0.824 | 0.840 |
