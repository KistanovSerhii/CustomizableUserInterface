# Customizable User Interface
Настраиваемый интерфейс пользователя 1C

* Управление видимостью объектов (в примере подсистемы "Администрирование") при помощи функциональных опций.

- Функциональная опция "НИП_ИнтерфейсАдминистратора" содержит объекты которые необходимо скрыть/показать админам и ссылается на ресурс "Видимость" (булево) рег. свед. "НИП_ПараметрыНИП"

- Параметр функциональной опции "НИП_ДоступАдминистратор" ссылается на измерения "Доступ" рег. свед. "НИП_ПараметрыНИП". ВАЖНО: Наименование всегда должно начинаться с приставки "НИП_"

- Справочник "НИП_Доступы" содержит табличную часть "Пользователи" с реквизитом "Пользователь" (Ссылка на справочник "Пользователи"). ВАЖНО: Наименование данного справочника должно быть точно как именуется Параметр функциональной опции. В ТЧ добавляем пользователей которым необходимо дать/забрать видимость объектов.

Справочник "НИП_Доступы" всегда должен содержать элемент с наименованием "ПоУмолчанию"!

# ВНЕДРЕНИЕ

В конфигураторе:
  1.1 Добавить функциональную опцию и в свойстве "состав" указать объекты которыми управляет данная ФО
  1.2 Свойство "хранение" ФО указать РегистрСведений.НИП_ПараметрыНИП.Ресурс.Видимость
  
  2.1 Добавить параметр функциональной опции (с префиксом "НИП_") где свойству "Использование" указать РегистрСведений.НИП_ПараметрыНИП.Измерение.Доступ

В режиме предприятия:
  3.1 Создать элемент справочника "НИП_Доступы" с наименованием "ПоУмолчанию"
  3.2 Создать элемент справочника "НИП_Доступы" с наименованием которое имеет параметр функциональной опции добавленной в разделе 2.1
  3.3 В элементе справочника "НИП_Доступы" добавленого в предыдущем разделе (3.2), в ТЧ "Пользователи" добавить необходимых пользователей
  
  4.1 Добавить запись в регистре сведений "НИП_ПараметрыНИП" указать справочник "ПоУмолчанию" где значение "Видимость" = Ложь
  4.2 Добавить запись в регистре сведений "НИП_ПараметрыНИП" указать справочник созданный в разделе 3.2 где значение "Видимость" = Истина

# Пояснение
  Платформеный метод "УстановитьПараметрыФункциональныхОпцийИнтерфейса" принимает первым параметром имя "Параметра функциональной опции" как в конфигураторе, а вторым 
  значение по которому метод выполнить отбор в регистре сведений которы указан объекте "Параметр функциональной опции" и значение ресурса будет влиять на объект "Функциональная опция" (так как в его свойствав хранение ссылается на данный ресурс)

# Пояснение
 В текущем исходнике (примере) в расширение из основной конфигурации добавлено:
  Справочник "Пользователи", Подсистема "Администрирование"
 Необходимо:
1. Добавить в справочник "НИП_Доступы" элемент с наименованием "ПоУмолчанию" и "НИП_ДоступАдминистратор" (это имя ПараметраФО), элементу с наименованием "НИП_ДоступАдминистратор" в табличную часть "Пользователи" добавить пользователя которому бедет доступна подсистема "Администрирование"
2. Добавить в регистр сведений "НИП_ПараметрыНИП" справочник "ПоУмолчанию" (ресурс "Видимость" = Ложь)
3. Добавить в регистр сведений "НИП_ПараметрыНИП" справочник "НИП_ДоступАдминистратор" (ресурс "Видимость" = Истина)

Результат:
  Пользователям указанным в ТЧ справочника "НИП_ДоступАдминистратор" будет доступна подсистема "Администрирование" (остальным пользователям - НЕТ!)
