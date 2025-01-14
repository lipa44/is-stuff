# Предмет: Операционные системы
Преподаватель/спикер:  **Маятин Александр Владимирович**

> ## Тема: **Лекция 5** Дата:  05.10.2021

> ### Процесс - совокупность набора исполняющихся команд, ассоциированных с ним ресурсов и контекста исполнения, находящаяся под управлением ОС (команды, ресурсы, контекст процесса)

*Один процесс может реализовывать несколько программ (за счёт системных вызовов)*

PCB (Process Control Block) - дискриптор процесса

- PID, PPID, UID
- Ресурсы
- История использования ресурсов

Почему стало не хватать определения процесса?

- Появились процессы которые умеют взаимодействовать со сложными и большими структурами данных **=> большое время ожидания**
- Появились многоядерные процессы, которые выполняют много потоков команд **=> хочется распараллелить потоки ввода-вывода**

> ### Поток (thread - нить) - это совокупность набора исполняемых команд и контекста исполнения, находящаяся под управлением ОС и разделяющая общие ресурсы одного процесса

Расходы:

- расходы на переключение потоков

*Многопоточность - задача оптимизации*

*Переключением потоков занимается планировщик*

> ### Облегчённый поток (fiber) - набор команд, разделяющий ресурсы и контекст исполнения своего потока  и находящийся под управлением пользовательского процесса

**Кооперативная многозадачность** - (только сам поток команд может передать управление другому потоку команд):

- поток команд даёт управление специальному менеджеру
- поток команд даёт управление *другому* потоку

![1.png](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/C706BF93-2641-4CBB-AD47-DDF03CE9A9D4_2/1.png)

> > ## Функции подсистемы управления процессами:

- > Создание процессов и потоков
- > Обеспечение ресурсами
- > Изоляция процессов
- > Планирование выполнения процессов
- > Диспетчеризация потоков
- > Межпроцессорное взаимодействие
- > Синхронизация процессов и потоков
- > Завершение процессов

***catred*** *- дерево потоков ядра*

`ctrl + c` *- завершение процесса*

`ctrl + z` *- введение процесса в "спячку"*

### Дерево процессов Linux

![2.png](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/B1E080E7-DFED-4E4C-897C-DC8D7B270271_2/2.png)

### Дерево процессов Windows

![3.png](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/3E8C62EB-F5BD-4C93-8BFB-5AE09C6CECAA_2/3.png)

---

> ## Тема: **Диспетчеризация** (Лекция 6)
Дата:  12.10.2021

*Диспетчеризация - задача смены состояний*

Минимальная модель диспетчеризации - **двухуровневая модель**:

- Состояние исполнения
- Завершение (выход)
- Возврат в состояние ожидания
- Состояние ожидания

> ## **Трёхуровневая модель**:

- Состояние исполнения
- Состояние ожидания
- Состояние готовности

![4.png](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/CCB9FAD4-31E7-45DC-B7AB-E97CDAEA006B_2/4.png)

> ## **Пятиуровневая модель**:

- Состояние исполнения
- Состояние ожидания
- Состояние готовности
- Состояние завершения
- Состояние рождения

![5.png](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/2FA58445-356C-45EB-A379-131A819217B8_2/5.png)

*Пятиуровневая модель - теор. базис, реализующийся почти во всех современных ОС*

> ## **Современные ОС**:

- Состояние исполнения
- Состояние ожидания (прерываемое)
- Состояние ожидания (**не** прерываемое)
- Состояние готовности
- Состояние завершения
- Состояние рождения
- Останов

![IMG_8283.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/F60E677A-E1C1-41E0-B8F6-6B43C626E90F_2/IMG_8283.jpeg)

> ## **Модели диспетчирезации**

|                                         | **Двухуровневая модель** | **Трёхуровневая модель** | **Пятиуровневая модель** | **Современные ОС** |
| --------------------------------------- | ------------------------ | ------------------------ | ------------------------ | ------------------ |
| Состояние исполнения                    | \+                       | \+                       | \+                       | \+                 |
| Завершение (выход)                      | \+                       |                          |                          |                    |
| Возврат в состояние ожидания            | \+                       |                          |                          |                    |
| Состояние ожидания                      | \+                       | \+                       | \+                       |                    |
| Состояние готовности                    |                          | \+                       | \+                       | \+                 |
| Состояние завершения                    |                          |                          | \+                       | \+                 |
| Состояние рождения                      |                          |                          | \+                       | \+                 |
| Состояние ожидания (прерываемое)        |                          |                          |                          | \+                 |
| Состояние ожидания (**не** прерываемое) |                          |                          |                          | \+                 |
| Останов                                 |                          |                          |                          | \+                 |

