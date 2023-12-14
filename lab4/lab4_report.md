University: [ITMO University](https://itmo.ru/ru/) \
Faculty: [FICT](https://fict.itmo.ru) \
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies) \
Year: 2023/2024\
Group: K4112C\
Author: Kuznetsov Vyacheslav Sergeevich \
Lab: Lab4 \
Date of create: 14.12.2023 \
Date of finished:   \

# Лабораторная работа №4 "Сети связи в Minikube, CNI и CoreDNS"

### Цель работы
Познакомиться с CNI Calico и функцией IPAM Plugin, изучить особенности работы CNI и CoreDNS

# Ход работы

## 1. Запуск Minikube с плагином Calico:
В командной строке запускаем ноду с плагином Calico:

![start](img/1.PNG) 

## 2. Добавление ноды:
С помощью команды `minikube node add` создаем дополнительную рабочую ноду и проверяем результат с помощью `kubectl get nodes`:

![node](img/2.PNG) 

## 3. Проверим поды Calico:
Для этого используем команду `kubectl get pods --namespace=kube-system`:

![calico](img/3.PNG) 


## 4. Настройка сервиса:
- Установим `calicoctl`:

![calicoctl](img/5.PNG)

- Установим `label` для запущенных нод:

![label](img/4.PNG)

- создадим config-файл  ![calico.config.yaml](https://github.com/vkuznetsoff/2023_2024-introduction_to_distributed_technologies-k4112c-kuznetsov_v_s/blob/main/lab4/calico.config.yaml)  для `CalicoAPIConfig`:

![config](img/7.PNG)

- используем ![манифест](https://github.com/vkuznetsoff/2023_2024-introduction_to_distributed_technologies-k4112c-kuznetsov_v_s/blob/main/lab4/ippool.yaml) для запуска Calico:
![ippool](img/8.PNG)

- создаем ![ConfigMap](https://github.com/vkuznetsoff/2023_2024-introduction_to_distributed_technologies-k4112c-kuznetsov_v_s/blob/main/lab4/config.map.yaml) с переменными, манифест для ![Deployment](https://github.com/vkuznetsoff/2023_2024-introduction_to_distributed_technologies-k4112c-kuznetsov_v_s/blob/main/lab4/deployment.yaml) и ![сервиса](https://github.com/vkuznetsoff/2023_2024-introduction_to_distributed_technologies-k4112c-kuznetsov_v_s/blob/main/lab4/service.yaml).

Разворачиваем все это:

![deployment](img/9.PNG)

## 6. Проверим созданные поды:

![pods](img/10.PNG)

## 7. Посмотрим, что все создано:
![all](img/11.PNG)

## 8. Запустим сервис на локальном компьютере:
` minikube kubectl -- port-forward service/lab4 3000:3000`

![lochost](img/13.PNG)

## 9. Проверим как пингуется соседняя пода:
` kubectl exec -it pods/lab4-57d4cbd7fd-r6rrt ping 10.244.0.72`

![ping](img/12.PNG)

## 10. Схема организации контейеров и сервисов:

![scheme](img/14.PNG)








