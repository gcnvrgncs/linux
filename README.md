# Тема: Как правильно делать резервные копии в Linux?

Хочу настроить резервное копирование на своем домашнем сервере с Linux. 

Рекомендую использовать rsync для простого инкрементального бэкапа. 
Очень легкий, надежный, можно запускать по cron.
Если хочешь более продвинутый вариант — глянь на tar в связке с gzip для архивирования.
А для автоматизации — bacula или amanda, но они посложнее.

Для простых случаев ставлю скрипт на rsync с удаленной машиной через ssh.
Очень удобно и быстро.
И не забудь проверить права доступа к файлам и папкам.

+1 к rsync.
Еще рекомендую добавить логирование в скрипт, чтобы отслеживать успешность бэкапов.

Сайт для проверки: http://87.242.103.172/

И как вообще настроить cron для запуска бэкапа?

Это запустит rsync каждый день в 2 часа ночи.
Чтобы отредактировать crontab, используйте команду crontab -e.





уководство пользователя программного обеспечения 
Версия ПО: 7.x
Дата издания: июля 2025 г.
1. Введение
1.1. Область применения
Программное средство VirtualBox предназначено для организации и управления виртуальными
машинами на компьютерах с архитектурой x86/x64 и ARM (в том числе Mac с M1/M2).
Используется для запуска различных гостевых операционных систем (Windows, Linux, macOS, BSD
и др.) в изолированной среде внутри основной (хост-) системы.
1.2. Краткое описание возможностей
• Создание, настройка и запуск виртуальных машин.
• Поддержка снимков (snapshots) и клонов виртуальных машин.
• Сетевые режимы: NAT, мостовой интерфейс (Bridged), внутренние и хостовые сети.
• Общие папки и буфер обмена между хостом и гостем.
• Поддержка 3D-ускорения, USB‑устройств, аудио и последовательных портов.
1.3. Уровень подготовки пользователя
Рекомендуется, чтобы пользователь имел базовые знания: - работы с компьютерными
операционными системами (установка и конфигурация); - основ виртуальных машин и сетевых
интерфейсов.
1.4. Эксплуатационная документация
Перед началом работы рекомендуется ознакомиться с: - Официальным руководством
пользователя Oracle VirtualBox (PDF). - Руководством по установке VirtualBox Extension Pack. -
Документацией гостевых дополнений (Guest Additions).
2. Назначение и условия применения
2.1. Виды деятельности и функции
• Тестирование программного обеспечения в изолированной среде.
• Обучение и демонстрация различных операционных систем.
• Разработка и отладка программ с возможностью быстрого восстановления состояний.
• Сетевое моделирование и анализ.
2.2. Условия применения
• Аппаратные требования:
• Процессор: не менее двух ядер x86/x64 или Apple Silicon (ARM).
1
• ОЗУ: минимум 4 ГБ (рекомендуется 8 ГБ и более).
• Диск: свободное пространство для образов виртуальных дисков (минимум 20 ГБ).
• Операционная среда (хост):
• Windows 10/11, macOS 11+, Linux (дистрибутивы с ядром 5.x+).
• Системное ПО:
• Поддержка аппаратной виртуализации (VT-x/AMD-V или HVM на ARM).
• Установленные драйверы USB и сетевых адаптеров.
• Входная информация:
• Образы установочных ISO гостевых ОС.
• Сетевые настройки и параметры виртуальных дисков.
• Требования к подготовке специалистов:
• Знание основ администрирования операционных систем.
• Навыки работы с командной строкой (по необходимости).
3. Подготовка к работе
3.1. Состав и содержание носителя данных
Носителем данных могут выступать: - Установочный пакет VirtualBox (.exe, .dmg, .rpm/.deb). -
Расширения: VirtualBox Extension Pack. - Образы Guest Additions ISO.
3.2. Порядок загрузки программ и данных
1. Скачайте установочный пакет с официального сайта.
2. Запустите инсталлятор и следуйте шагам мастера установки.
3. После завершения установки запустите VirtualBox.
4. При необходимости установите Extension Pack: меню Файл → Параметры → Расширения
→ Добавить пакет.
3.3. Порядок проверки работоспособности
1. Запустите VirtualBox.
2. Перейдите в Справка → О VirtualBox; убедитесь, что отображается версия.
3. Создайте тестовую виртуальную машину с минимальными параметрами.
4. Смонтируйте ISO с линукс-дистрибутивом и запустите установку гостевой ОС.
5. Убедитесь, что виртуальная машина запускается и реагирует на ввод с клавиатуры и
мыши.
4. Описание операций
В данном разделе описаны основные операции с виртуальными машинами.
4.1. Создание виртуальной машины
• Наименование: Создание ВМ
• Условия: VirtualBox запущен, свободные ресурсы оперативной памяти и дискового
пространства.
• Подготовительные действия:
• Откройте главное окно VirtualBox.
• Проверьте настройки сети и папок общего доступа (при необходимости).
• Основные действия:
2
• Нажмите кнопку Создать.
• Введите имя ВМ и выберите тип/версию ОС.
• Укажите объем ОЗУ и размер виртуального диска.
• Настройте дополнительные параметры (сеть, USB, папки).
• Нажмите Готово.
• Заключительные действия:
• Убедитесь, что новая ВМ отображается в списке.
• При необходимости отредактируйте параметры через Настройки.
• Ресурсы: ОЗУ, дисковое пространство, сетевые адаптеры.
4.2. Запуск и остановка виртуальной машины
• Наименование: Запуск/остановка ВМ
• Условия: ВМ создана.
• Подготовительные действия: Убедитесь, что ISO или образ диска подключены.
• Основные действия:
• Выберите ВМ и нажмите Запустить.
• Для остановки: меню Машина → Закрыть → Завершить работу или Сохранить
состояние.
• Заключительные действия: Проверьте логи в случае ошибок.
• Ресурсы: Процессор, ОЗУ.
4.3. Снимки состояния (Snapshots)
• Наименование: Создание снимка
• Условия: ВМ запущена или остановлена.
• Подготовительные действия: Подготовить наименование и описание снимка.
• Основные действия:
• Меню Машина → Снимки.
• Нажмите Создать снимок.
• Введите имя и описание.
• Заключительные действия: Убедитесь, что снимок добавлен.
• Ресурсы: Дисковое пространство.
(Аналогично описать восстановление снимка, удаление, создание клона.)
5. Аварийные ситуации
5.1. Несоблюдение условий выполнения
• Признаки: ВМ не запускается, ошибки виртуализации.
• Действия:
• Проверить включение аппаратной виртуализации в BIOS/UEFI.
• Перезапустить хост-систему.
5.2. Отказ носителей данных
• Признаки: Ошибки чтения виртуального диска.
• Действия:
• Проверить целостность VDI/VMDK-файла.
• Восстановить из резервной копии.
3
5.3. Обнаружение ошибок в данных
• Признаки: Некорректная работа гостевой ОС.
• Действия:
• Запустить проверку файловой системы гостя.
• Восстановить снимок перед ошибкой.
5.4. Несанкционированный доступ
• Признаки: Неизвестные учетные записи, изменения в настройках.
• Действия:
• Изменить пароли доступа хоста.
• Проверить права на файлы VM.
• Отключить общий буфер обмена и папки.
5.5. Другие аварийные ситуации
• Признаки: Перегрузка хоста, утечка памяти.
• Действия:
• Освободить ресурсы (закрыть ненужные процессы).
• Пересмотреть настройки ОЗУ и ЦП для ВМ.
6. Рекомендации по освоению
6.1. Общие рекомендации
• Начните с простых тестовых ВМ (минимальные ресурсы).
• Изучите команды VBoxManage для автоматизации.
• Практикуйтесь в создании и восстановлении снимков.
6.2. Контрольный пример
• Задача: Установить Ubuntu 22.04 в VirtualBox и создать снимок.
• Шаги запуска и выполнения:
• Создать ВМ с именем "Ubuntu_Test", 2048 МБ ОЗУ, диск 20 ГБ.
• Смонтировать ISO Ubuntu 22.04.
• Запустить ВМ и установить ОС.
• После установки и первого запуска сделать снимок "Clean_Install".
6.3. Правила запуска и выполнения
• Всегда храните описания снимков с указанием версии ОС и состояния.
• Перед внесением существенных изменений создавайте новый снимок.
• Документируйте конфигурацию ВМ (ОЗУ, CPU, сеть) отдельно от сним








