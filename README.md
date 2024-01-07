# ESP32 Arduino libraries
Compiled libraries for use in TeenAstro UniversalMainUnit enabling external crystal.
Using ESP Build Option CONFIG_ESP32S3_RTC_CLK_SRC_EXT_CRYS=y which is not selectable in Arduino.

## Install v4.4.6 of ESP-IDF
### Get ESP-IDF from github
```
makedir ~/esp
cd ~/esp
git clone -b v4.4.6 --recursive https://github.com/espressif/esp-idf.git esp-idf-v4.4.6
cd esp-idf-v4.4.6
```

### Modify ~/esp/esp-idf-v4.4.6/requirements.txt to compile with Linux Mint 21.2 using python 3.10
```
gdbgui==0.13.2.0; python_version < "3.10"
pygdbmi<=0.9.0.2; python_version > "3.9"
```

### Continue installation v4.4.6 of ESP-IDF
```
./install.sh
. ./export.sh
```

## Modify ~/.profile by adding path
```
export IDF_PATH=~/esp/esp-idf-v4.4.6
export PATH="$IDF_PATH/tools:$PATH"
```

## Install v4.4 of ESP Arduino Libary builder
### Get ESP Arduino Libary builder
```
cd ~
git clone -b release/v4.4 https://github.com/espressif/esp32-arduino-lib-builder
cd esp32-arduino-lib-builder
./build.sh
```

### Modify setting in ~/esp32-arduino-lib-builder/configs/
```
# CONFIG_ESP32S3_RTC_CLK_SRC_INT_RC is not set
CONFIG_ESP32S3_RTC_CLK_SRC_EXT_CRYS=y
# CONFIG_ESP32S3_RTC_CLK_SRC_EXT_OSC is not set
# CONFIG_ESP32S3_RTC_CLK_SRC_INT_8MD256 is not set'
```
### Build actual libaries and copy them to temp folder
./build.sh -c ~/esp32-arduino-lib-builder/temp

merge temp folder with copy of framework-espressif32 from ~.platformio/packages/framework-espressif32
upload to github

### Set reference in VS Code - Platformio.ini
```
platform = espressif32
platform_packages =
  platformio/tool-openocd-esp32
  platformio/framework-arduinoespressif32 @  https://github.com/ncleesattel/framework-arduinoespressif32#585b3bd
 
framework = arduino
```