### Обобщённая модель устройства ОС

![IMG_8287.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/109D8061-CB31-4DDC-BFF5-2AA610B47BD4_2/IMG_8287.jpeg)

> ## **Критерии планоривания**

   - Критерий справедливости (распределять ресурсы процессам поровну)
   - Критерий эффективности
   - Критерий полного исполнения
   - Критерий времени ожидания
   - Время отклика

> ## **Свойства планирования**

   - Предсказуемость
   - Минимальные накладные расходы
   - Хорошая масштабируемость

> ## **Параметры планирования**

   - Статические
   - Динамические
   - Системные
   - Процессы

|              | Параметры системы | Параметры процесса     |
| ------------ | ----------------- | ---------------------- |
| Статические  |                   |                        |
| Динамические |                   | CPU-burst<br>I/O-burst |

> ## Тема: **Лекция 7** Дата:  19.10.2021

> ## Типы алгоритмов планирования:

   - Выетянсющие - есть механизм принудительно забрать ресурс (например, по тмаймеру)
   - НЕвытесняющие

> ## Алгоритмы:

- ### First Came - First Served (Queue/FCFS)

![IMG_1691 2.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/EB3E0BB1-B40F-40F8-B86B-1DA252830C8D_2/IMG_1691%202.jpeg)

- ### Round Robin (RR)

![Image.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/6C7FECB1-0FED-4557-9B08-806A6B8D4A12_2/Image.jpeg)

> Для Round Robin оптимальным значением K (значением кванта) зависит от конкретного распределения процессов по их времени

- ### Shortest Job First (SJF) - обычно вытесняющий

![Image-2.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/7C2C60EF-4357-4C60-9547-80D3BC20DCCC_2/Image-2.jpeg)

### Гарантированное планирование

$$r_i = T_i/N$$ - *примерно равно*

$$R = (r_i * N)/T_i$$ - коэффициент справедливости

   - $$N$$ - кол-во процессов
   - $$T_i$$ - время процесса в системе
   - $$r_i$$ - время исполнения процесса

### Внешнее управление приоритетов

### Многоуровневые очереди

> ## Требования к планировщикам

- Должен поддерживать управление приоритетами (полностью использовать время процессора)
- Должно быть обеспечено эффективное использование ресурса (хотим, чтобы процессы максимально быстро покидали память)
- Должно быть минимизировано количество переключений в режим ядра/переключение смены контекста
   - Должен эффективно использоватсья кеш-процессор
- Реализация алгоритма должна быть эффективна с точки зрения количества накладных расходов
- Должны быть минимизированы риски взаимо-блокировок

> ## Тема: **Лекция 8** Дата:  26.10.2021

> > ## Модель планировщика Windows

32 очереди, чем больше номер очереди, тем больше приоритет

![IMG_8352.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/493B1399-6B94-4765-A3F6-3F6D23EAF4B3_2/IMG_8352.jpeg)

- В REalTime процесы **не** могут менять свои очереди
- В Dynamic процесы **могут** менять свои очереди

> ### Классы приоритетов процессов

1) Realtime - 24

2) High - 13

3) Above Normal - 10

4) Normal - 8

5) Below Normal - 6

6) Idle - 4

> ### Уровни насыщения потокое

1) Time critical - +15

2) Highest - +2

3) Above Normal - +1

4) Normal - 0

5) Below Normal - -1

6) Lowest - -2

7) Idle - -15

> > ## Модель планировщика Linux

> ### Планировщик O(1)

![IMG_8353.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/27EF8602-AE07-49C0-84F2-391B84E6CD75_2/IMG_8353.jpeg)

### Балансировщик

- запускается 1 раз в 200мс и оценивает балансировку нагрузки процессов, а также делает балансировку этой нагрузки

> ### Планировщик CFS (completly fair schedule[r])

![IMG_8354.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/379585AF-57A5-4CB3-A06E-D5AA38D66D77_2/IMG_8354.jpeg)

> ## Тема: **Лекция 9** Дата:  09.11.2021

> ## Требования для…

- Тупик

> > ## Парадокс обадеющих философов

> Множество процессов находятся в **::тупиковой ситуации::**, если каждый процесс из этого множества ожидает события, которое может вызвать только другой процесс из этого же множества

> ## Условия возникновения тупика

- ::Mutal exclution:: - ресурс одновременно используется только одним процессом (условие взаимоисключения)
      - пример с принтером (всё ломается если ничё не сохранить)
- ::Hold and Wait:: - удерживаем имеющийся ресурс и при этом находимся в ожидании другого ресурса
      - Двухфазный захват ресурса - процесс берёт ресурсы, ему их дают, эти процессы блокируются
