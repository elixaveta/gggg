#Тату салон
- Клиент (Client)
- Мастер (Master)
- Услуга (TattooService)
- Запись (Appointment)
- Отзыв (Review)
- Способ оплаты (PaymentMethod)

#Структура папок
tattoo_salon/
    bin/
        main.dart #Точка входа
    lib/
        tattoo_salon.dart #Публичный экспорт всех модулей
        src/
            domain/ #Слой предметной области
                models/ #Модели данных (6 сущностей)
                    identity.dart
                    client.dart
                    master.dart
                    appointment.dart
                    payment_method.dart
                    review.dart
                    service.dart
                validators/ #Валидаторы (текст/числа)
                    text_validator.dart
                    number_validator.dart
        data/ #Слой данных sqlite
            database.dart #Работа с SQLite
            repositories/ #CRUD операции
                client_repository.dart
                master_repository.dart
                service_repository.dart
                appointment_repository.dart
                review_repository.dart
                payment_method_repository.dart
        cli/ #меню и обработка ввода
            menu.dart #Главное меню и команды
            input_helper.dart #Ввод с валидацией
    test/ #Тесты
        domain_test.dart
        data_test.dart
        validation_test.dart


#Что вынесено в каждый слой и почему

#Domain слой (lib/src/domain/)
- Модели (Client, Master, TattooService, Appointment, Review, PaymentMethod)
- Валидаторы (текстовые и числовые проверки)
- Почему: Этот слой содержит бизнес-логику и правила предметной области. Он не зависит от базы данных и интерфейса пользователя, что позволяет легко тестировать и изменять бизнес-правила.

#Data слой (lib/src/data/)
- Database - создание таблиц, подключение к SQLite
- CRUD операции - все методы работы с БД
- Почему: Изолирует работу с базой данных. При смене БД (например, на PostgreSQL) нужно переписать только этот слой.

#CLI слой (lib/src/cli/)
- Menu - пользовательское меню, команды
- InputHelper - повторный ввод с валидацией
- Почему: Отвечает только за взаимодействие с пользователем. При переходе на Web/API нужно заменить только этот слой.

#Реализованные валидации
-  Обязательное текстовое поле (не пустое после trim())
- Форматные/числовые поля (Числовое поле > 0, Email (формат), Телефон (формат), Дата/время записи)
-

#тесты
- Тесты сущностей (test/domain_test.dart)
- Тесты БД (test/data_test.dart)
- Тесты валидации (test/validation_test.dart)

#Запуск
- Установить зависимости: dart pub get
- Запустить приложение: dart run
- Запустить тесты: dart test
