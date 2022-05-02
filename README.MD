# Что тут
Это пример кода, все чувствительные места я стер, либо заменил на "Example" и прочее.

**Сам код** - это пользовательская интеграция для AmoCRM, выполненная на стеке: **Phalcon, Mongodb, Redis, Beanstalk, js**. Интеграция работает не сама по себе, а на базе ядра, которое я не привожу, т.к. писалось оно не мной и нехорошо чужие работы вот так отдавать)


# Что оно делает

У службы доставки еды есть самописная CRM-система, также у этой службы есть AmoCRM - наша задача синхронизировать их работу по определенной логике. Если коротко, когда в ту CRM пришел заказ - поймать об этом сигнал, создать сделку в Amo, когда в Amo менеджер добавил комментарий к заказу - отправить изменения в ту CRM систему и тд. Также, помимо этого нужно писать логи, работать с очередями, обрабатывать ошибки и прочие мелочи.

Как и что конкретно работает проще будет узнать из самого кода, он хорошо прокомментирован, советую начать с контроллеров. 

# Структура

- **api**
  - **Controller** 
    - **AmoWebhookController.php** - *обрабатывает вебхуки из AmoCRM (реагирует на добавление\изменение\удаление сделок в AmoCRM)*
    - **CreateLeadController.php** - *обработка запросов из виджета CreateLead*
    - **ExampleCrmController.php** - *обработка запросов из клиентской crm (когда из их црм, на наш сервер падает запрос о добавлении\изменении\удалении заказа)*
- **cli**
  - **Task** - *тут задачки. Контроллер кидает задачки в очередь, таск выполняет задачки*
    - **AmocrmTask.php** - *задачки от AmoCRM*
    - **ExampleCrmTask.php** - *задачки от клиентской crm* 
- **common**
  - **Constants.php** 
  - **HookCache.php** - *работа с кешем*
- **resource**
  - **config** - *тут конфиги, крон задачки и тд*
  - **widgets** - *тут виджеты для AmoCRM, внутри каждый виджет имеет структуру, которую делают по регламенту Amo*
    - **create_lead** 
      - **widget** - *сам виджет*