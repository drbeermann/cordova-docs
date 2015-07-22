---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
---

# Платформа Android руководство

Это руководство показывает, как настроить среду разработки SDK для развертывания приложений Cordova для устройств Android. Он проведет вас через процесс установки Android SDK, открытие Android-проект в Eclipse SDK и развертывание на эмуляторе или устройстве. Вам будет нужно следовать этому руководству, чтобы по крайней мере установить Android SDK, независимо от того, какой процесс вы следуете. ( *Веб проекта Dev* и *Родной платформе Dev* рабочие процессы требуют Android SDK, чтобы быть установлен и доступен через ваш путь).

Смотрите ниже для более подробной информации конкретной платформы:

*   Андроид конфигурации
*   Андроид WebViews
*   Андроид плагины
*   Обновление Android
*   Android средства командной строки

Средства командной строки относятся к версии до 3.0 Кордова. Смотрите информацию о текущем интерфейсе интерфейс командной строки.

## Требования и поддержка

Смотрите [системные требования][1] Android SDK.

 [1]: http://developer.android.com/sdk/index.html

Кордова поддерживает Android 2.2, 2.3 и 4.x. Как правило являются устаревшими платформ, как они опустится ниже 5% на Google в [панель распределения][2].

 [2]: http://developer.android.com/about/dashboards/index.html

<!--
NOTE, doc said:
- Android 2.1 (Deprecated May 2013)
- Android 3.x (Deprecated May 2013)
-->

Разработчики должны использовать `cordova` утилита в сочетании с Android SDK. Увидеть интерфейс командной строки для получения информации, как установить его, добавить проекты, а затем построить и развернуть проект.

Установить Android SDK от [Developer.Android.com/SDK][3]. Android sdk распространяется в виде «АТД-Комплект -<os>-<arch>-<ver>' файл. На windows АТД Комплект поставляется с инсталлятором. На OSX и Linux, просто распакуйте adt пакет в папке хранить средства разработки. [Более подробную информацию по установке Android SDK можно найти здесь][4]

 [3]: http://developer.android.com/sdk/
 [4]: http://developer.android.com/sdk/installing/bundle.html

Для Кордова средства командной строки для работы, вам необходимо включить в SDK `tools` и `platform-tools` каталогов в среде PATH. На Mac, вы можете использовать текстовый редактор для создания или изменения `~/.bash_profile` файл, добавив строку, например, в зависимости от того, где SDK устанавливает:

    экспорт путь = ${путь}: / развития/АТД Комплект/sdk/платформы tools: / развития/АТД Комплект/sdk/инструменты
    

Это предоставляет средства SDK в недавно открытый терминал windows. В противном случае выполните это, чтобы сделать их доступными в текущем сеансе:

    $ Источник ~/.bash_profile
    

Чтобы изменить путь среды на Windows 7:

*   Нажмите на меню " **Пуск** " в левом нижнем углу рабочего стола, щелкните правой кнопкой мыши на **компьютере**, а затем нажмите кнопку **Свойства**.

*   Нажмите кнопку **Дополнительные параметры системы** в столбце слева.

*   В открывшемся диалоговом нажмите **Переменные среды**.

*   Выберите переменную **PATH** и нажмите **редактировать**.

*   Добавьте следующее в путь, основанный на котором установлен пакет SDK, например:
    
        ;C:\Development\adt-bundle\sdk\platform-tools;C:\Development\adt-bundle\sdk\tools
        

*   Сохраните значение и закройте оба диалоговые окна.

Также может потребоваться включить Java и Ant. открыть командную строку и введите `java` , а также ввести `ant` . Добавления к пути зависимости не удается запустить:

        ;%JAVA_HOME%\bin;%ANT_HOME%\bin
    

## Откройте проект в SDK

Использование `cordova` утилита для настройки нового проекта, как описано в Cordova интерфейс командной строки. Например в каталоге исходного кода:

        $ cordova create hello com.example.hello "HelloWorld"
        $ cd hello
        $ cordova platform add android
        $ cordova build
    

После создания, вот как использовать пакет SDK для его изменения:

*   Запустите приложение **Eclipse** .

*   Выберите пункт меню **Создать проект** .

