# Дерево устройства RMX3393 (ВНИМАНИЕ СМ. ПРОБЛЕМЫ)
Дерево было сгенерированно скриптом twrpdtgen и добавлены некоторые флаги.
## Требования к системе для сборки
- 18+Гб Ram (в витруальной машине выставим 16Гб тк компилятор требует минимум 16)
- 6-ти и больше ядерный процессор
- ну по желанию видеокарту

## Требования к смартфону
- Разблокированный загрузчик (я могу протестировать вы только напишите в лс)
- Умение пользоваться командами ```fastboot``` и ```adb``` (если соблюдён пункт 1)

## Инструкция как собрать
- Скачиваем vitrualbox или устанавливаем систему на флешку и загружаемся с неё, но это неудобно
- Скачиваем с офф сайта ubuntu lts
- Настраиваем virtualbox. Важно не ставить галку автоматической настройки системы и лучше ставить пункт динамический диск размером 80 или 90 гигов. Так много потому что исходники весят много.
ВАЖНО: Установите дополнения для гостевой ОС. В ubuntu это делается с костылями загуглите. DragnDrop не будет работать, только копирование и вставка текста!
- После настройки и установки системы (важно запомнить пароль root он нам понадобиться для установки доп пакетов), запускаем.
- Открываем терминал на рабочем столе и пишем по очереди команды (при запросе пароля вводим тот, который задали при настройке):
```sh
cd
sudo -s
apt install curl (если задаст вопрос всегда нажимаем y)
apt install libssl-dev
apt install python3-pip
apt install linux-headers-6.2.0-26-generic build-essential dkms
apt install libc6-dev
apt install openjdk-19-jre-headless
apt install git
apt install rsync
apt install virtualbox-guest-x11 (это если дополнения установились но разрешение не меняется автоматом при масштабировании окна)
apt install pcmanfm (удобный файловый менеджер, мне понравился. НЕ РЕКЛАМА)
sudo ln -s /usr/bin/python3 /usr/bin/python
```
- Далее выбираем место куда будем собирать twrp. Я рекомендую в домашнюю папку. Важно кирилица недопустима (папка рабочий стол на русском написана)
- Создаём папку и в ней открываем консоль. Пишем:
```sh
sudo apt update
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
repo init --depth=1 --no-repo-verify -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1 -g default,-mips,-darwin,-notdefault
repo sync -c --no-clone-bundle --no-tags --optimized-fetch --prune --force-sync -j8
```
- После того как всё скачалось открываем папку и переходим в папку device
- Открываем консоль и пишем команду:
```sh
git clone https://github.com/An0th3rAE/device_tree_rmx3393
```
- Переносим папку oplus в device
- Должно получиться так: ```/*ваша_папка*/device/oplus/ossi/```
- Далее переходим в корень этого проекта ```/*ваша_папка*/``` открываем консоль и пишем:
```sh
. build/envsetup.sh
lunch (выбираем omni_ossi-eng по идее цифра 5)
make -j*цифра* bootimage (на месте *цифра* пишите сколько ядер вы готовы отдать компилятору. больше быстрее соберётся.
```
- Если ошибок нет и у вас появилась зелёная надпись в консоле, то готовый образ находится по пути: ```/*ваша_папка*/out/target/product/oplus/ossi/boot.img```

## Это конечно хорошо, но вот проблемы
- [x] проблемы с шифрованием из-зп размера образа

## ПОМОГИТЕ
Я прошу помощи тк я уже не знаю что не хватает для успешной инициализации загрузки в систему и с шифрованием даты и с рабочим twrp и тд и тп. Тут есть лишние файлы, только я не знаю какие. Я жду любые предложения и исправления. Тестировать я буду тк загрузчик у меня разблокированный. Я уже собирал тврп, но для 12 андроида и у меня собралось и даже загрузилось, но всё зашифровано и загрузиться в систему не удавалось. Жду помощи!

## Контакты
4PDA QMS: [Another2281337](https://4pda.to/forum/index.php?showuser=5705704) — я
