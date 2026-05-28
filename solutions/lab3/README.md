# Лабораторная 3 — Сегментация дорожных знаков + трекинг

**Цель ТЗ:** сегментация (single class) + сравнение BotSORT vs ByteTrack + прогон на собственных видео.

## Подход

**YOLO11n-seg** — single-class сегментация.
- VIA polygon-разметка → YOLO seg

Весь пайплайн построен на Ultralytics. BotSORT и ByteTrack идут с фреймворком из коробки.

Трекеры одной моделью отдают боксы: **BotSORT** (Kalman + ReID), **ByteTrack** (Kalman без ReID).

## Структура

```
lab3/
├── README.md
├── botsort.yaml, bytetrack.yaml  # конфиги трекеров
├── results.ipynb                 # графики, метрики, демо
├── input/                        # реальные данные для демо
├── output/                       # результаты demo
└── v3/kaggle/                    # артефакты с Kaggle (датасет хранится на Kaggle)
    ├── lab3-kaggle-full.ipynb    # train-ноутбук, запускался на Kaggle
    └── release/lab3/
        ├── checkpoints/          # лучшие веса каждой модели
        ├── history/              # метрики обучения
        └── manifest.json
```

## Запуск

Положить данные в `input/` → открыть `results.ipynb` → Run All.

## Результаты

| Метрика | Значение |
|---|---|
| box_mAP50 | 0.869 |
| mask_mAP50 | 0.815 |
| mean per-image IoU | 0.665 |
| frac IoU ≥ 0.5 | 0.756 |
| frac IoU ≥ 0.75 | 0.512 |

## Сравнение трекеров (3 видео ИТМО)

| Трекер | unique_ids | detections | fps | id_switches_approx |
|---|---|---|---|---|
| BotSORT | 64 | 7254 | 22.6 | 60 |
| ByteTrack | 64 | 7257 | 22.6 | 60 |
