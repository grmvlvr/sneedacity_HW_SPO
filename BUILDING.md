# Сборка Sneedacity

## Требования

* **python3** >= 3.5
* **cmake** >= 3.16
* Работающий компилятор C++17

### CMake

На Windows, пожалуйста, используйте [готовые бинарные файлы](https://cmake.org/download/).

На macOS, самый лёгкий способ установить CMake - это команда `brew install cmake`.

На Linux, `cmake` обычно доступен из системного пактеного менеджера.

### Windows

Мы собираем Sneedacity, используя [Microsoft Visual Studio 2019](https://visualstudio.microsoft.com/vs/community/). Для сборки Sneedacity необходимо выбрать предустановку **Desktop development with C++**.

Хотя мы запрашиваем только C++17 - MSVC 2017 тоже подходит.

### MacOS

Мы собираем Sneedacity, используя XCode 12. Однако, это также возможно с XCode 7.

### Linux

Мы используем GCC 9, но любой совместимый с C++17 компилятор должен подойти.

На Debian/Ubuntu всё необходимое можно установить при помощи соедующих команд:

```
$ sudo apt-get update
$ sudo apt-get install -y build-essential cmake git python3-pip
$ sudo apt-get install libgtk2.0-dev libasound2-dev libavformat-dev libjack-jackd2-dev uuid-dev
```

## Сборка на Windows

1. Склонируйте Sneedacity из проекта Sneedacity на GitHub. 
  
   Например, в **git-bash** это будет выглядеть так:

    ```
    $ git clone https://github.com/formerlychuck/sneedacity/
    ```

2. Откройте CMake GUI. 
   
   Установите **Where is the source code** как директорию, в которую склонировали Sneedacity. 
   
   Установите **Where to build the binaries** как директорию, в которую хотите сохранить файлы сборки. Желательно, чтобы это не была та же директория, в которой хранятся исходные файлы.

3. Нажмите **Configure**. Во всплывающем окне вы можете выбрать версию Visual Studio и платформу для сборки. Мы поддерживаем платформы **x64** и **Win32**. Платформа **x64** выбрана по умолчанию. Нажмите **Finish**, чтобы начать процесс настройки.

4. После успешной настройки вы увидите `Configuring done` в последней строке журнала. Нажмите **Generate**, чтобы сгенерировать проект Visual Studio. 

5. После появления надписи «Generating done» нажмите **Open Project**, чтобы открыть проект в Visual Studio.

6. Выберите «Build -> Build Solution».

7. Теперь вы можете запускать и отлаживать Sneedacity!
      
Как правило, шаги 1-5 нужны только при первой настройке. Затем, сгенерировав решение, вы можете открыть его в Visual Studio в следующий раз. Если конфигурация проекта изменилась, IDE вызовет CMake изнутри. 

## macOS

1. Склонируйте Sneedacity из проекта Sneedacity на GitHub. 
  
    ```
    $ git clone https://github.com/formerlychuck/sneedacity/
    ```

2. Настройте Sneedacity, используя CMake:
   ```
   $ mkdir build && cd build
   $ cmake -GXcode -T buildsystem=1 ../sneedacity
   ```

3. Откройте проект Sneedacity в XCode:
   ```
   $ open Sneedacity.xcodeproj
   ```
   и соберите Sneedacity, используя IDE. 

Шаги 1 и 2 требуются только для первых сборок. 

В качестве альтернативы вы можете использовать **CLion**. Если вы решили сделать это, откройте каталог, в который вы клонировали Sneedacity с помощью CLion, и все готово.

На данный момент мы поддерживаем только сборки **x86_64**. Можно собирать на аппаратном обеспечении AppleSilicon, но **mad** и **id3tag** должны быть отключены.:

```
cmake -GXCode -T buildsystem=1 -Dsneedacity_use_mad="off" -Dsneedacity_use_id3tag=off ../sneedacity
```

## Linux и другие ОС

Примечание: официально поддерживаются только Debian и Ubuntu.

1. Склонируйте Sneedacity из проекта Sneedacity на GitHub. 
  
    ```
    $ git clone https://github.com/Sneeds-Feed-and-Seed/sneedacity/
    ```

2. Настройте Sneedacity, используя CMake:
   ```
   $ mkdir build && cd build
   $ cmake -G "Unix Makefiles" -Dsneedacity_use_ffmpeg=loaded ../sneedacity
   ```
   По умолчанию будет настроена сборка Debug. Чтобы изменить это, передайте в CMake команду `-DCMAKE_BUILD_TYPE=Release.

3. Соберите Sneedacity:
   ```
   $ make -j`nproc`
   ```

4. Тестирование сборки:
Добавление папки «Portable Settings» позволяет Sneedacity игнорировать настройки любой существующей установки Sneedacity.
   ```
   $ cd bin/Debug
   $ mkdir "Portable Settings"
   $ ./sneedacity
   ```

5. Установите Sneedacity
   ```
   $ cd <build directory>
   $ sudo make install
   ```

