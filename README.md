# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Устинов Никита Валерьевич
- РИ-210910
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Выводы.
- ✨Magic ✨

## Цель работы
Интегрировать экономическую систему в проект Unity и обучение ML-Agent

## Задание 1 
### Составить рабочий макет по методичке. Ознакомиться с его работой

Ход работы:

Установил компоненты для работы MLAgent, запустил сцену

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_1.png)

По завершении обучения получил результат

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_gif.gif)

получил yaml-файл с содержанием

```
default_settings: null
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 0.0003
      beta: 0.01
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3
      learning_rate_schedule: linear
      beta_schedule: linear
      epsilon_schedule: linear
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
      vis_encode_type: simple
      memory: null
      goal_conditioning_type: hyper
      deterministic: false
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
        network_settings:
          normalize: false
          hidden_units: 128
          num_layers: 2
          vis_encode_type: simple
          memory: null
          goal_conditioning_type: hyper
          deterministic: false
    init_path: null
    keep_checkpoints: 5
    checkpoint_interval: 500000
    max_steps: 750000
    time_horizon: 64
    summary_freq: 5000
    threaded: false
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      window: 10
      play_against_latest_model_ratio: 0.5
      initial_elo: 1200.0
    behavioral_cloning: null
env_settings:
  env_path: null
  env_args: null
  base_port: 5005
  num_envs: 1
  num_areas: 1
  seed: -1
  max_lifetime_restarts: 10
  restarts_rate_limit_n: 1
  restarts_rate_limit_period_s: 60
engine_settings:
  width: 84
  height: 84
  quality_level: 5
  time_scale: 20
  target_frame_rate: -1
  capture_frame_rate: 60
  no_graphics: false
environment_parameters: null
checkpoint_settings:
  run_id: Economic
  initialize_from: null
  load_model: false
  resume: false
  force: true
  train_model: false
  inference: false
  results_dir: results
torch_settings:
  device: null
debug: false
```

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_2.png)

получил графики
## Задание 2
### Изменить параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели

Ход работы:

Изменил 7 параметров из yaml-файла

1) изменение параметра **beta** с 1.0e-2 до 1.0e-9

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_beta.png)

2) изменил параметр **epsilon** с 0.2 до 0.9

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_epsilon.png)

3) изменил параметр **lambda** с 0.2 до 0.9

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_lambda.png)

4) изменил параметр **num_epoch** с 3 до 60

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_num_epoch.png)

5) изменил параметр **gamma** с 0.99 до 0.01

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_gamma.png)

6) изменил параметр **learning_rate** с 3.0e-4 до 3.0e-20. Результаты обучения были непостоянными: после роста значения на одной итерации, оно падало на другой. Было принято решение закончить обучение при получении максимальной награды на итерации

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_learning_rate.png)

7) изменил параметр **strength** с 1.0 до 0.5. Результаты обучение показывали, что модель получала максимум награды после первого эпизода обучения, но продолжило обучение дальше, поэтому прервал обучение, т.к. результат не изменялся

![Image alt](https://github.com/GreatSherhebe1/UrFU_labaratory_Lab-5/raw/main/Лаба5_скрины/Laba5_strength.png)

## Задание 3
### Описать результаты, выведенные в TensorBoard

## Выводы

