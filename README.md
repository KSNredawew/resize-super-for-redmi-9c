# Расширение раздела Super для Redmi 9C (Angelica, Angelican, Garden)

Инструкция для расширения раздела Super на устройствах Redmi 9C (кодовые имена: Angelica, Angelican, Garden) с установкой модифицированного образа Super и кастомной прошивки Bliss ROM.

Внимание: Процедура рискованная! Ошибки могут привести к потере данных или "кирпичу" устройства. Делайте резервную копию и действуйте на свой страх и риск!

## Требования
- Redmi 9C (Angelica, Angelican или Garden) с разблокированным загрузчиком
- Установленные ADB и Fastboot на компьютере
- Совместимое рекавери (например, TWRP)
- Модифицированный образ Super: https://drive.google.com/file/d/1qHKRnmrkjdS3rpHiEHMozq6bwX09it2k/view
- Модифицированная прошивка Bliss ROM: https://drive.google.com/file/d/1lbwPOeY56k7T1TSbu1bG3AMtxiH5dkVj/view

## Инструкция

1. Вход в ADB Shell
   Подключите устройство к ПК и выполните:
   adb shell

2. Удаление разделов
   Удалите разделы 38 и 41 с помощью sgdisk:
   
   /system/bin/sgdisk --delete=38 /dev/block/mmcblk0
   /system/bin/sgdisk --delete=41 /dev/block/mmcblk0

4. Создание новых разделов
   Создайте раздел Super размером 10 ГБ и обновите Userdata:
   
   /system/bin/sgdisk --new=38:0:+10G --typecode=38:8300 --change-name=38:super /dev/block/mmcblk0
   /system/bin/sgdisk --new=41:0:0 --typecode=41:8300 --change-name=41:userdata /dev/block/mmcblk0

6. Сохранение изменений
   Синхронизируйте изменения:
   sync

7. Выход из ADB Shell
   Завершите сессию:
   
   exit

9. Перезагрузка в рекавери и сброс данных
   Перезагрузитесь в рекавери и выполните wipe data/factory reset.

10. Переход в Fastbootd
   Перезагрузитесь в режим Fastbootd (не обычный Fastboot!):
   adb reboot fastboot

11. Очистка раздела Super
   Удалите содержимое раздела Super:
   fastboot erase super

12. Прошивка модифицированного образа Super
   Прошейте скачанный образ Super:
   fastboot flash super super.img

13. Установка Bliss ROM
    В рекавери установите скачанную прошивку Bliss ROM.

14. Перезагрузка в систему
    Если загрузка прошла успешно, всё готово!

## Устранение неполадок
- Устройство не загружается: Перепроверьте правильность выполнения шагов, особенно прошивку Super и ROM.
- Ошибки ADB/Fastboot: Убедитесь, что драйверы установлены и устройство распознаётся.
- Проблемы в рекавери: Используйте последнюю версию TWRP, совместимую с вашим устройством.

## Примечания
- Резервная копия обязательна перед началом.
- Автор не несёт ответственности за повреждение устройства.
- Задавайте вопросы в сообществах, например, на XDA Developers.

## Благодарности
- SamuraiArtem 
- Команде Bliss ROM за прошивку.
