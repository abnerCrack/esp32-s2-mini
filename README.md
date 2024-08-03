# esp32-s2-mini
esp32-s2-mini 记录下折腾过程

## 准备工作
安装一些串口工具可以更方便的看到信息
```
brew install minicom lsusb
```
## 硬件准备
按住 `0` 点按 `rst`, 放开 `rst`键, 放开`0`键

## 下载镜像
https://www.micropython.org/download/LOLIN_S2_MINI/
## 确认设备被识别
执行 lsusb 可以看到 ESP32-S2
```
2024-08-03 18:51:48.243 system_profiler[8690:37823] SPUSBDevice: IOCreatePlugInInterfaceForService failed 0xe00002be
Bus 020 Device 000: ID 05ac:8290 Apple Inc. Bluetooth USB Host Controller
Bus 020 Device 007: ID 303a:0002 303a ESP32-S2  Serial: 0
Bus 000 Device 001: ID 1d6b:IWPT Linux Foundation USB 3.0 Bus
```
## 格式化
```
esptool.py --chip esp32s2 --port /dev/cu.usbmodem01  erase_flash          [18:53:48]

以下是打印信息:
esptool.py v3.0
Serial port /dev/cu.usbmodem01
Connecting...
Chip is ESP32-S2FH32
Features: WiFi, Embedded 4MB Flash, 105C temp rating
Crystal is 40MHz
MAC: 80:65:99:fb:2a:4a
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...

Chip erase completed successfully in 15.3s
Hard resetting via RTS pin...
ERROR: ESP32-S2FH32 chip was placed into download mode using GPIO0.
esptool.py can not exit the download mode over USB. To run the app, reset the chip manually.
To suppress this error, set --after option to 'no_reset'.
```
## 镜像写入
- 执行命令 写入镜像文件
- LOLIN_S2_MINI-20220618-v1.19.1.uf2 是镜像，保持在同一个目录执行
```
esptool.py --chip esp32s2 --port /dev/cu.usbmodem01 write_flash -z 0x1000 LOLIN_S2_MINI-20220618-v1.19.1.uf2

以下是打印信息:
esptool.py v3.0
Serial port /dev/cu.usbmodem01
Connecting...
Chip is ESP32-S2FH32
Features: WiFi, Embedded 4MB Flash, 105C temp rating
Crystal is 40MHz
MAC: 80:65:99:fb:2a:4a
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Compressed 2342400 bytes to 864490...
Wrote 2342400 bytes (864490 compressed) at 0x00001000 in 22.2 seconds (effective 843.9 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
ERROR: ESP32-S2FH32 chip was placed into download mode using GPIO0.
esptool.py can not exit the download mode over USB. To run the app, reset the chip manually.
To suppress this error, set --after option to 'no_reset'.
```
## 其他
驱动 https://cn.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads

