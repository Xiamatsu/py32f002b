##  Обзор и тестирование семейства контроллеров PY32F002B,L020

### Введение
PY32F002B построены на одном и том же кристалле что и PY32L020.<br>
Отличий не много - для F002B не объявлено: поддержка HSI 48 MHz  и  режим  DeepStop<br>
PY32L020 - нет информации о продажах (только внутри Китая - наверно)<br>
По информации из конфигурационных файлов пакетов к данному семейству относятся также<br>
PY32F002X,PY32F002Z - ещё урезанные 8K/16K - Flash size;

Внутренняя переферия
```
Flash/RAM:  24K/3K 
Max Frequency: 48 MHz
  HSI - 24; 48 MHz (есть калибровочные константы)
  LSI - 32.768kHz (есть калибровочные константы)
        ( в RM - есть описание что есть ещё 38.4 kHz - константа)
  LSE - 0-1000kHz  (not in: qfn16, sop8 ) (PC1,PB7)
  HSE - Ext Clock (input) (1-32MHz) (PA6)
OTP: 128 byte
IWDG, SysTick
Timers (16b): Adv:1, GP:1, LP:1, 
1x USART, 1х SPI, 1x I2C
ADC 12bit (8+2ch) (0,75 Msps); 1-2 COMP
Hardware CRC-32 module
Low power modes: Sleep/Stop/DeepStop
User configuration Bootload region and code. (max 4K)
1.7 - 5.5 V

not PLL,DMA,RTC,WWDG,Bootloader
```

Дополнительные сведения по серии из [Factory Config](./FactoryConfig/README.md)

### Документация и программы

Информация есть на сайте компании PUYA (только лучше смотреть китайский вариант)<br>
Обновляется довольно часто

Также стараюсь актуальные версии выкладывать в облако
[DOCS - PY32](https://disk.yandex.ru/d/-6DTrL-0xZCn6g/%5B%20ARM%20%5D/PY32)

### Ревизии

Только замечена ревизия - 'A'

### Корпуса (только для  PY32F002B)
```
pinout - только одна версия '1'

qfn20(3x3)  e=0.4   (F002BF15Ux)
tssop20     e=0.65  (F002BF15Px)
sop20       e=1,27  (F002BF15Sx)
qfn16(3x3)  e=0.5   (F002BW15Ux)
sop16       e=1,27  (F002BW15Sx)
sop14       e=1,27  (F002BD15Sx)
sop8        e=1,27  (F002BL15Sx)
```

<img src="./images/py32f002b.png" alt="drawing" width="200"/>


### Демоплаты
```
1. EmbedFire PY32F002BF15U6TR  ( чип без опозновательных знаков )
   LED1      - Power
   LED2,3,4  - PA1,PA4,PA5
   Key RST   - Reset (PС0)
   KEY1,2    - PA3,PA0
   LSE       - opt (PC1,PB7)
   I/O       - 18 (PA0-7,PB0-7,PC0-1) 
```

<img src="./images/embedfire_py32f002bf15u6.png" alt="drawing" width="350"/>


### Ремапинг 

Скромный выбор ремапинга функций портов (альтернативные функции)<br>
  (обусловлено небольшим количеством периферии)<br>
Индивидуально можно настроить каждый пин до 8 функций.<br>
Шаблон возможных вариантов ( в разработке )<br>


### Программаторы, Утилиты, IDE 

Полностью подобно как и для семейства PY32F002A;F003;F030<br>
Firmware - только другое --> [Firmware 1.2.1](https://www.puyasemi.com/download_path/%E5%BA%93%E5%87%BD%E6%95%B0%E4%B8%8E%E4%BE%8B%E7%A8%8B/MCU%20%E5%BE%AE%E5%A4%84%E7%90%86%E5%99%A8/PY32F002B_Firmware_V1.2.1.zip) / на 22.09.2025



### Интересные тесты

#### Проверка что это один и тот-же кристалл

в FactoryConfig - есть калибровочная константа для 48 MHz HSI - надо пробовать запустить!