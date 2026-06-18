# 🐈‍⬛ A/B тест Cookie Cats — анализ влияния ворот на удержание игроков

![Статус](https://img.shields.io/badge/Завершён-fe8616?style=flat-square&labelColor=2d2d2d)
![Python](https://img.shields.io/badge/Python-bdf522?style=flat-square&labelColor=2d2d2d)
![A/B тест](https://img.shields.io/badge/A%2FB_тест-7b46f8?style=flat-square&labelColor=2d2d2d)
![EDA](https://img.shields.io/badge/EDA-fa51a2?style=flat-square&labelColor=2d2d2d)


## О проекте
 
**Cookie Cats** — мобильная игра-головоломка в жанре «три в ряд». В ней есть **ворота** — точки, где игрок вынужден сделать паузу (подождать или совершить покупку).

Команда разработчиков рассматривает перемещение ворот с 30-го на 40-й уровень, был проведен A/B тест: части новых пользователей ворота ставили на 30-й уровень, а остальным - на 40.

Цель анализа — оценить, как это скажется на суммарном количестве сыгранных раундов за 14 дней, ретеншне первого дня и ретеншне седьмого дня.

## Ключевые результаты

| Метрика | gate_30 | gate_40 | p-value |
|---|---|---|---|
| Ретеншн 1 день | 44.82% | 44.23% | > 0.05 |
| Ретеншн 7 день | 19.02% | 18.20% | > 0.05 |
| Медиана раундов | 17 | 16 | > 0.05 |

💜 Статистически значимых различий между группами не обнаружено ни по одной метрике.

💛 Менее трети пользователей вообще доходит до ворот на 30 уровне.

💚 Рекомендовано оставить ворота на 30 уровне и улучшить онбординг.

## Стек
 
`pandas` · `numpy` · `matplotlib` · `seaborn` · `scipy.stats` · `Jupyter Notebook`
 
## Структура репозитория
 
```
cookie_cats_ab_test/
├── README.md
├── data/
│   └── cookie_cats.csv        # датасет (Kaggle, открытый доступ)
├── notebooks/
│   └── data_analysis.ipynb    # основной анализ
└── requirements.txt
```

## Данные
 
Датасет [`cookie_cats.csv`](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats/data) — открытый доступ, Kaggle.
 
| Поле | Описание |
|---|---|
| `userid` | Уникальный ID игрока |
| `version` | Группа: `gate_30` или `gate_40` |
| `sum_gamerounds` | Кол-во раундов за 14 дней после установки |
| `retention_1` | Вернулся ли игрок на следующий день |
| `retention_7` | Вернулся ли игрок через неделю |
 
  
## Методология
 
1. **Предобработка** — проверка пропусков, дублей, выбросов
2. **EDA** — анализ состава групп, распределения раундов и ретеншна по группам
3. **Статистические тесты:**
   - `sum_gamerounds` → U-критерий Манна-Уитни (ненормальное распределение, тяжёлый хвост) + вероятность превосходства
   - `retention_1`, `retention_7` → критерий χ² Пирсона + коэффициент Крамера


## Запуск
 
```bash
git clone https://github.com/FragileMouse/Mobile_Games_A-B_Testing_Cookie_Cats.git
cd Mobile_Games_A-B_Testing_Cookie_Cats
pip install -r requirements.txt
jupyter notebook notebooks/data_analysis.ipynb
```
 
 
## Автор
 
**Анастасия Солдатова** · [github.com/FragileMouse](https://github.com/FragileMouse)
 
