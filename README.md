# Ozon Go School Lecture

## 23.06.2020 

Инфраструктура:
  - Микросервисная архитектура
  - Kubernetes: поды, сервисы, кластеры
  - CI 

## 25.06.2020

Цикл разработки в Ozon: 
- подготовка
- проектирование 
- создание 
- поддержка и развитие 

Модели:
- водопадная (-)
- V-модель (каскадная) 
- инкрементальная модель (кросскмандность требует большего контроля)
- спиральная модель 
- итерационная модель 

Особенности монолита:
  - привлекали тестировщиков из других команд 
  - долго 
  - в случае ошибок откатывался релиз целиком 
  - сложно вносить незапланированные изменения 

Созданы инструменты для быстрого создания микросервисов (scratch)

Микросеврисы плюсы: 
  - запрещено писать в одну базу разным микросервисам
  - в случае ошибки в релизе откатывается только один микросервис 
  - в случае сбоя приложение потеряет только часть функций 

Микросеврисы минусы: 
  - необходимость держать штат SRE 
  - мониторинг всего и везде, у каждой команды свой TV-дашборд 
  - строгие линтеры 
  - выше порог входа 
  - необходимо переосмемление архитектуры приложения 

## 27.06.2020
Редакторы кода 
  - vscode
  - goland 
  - vim 

Плагины:  
Goland: Makefile, Protobuff support   
VS Code: Go support, Go toolset, vscode-proto3  

Стректура проекта 
my-project 
  - cmd/my-project 
  - internal/app/my-project 
  - internal/app/config 
  - pkg (все экспортируемые пакеты) 
  - vendor 
  - api (описание вашего сервиса, внешних запросов)
  - bin (все зависимости вашего исполняемого файла, линтеры и т.д.)

Инструменты для работы с кодом   
  Форматирование кода:   
    - gofmt  
    - goimports   
    - go vet   

Тесты и бенчмарки - бенчмарки проверяют скорость кода   
```
go test ./...  
go test -bench ./...  
```
Линтеры 
```
golangci-lint 
golangci-lint run 
--config=.golangci.pipeline.yaml ./... 
```

Контекст и обработка ошибок 
Контекст: 
  - содержит в себе служебные данные 
  - передается во все функции как есть 
  - нельзя изменить, только создать новый 
  - древовидная структура наследования 

Обработка ошибок 
```
  if err != nil { return ... }
  err := fmt.Errorf("got wrong response: %w". productErr)

  if errors.ls(err, productErr) {
    return nil, errors.Wrap(err)
  }
```

Рекомендации:
  1. Используйте короткие названия функций и переменных 
  2. Потратье время на то, чтобы разобраться в разных типах данных. Обратите внимание на то, как рабоает рефлексия 
  3. Придерживайтесь четкой структуры проекта 
  4. Интерфейсы - очень важный и сильный концепт (практически как классы)
  5. Пишите на Go как на Go
  6. Смотреть стандартную библиотеку 
  7. Производительность и простота - отличные черты Go 

## 30.06.2020
  KISS = Keep it simple stupid
  - разбивайте задачи на короткие подзадачи 
  - сохраняйте ваши методы короткими 
  - сохраняйте ваши классы короткими 
  - придумайте решение задачи, потом напишите код 
  - не бойтесь избавляться от кода 

  YAGNI = You ain't gonna need it 
  - новые функции должны быть отлажены и документированы
  - новая функциональность ограничивает то, что может быть сделано в будущем 
  - пока новые функции не нужны, трудно предугадать, что они должны делать, и протестировать их 
  - добавление новой функциональности может привести к желанию еще более новой функциональности

  DRY = Dont repeat yourself 

  SOLID:
  - Single responsibility 
  - Open Closed 
  - Liskov Substitution 
  - Interface segregation 
  - Dependency inversion 

  GRASP = General responsibility assignment software 
  - Creator 
  - Information expert 
  - Controller 
  - High cohension/low coupling 
  
## 02.07.2020
Многопоточность 

Планировщик OS и GO
Закон амдала 

## 4.07.2020
Паттерны:
adapter 
observer 

Performance, Profiling, Debugging   
  go test -bench   
  Аллокация - выделение памяти под какой-то объект   
  pprof   
  
  .s - быстрее работает   
  Избавлемся от аллокаций  
  Debugging: printf() или ставить условие и выполнять   

## 7.07.2020    
Тестирование в GO   
  - Функциональное тестирование   
  - Компонентное тестирвоание   
  - Интеграционное тестирование   

Основная структра: 
  T - Test: тип для функционального тестирования, управление состоянием и форматирование логов.  
  B - Benchmark. Управляет временем и количеством итераций.  
  M - TestMain. Управляет запуском тестов.  

Наименование:
  GivenWhenThen / Arrange-Act-Assert   
  SUT - System under test   
 ``` 
  func (c *T) Fail()
  func (c *T) FailNow()
  func (c *T) Log()

  func (c *T) Error()

  import testing 
  t.Parallel() - параттельное тестирование 
```
Ипользовать параметезиованные тесты (struct)

## 09.07.2020
Run & deploy   
  Docker - система контейнерезации  
  Registry - хранилка артефактов, на основе кторых запускаются контейнеры. Это образы.  
  Утилита dive   
  