- ::No preemtion:: - не можем самостоятельно забрать ресурс у процесса (неперераспределяемость)
      - Процесс считает, что он по прежнему владеет процессом n, при этом он фактически им уже не владеет...
- ::Circilar Wait:: - существует кольцевая цепь процессов, в которой каждый процесс ждёт доступ к ресурсу, удерживаемомому другим процессом этой цепи (условие кругового ожидания)
      - Пересчитываем все ресурсы в системе и переименовываем их, и водим правило: любой процесс может запрашивать ресурсы только с номером, больше, чем любой из номеров, которые у него уже есть

> ## Методы предотвращения тупиков

- Игнорирование
- Предотвращение возникновения
- Обнаруживать и восстанавливаться

> ## Тема: **Лекция 10** Дата:  16.11.2021

> > ## Управление памятью

Концепция иерархии памяти - выделение нескольких уровней иерархии, причём на каждом уровне у нас будет увеличиваться объём, но уменьшаться скорость взаимодействия с памятью

- > Регистры CPU - байты (самая быстрая память ~ 1/10 н/сек)
- > L1 кеш - КБайты (~ 5/10 н/сек)
- > L2 кеш - МБайты (~ 5 н/сек)
- > RAM -  ГБайты (~ 50 н/сек)
- > HDD -  ТБайты (~ 5 м/сек)

**Символьный адресс** *::-(транслятор)-→>::* **виртуальный адресс** *::-(перемещающий загрузчик/динамическое преобразование)-→>::* **физический адресс**

> В основном ОС работает в RAM - HDD (swap или подкачка)

> > ## Функци ОС в управлении памяью (подсистема управления памятью)

- > Отслеживание или учёт свободной и занятой памяти
- > Первоначальное и динамическое выделение памяти
- > Настройка адрессов программы на конкретную область физической памяти *::(перемещающий загрузчик/динамическое преобразование памяти)::*
- > Полное/частичное вытеснение кода и данных из оперативной патмяти в хранилище и обратно (подкачка)
- > Защита памяти
- > Дефрагментация памяти

> ## Тема: **Лекция 11** Дата:  23.11.2021

> > ## Страничный обмен

> ***Сегментный подход*** - выделяем каждому процессу несколько сегментов

> ***Станичная организация памяти*** - представоение памяти как множества страниц, каждая из которых имеет одинаковый фиксированный размер

![Image-3.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/D46D4A7F-3436-4B18-8BFD-67AEBAABA30D_2/Image-3.jpeg)

> **Сегментно-страничная организация памяти** - у каждого процесса адресное пространство представляет собой множество сегментов

> ## Тема: **Лекция 12** Дата:  30.11.2021

> > ## Управление хранилищем (файловая система)

![telegram-cloud-photo-size-2-5273951413078178438-y.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/A6E0FA07-9C29-4D10-B6BE-9A52D20350C2_2/telegram-cloud-photo-size-2-5273951413078178438-y.jpeg)

![telegram-cloud-photo-size-2-5273951413078178439-y.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/9C769DEB-3063-49C2-9C52-8DE3DD47AF3E_2/telegram-cloud-photo-size-2-5273951413078178439-y.jpeg)

> ## Тема: **Лекция 13** Дата:  14.12.2021

> > ## Технологии виртуализации

+ > ### Задачи, ради которых нужна технология виртуализации
   1. Поддержка устаревших ОС и приложений
   2. Повысить отказоустойчисовть и … засчёт …
   3. Создание сред для тестирования ПО, инфраструктуры и лабораторных исследований
   4. Консолидация серверов (сервера должны сущестовать отдельно друг от друга)
   5. Повышение управляемости сетевой инфраструктуры
+ > ### Решения по прнципу действия
   1. Эмуляция аппаратуры (*непроизводительный вариант*)

![123.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/160EE454-CFAC-44DC-8FA0-57FBA68CFB11_2/123.jpeg)

   `Преимущество такой модели`: можно поддержать **любую** ОС

   `Недостатки такой модели`: огромные накладные расходы на любые операции выделения ресурсов

   2. Полная виртуализация (*производительный вариант*)

![12.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/441340D4-6B52-426A-A6CB-A2635F84B4A9_2/12.jpeg)

   3. Виртуализация уровня ядра ОС

![1.jpeg](https://res.craft.do/user/full/dc444d3a-1e58-7873-981d-9ea29c1e084f/doc/952A1D19-BA1A-4261-AC7C-D7A4DA009AF2/ACC50054-DA97-41FE-B61F-01F98C0C75C8_2/1.jpeg)

