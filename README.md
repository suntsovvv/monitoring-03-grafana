# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Задание повышенной сложности

**При решении задания 1** не используйте директорию [help](./help) для сборки проекта. Самостоятельно разверните grafana, где в роли источника данных будет выступать prometheus, а сборщиком данных будет node-exporter:

- grafana;
- prometheus-server;
- prometheus node-exporter.

За дополнительными материалами можете обратиться в официальную документацию grafana и prometheus.

В решении к домашнему заданию также приведите все конфигурации, скрипты, манифесты, которые вы 
использовали в процессе решения задания.

**При решении задания 3** вы должны самостоятельно завести удобный для вас канал нотификации, например, Telegram или email, и отправить туда тестовые события.

В решении приведите скриншоты тестовых событий из каналов нотификаций.

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.
![image](https://github.com/suntsovvv/monitoring-03-grafana/assets/154943765/903049f1-2448-44a3-9501-2ab82c175db9)


## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.   

### утилизация CPU для nodeexporter:   

```
100 - (avg (rate(node_cpu_seconds_total{job=~"nodeexporter",mode="idle"}[1m])) * 100)
```
### CPULA 1/5/15:

```
avg(node_load1{job=~"nodeexporter"})
avg(node_load5{job=~"nodeexporter"})
avg(node_load15{job=~"nodeexporter"})
```

### количество свободной оперативной памяти:

```
node_memory_MemFree_bytes{job=~"nodeexporter"}
```

### количество места на файловой системе:

```
node_filesystem_avail_bytes{job=~"nodeexporter",mountpoint="/",fstype!="rootfs"}
```
![image](https://github.com/suntsovvv/monitoring-03-grafana/assets/154943765/26679954-73e3-4711-9945-5381d64ca0b1)


## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.
![image](https://github.com/suntsovvv/monitoring-03-grafana/assets/154943765/ac169d70-4a2a-4a32-9c2b-ad90b2f89e64)
Создал канал связи для Telegram.
Создал условия для сработки аллерта.
В телеграм пришло оповещение:
![image](https://github.com/suntsovvv/monitoring-03-grafana/assets/154943765/ddf558a3-d448-4b4a-ba61-fe4b699c0dd7)


## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.

      
[json](https://github.com/suntsovvv/monitoring-03-grafana/blob/main/json)





