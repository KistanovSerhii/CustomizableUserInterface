# Customizable User Interface
Настраиваемый интерфейс пользователя 1C

* Управление видимостью объектов (в примере подсистемы "Администрирование") при помощи функциональных опций.

- Функциональные опции содержат объекты видимостью которых необходимо управлять
- Параметры ФО выполняют отбор в рег. свед. что бы получить запись с ресурсами на которые ВСЕГДА смотрят ФО
- При начале работы ФО читает значение ресурсов на которые ФО смотрят и управляет объектами (скрывает/показывает)
  по этому в событии при начале работы системы мы можем: методом платформы "УстановитьПараметрыФункциональныхОпцийИнтерфейса"
  установить значение параметра ФО, а также этот метод установит отбор в рег. свед на которые ссылается данный параметр ФО и
  тогда будет отобрана необходимая запись где значения ресурсов для ФО будет нужным!

# ПРИНЦИП РАБОТЫ:

1. Функциональные опции ВСЕГДА смотрят на значение ресурса
2. Параметры ФО отбором получают запись с этими самыми значениями ресурсов

1.1 Создаем ФО указав в состав объекты видимостью которых необходимо управлять, далее
1.2 создаем ресурс в рег. свед. "НИП_НастройкиИнтерфейсаПользователя" на который смотим.

1.1 При начале работы делаем методом платформы устанавливаем знч параметра ФО "НИП_ОтборПоПользователю"
1.2 Платформа тем самым выполнит отбор в рег. свед. и получит знч ресурсов для всех ФО которые на эти ресурсы смотрят!


# ВНЕДРЕНИЕ:

1.1 Добавляем функциональную опцию "ИмяХ" где указываем состав объектов которым необходимо управлять
1.2 Добавляем ресурс "ИмяХ" в рег. свед. "НИП_НастройкиИнтерфейсаПользователя" с типом булево
1.3 Вернемся к функциональной опции "ИмяХ" и указываем свойство хранение как ссылка на ресурс (созданый на шаге 1.2)
(ФО.Хранение = РегистрСведений.НИП_НастройкиИнтерфейсаПользователя.Ресурс.ИмяХ)