Отчёт по установке и настройке операционной системы
Конечный пользователь: техник-программист отдела мобильной разработки
Используемая OS: Ubuntu 20.04LTS

Предоставляемые аппаратные параметры:
8ГБ ОЗУ
8 ядер процессора
256мб видеопамяти с графическим ускорением
25гб жесткий диск для работы системы
6гб флеш-накопитель USB для создания образа ISO.



Установка и настройка ОС
Для выбора операционной системы были заданы данные критерии:
* Надежность операционной системы, поддержка стабильности
* Наличие большинства современного ПО
* Богатый набор инструментов
* Приятный визуальный интерфейс
Ubuntu на базе Linux подходит под заданные критерии

Установка системы совершалась с .iso образа Ubuntu 20.04LTS. Процесс установки - стандартный с установкой всех инструментов.

Для входа в систему от лица администратора были заданы параметры авторизации:
Логин: pewpow
Пароль: pewpow228

Для безопасной работы с ОС и выполнения обязанностей техника-программиста также был создан пользователь:
Логин: fixer
Пароль: password24#%

После авторизации в системе доступен рабочий стол для работы с системой(см. Рисунок 1)


Доступ в интернет по кабелю был настроен в процессе установки операционной системы.
Чтобы проверить доступ в интернет, был использован браузер Firefox (см. Рисунок 2). На данном рисунке совершен http запрос по адресу https://google.com. Результат - соединение присутствует.


