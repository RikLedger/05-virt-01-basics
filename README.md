# Домашнее задание к занятию "1. Введение в виртуализацию. Типы и функции гипервизоров. Обзор рынка вендоров и областей применения." `Горбачев Олег`

## Задача 1

### *Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.*

* Полная виртуализация подразумевает абсолютный отказ от хостовой ОС и представляет собой набор инструкций, которые добавлены в центральный процессор и обеспечивают соответствующее разграничение ресурсов системы.

* Говорить о паравиртуализации можно, когда гипервизор устанавливается на хостовую ОС, является надстройкой над ней и осуществляет выделение гостевым ОС резурсов системы

* При виртуализации уровня ОС сама ОС и выполняет функции гипервизора. На ней запускаются изолированные ОС - контейнеры.

## Задача 2

### *Выберите один из вариантов использования организации физических серверов, в зависимости от условий использования.*

Организация серверов:
- физические сервера, 
- паравиртуализация,
- виртуализация уровня ОС.

Условия использования:
- Высоконагруженная база данных, чувствительная к отказу - *Тут требуется высокая производительность. Следовательно, важно оптимально расходовать ресурсы системы. Этого можно добиться при использовании физических серверов или виртуализации уровня ОС. Но в случае с БД также важным фактором является возможность масштабирования. Поэтому, я считаю, что лучше обратиться к виртуализации уровня ОС*
- Различные web-приложения - *тут аналогично - виртуализация уровня ОС. Причины: возможность масштабирования в случае увеличения нагрузки. А также легкость балансировки этой самой нагрузки*
- Windows системы для использования бухгалтерским отделом. - *Оптимально использовать паравиртуализацию. Так как одной из основных задач будет соблюдение лицензионных требований. Ну и грамотно утилизировать аппаратные ресурсы можно*
- Системы, выполняющие высокопроизводительные расчеты на GPU. - *Тут физические сервера. Для выполнения подобного рода задач очень важно снизить расходы (в т.ч. на гипервизор). Все ресурсы - на выполнение основной задачи*

## Задача 3

### *Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.*

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.

*Для организации требуемой инфраструктуры подойдет Hyper-V или VMWare. Функционал обоих решений покроет требования данного сценария.*

2. Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.

*В этом случае будет оптимально выбрать KVM. Как раз open source с поддержкой Linux и Windows гостевых ВМ*

3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows инфраструктуры.

*Максимально совместимый гипервизор для виртуализации Windows - это Hyper-V. В данном сценарии это должна быть его бесплатная версия.*

4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

*Если говорить о Linux, то тут опять же я бы выбрал KVM, как наиболее совместимый. 
Но могу также предположить, что для тестирования приложений, возможно, лучше было бы воспользоваться каким-нибудь облаком (PaaS). Но конкретного провайдера даже не буду указывать (ибо пальцем в небо)*

## Задача 4

### *Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.*

##### Всё нижесказанное - только мои предположения, по той простой причине, что я никогда не видел таких решений. #####
Я думаю, проблемы могут быть такими:
- необходима высокая квалификация сотрудника(ов). Не исключено, что это не один и не два инженера, а команды (каждая из которых занимается сопровождением своей системы виртуализации);
- при этом, полагаю, кратно усложняется отладка в случае возникновения проблем;
- вероятно увеличение материальных затрат (как на квалифицированные кадры, так и на лицензии);
- такая среда виртуализации будет намного менее гибкой. Думаю, что масштабирование или миграция будут проходить гораздо тяжелее.

Для решения перечисленных проблем стараться избегать применения гетерогенной среды виртуализации )))
Но скорее всего, такие решения используются в тех случаях, когда другого выхода нет. Поэтому надо:
- максимально документировать все процессы, чтобы быстрее дебажить и чтобы не так болезненно было прощаться с ценными кадрами;
- максимально автоматизировать все процессы.

Я бы предпочел избегать использования нескольких систем управления виртуализацией одновременно. Но повторюсь, уверен, что это всегда вынужденная мера.*