*   Выберите **Android-проект из существующего кода** из диалогового окна полученный и нажмите **Далее**: ![][5]

*   Перейдите к `hello` , или какой вы создан каталог для проекта, затем в `platforms/android` подкаталога.

*   Убедитесь, что оба `hello` и `hello-CordovaLib` должны быть импортированы выбранные проекты. `hello-CordovaLib`Проект необходим по состоянию на Cordova 3.3.0, потому что Кордова в настоящее время используется как Android библиотеки вместо файла .jar.

*   Нажмите кнопку **Готово**.

 [5]: img/guide/platforms/android/eclipse_new_project.png

После того, как откроется окно Eclipse, красный **X** может показаться указывают нерешенные проблемы. Если это так, выполните следующие дополнительные действия:

*   Щелкните правой кнопкой мыши на папке проекта.

*   В результате диалоговом окне **свойств** выберите **Android** из области переходов.

*   Для проекта цели, выбирать самый высокий уровень Android API, которые вы установили.

*   Нажмите **кнопку ОК**.

*   Выберите **очистить** из меню **проект** . Это должно исправить все ошибки в проекте.

## Развернуть эмулятор

Вы можете использовать `cordova` утилита для запуска приложения в эмуляторе, или вы можете запустить его в рамках SDK. В любом случае, SDK сначала должен быть настроен для отображения по крайней мере одно устройство. Чтобы сделать это, используйте менеджер SDK Android, Java-приложение, которое запускается отдельно от Eclipse. Существует два способа, чтобы открыть ее:

*   Запуск `android` в командной строке.

*   В Eclipse, нажмите этот значок панели инструментов:
    
    ![][6]

 [6]: img/guide/platforms/android/eclipse_android_sdk_button.png

После открытия, Android SDK Manager отображает различные библиотеки времени выполнения:

![][7]

 [7]: img/guide/platforms/android/asdk_window.png

Выберите **Инструменты → Управление AVDs** (Android виртуального устройства), а затем выберите любой элемент из **Определения устройства** в диалоговом окне возникшей:

![][8]

 [8]: img/guide/platforms/android/asdk_device.png

Нажмите **Создать AVD**, при необходимости изменяя имя, затем нажмите **кнопку ОК** , чтобы принять изменения:

![][9]

 [9]: img/guide/platforms/android/asdk_newAVD.png

AVD затем появляется в списке **Android виртуальных устройств** :

![][10]

 [10]: img/guide/platforms/android/asdk_avds.png

Чтобы открыть эмулятор как отдельное приложение, выберите AVD и нажать кнопку **старт**. Он запускает, как он на устройстве, с дополнительные элементы управления, доступные для аппаратных кнопок:

![][11]

 [11]: img/guide/platforms/android/asdk_emulator.png

В этот момент вы можете использовать `cordova` утилита для развертывания приложения в эмулятор из командной строки:

        $ cordova emulate android
    

Если вместо этого вы работаете в среде Eclipse, щелкните правой кнопкой мыши проект и выберите **выполнить как → приложения для Android**. Вас могут попросить указать AVD, если ни один уже открыт.

Для более быстрый опыт используйте изображение на основе Intel эмулятора:

*   Установите один или несколько `Intel x86 Atom` образы системы, а также `Intel Hardware Accelerated Execution Manager` , доступных под **экстра**.

*   Запустите инсталлятор Intel, который доступен в вашем Android SDK в`extras/intel/Hardware_Accelerated_Execution_Manager`.

*   Создайте новый AVD с поставленной цели Intel изображения.

*   При запуске эмулятора, обеспечить существует без сообщений об ошибке, указывающее на сбой загрузки модулей HAX.

## Развертывание на устройство

Для проталкивания приложение непосредственно на устройство, убедитесь, что включена отладка USB на вашем устройстве, как описано на [Android Разработчик сайта][12]и использовать мини-USB кабель, подключить его к вашей системе.

 [12]: http://developer.android.com/tools/device.html

Вы можете нажать приложение на устройство из командной строки:

        $ cordova run android
    

Попеременно в Eclipse, щелкните правой кнопкой мыши проект и выберите **выполнить как → приложения для Android**.