Для работы с оборудованием были установлены гостевые драйвера VirtualBox. Они обеспечивают масштабирование окна, работу со звуком, обработку графики видеокартой. (см. Рисунок 3)


Настройка ssh соединения.
Для удаленного подключения к терминалу ПК был установлен и запущен openssh-server. 
Sudo apt install openssh-server
Работа сервера была проверена командой
sudo systemctl status ssh


Настройка пользователей и групп проводилась через утилиту Users and Groups(см.Рисунок )

Пользователь fixer был добавлен в группу fixers. Также пользователю были удалены привилегии просмотра системных журналов, использование беспроводных сетей и настройки оборудования. Благодаря этому пользователь может использовать лишь доступные для него инструменты и не может навредить системе.


Настройка ядра была выполнена автоматически на этапе установки ОС. Также для настройки была использована утилита sysctl(доступна в стандартном наборе утилит Ubuntu). На Рисунке показано применение sysctl для настройки маршрутизации пакетов в локальной сети.


К ОС через параметры системы был добавлен виртуальный принтер VitrualBox


Большая часть базового программного обеспечения была установлена в процессе установки ОС.  В том числе бесплатный офисный пакет “LibreOffice” (Рисунок). Также был установлен антивирус ClamTk и инструмент для работы с 2д графикой “GIMP”.
На рисунке: браузер, калькулятор и календарь

Календарь

Калькулятор

Оффисный пакет LibreOffice

Браузер Fixefox

Проводник

Интрумент работы с 2д графикой GIMP

Антивирус Clamtk установлен и настроен:



В случае возникновения проблем с системой, была создана резервная копия с помощью системной утилиты “Резервное копирование”(Рисунок )

Резервная копия создана, сохранена на локальном диске и доступна для восстановления (Рисунок)


В качестве дополнительной меры возврата системы была использования утилита Timeshift для создания точек восстановления (Рисунок). Timeshift сохраняет полную копию системы в определенных интервалах времени. В данный момент утилита настроена на создание двух точек восстановления в месяц.


Журналы мониторинга настроены и доступны в удобном виде через утилиту “Журналы”


Установка и настройка конфигурации программного обеспечения
В качестве интегрированной среды разработки для создания приложений на android была выбран и установлен Android studio. IDE прошла настройку и не имеет искажений в интерфейсе. Как инструмент работы с 3D графикой был выбран OpenSCAD(Рисунок 2). Для тестирования различных операционных сред была выбрана и установлена программа VitrualBox.

Android Studio

OpenSCAD

VirtualBox

Масштабирование изображения отключено

Композиция рабочего стола отключена. WaylandEnable=false отключает композитор рабочего стола Wayland и использует Xorg.

Данное ПО прошло настройку и готово к использованию.
Проверка масштабирования:
Результат: кнопки Android studio читаемые, интерфейс оптимального размера. Проверка цветопередачи. В качестве старого ПО был взят GIMP
