# TSC-EBookReader
1. Introducere si scop
OpenBook este un dispozitiv avansat construit in jurul microcontrolerului ESP32-C6, avand mai multi senzori si interfete. Acest dispozitiv este conceput pentru a oferi o experienta de citire electronica eficienta, cu un consum redus de energie si multiple functionalitati.

2. Diagrama bloc
   ```
           +------------------+
           |     Baterie       |
           +--------+---------+
                    |
                    v
           +------------------+
           |   Circuit Incarcare|
           | (Charging IC)      |
           +--------+---------+
                    |
                    v
           +------------------+
           |       LDO        |
           |   (3.3V Output)  |
           +--------+---------+
                    |
    +--------------+-------------------+-------------------+
    |              |                   |                   |
    v              v                   v                   v
```
+--------+   +-------------+   +----------------+   +-----------------+
| ESP32  |<->|    Display   |<->|    BME688      |<->|  Butoane tactile |
|  -C6   |   |   (SPI: 4W)  |   |   (I2C Bus)    |   | (GPIO + RC)      |
+--------+   +-------------+   +----------------+   +-----------------+
     |               ^                 ^                     ^
     |               |                 |                     |
     |               |           Rezistente Pull-up      Circuit RC de 
     |               |                                      debounce
     v               |
+---------------------------+
|     Conector USB-C        |
| (Date USB ↔ ESP32 USB)    |
| (Protectie ESD & Terminare)|
+---------------------------+
```
   
4. BOM (Bill of Materials)
Lista de materiale (BOM)
Componenta	Link achizitionare	Link Datasheet
112A-TAAR-R03 ATTEND	https://store.comet.srl.ro/Catalogue/Product/43497/	https://www.snapeda.com/parts/112A-TAAR-R03/Attend/datasheet/
BD5229G-TR	https://www.digikey.com/en/products/detail/rohm-semiconductor/BD5229G-TR/3663792	https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf
ESP32 WROVER BME680 Sensor	https://store.comet.srl.ro/Catalogue/Product/50164/	https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf
LED CHG_LED	https://ro.mouser.com/ProductDetail/Kingbright/KP-1608SURCK?qs=2JU0tDl2GZ3FuyEWfBV1%2Fg==	https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/datasheet/
Condensator C0402	https://ro.mouser.com/c/passive-components/capacitors/ceramic-capacitors/?q=CC0402	https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf
Condensator Tant	https://ro.mouser.com/ProductDetail/KYOCERA-AVX/TAJW107M010RNJ?qs=Wtp%252Bf%2FAeVqIH8v1VxV%252B1Rg%3D%3D	https://ro.mouser.com/datasheet/2/40/TAJ-3165264.pdf
Q1 DMG2305UX-7	https://www.digikey.com/en/products/detail/diodes-incorporated/DMG2305UX-7/4340666	https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf
RTC MODULE DS3231SN#	https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda	https://www.snapeda.com/parts/DS3231SN%23/Analog%20Devices/datasheet/
ESP32 C6 WROOM-1-N8	https://ro.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8?qs=8Wlm6%252BaMh8ST02Gmwp74cw%3D%3D	https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif%20Systems/datasheet/
FH34SRJ-24S-0.5SH(99)	https://ro.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-24S-0.5SH99?qs=vcbW%252B4%252BSTIpKBl5ap9J8Fw%3D%3D	https://www.snapeda.com/parts/FH34SRJ-24S-0.5SH(99)/Hirose%20Connector/datasheet/
MAX 17048G+T10	https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda	https://www.snapeda.com/parts/MAX17048G+T10/Analog%20Devices/datasheet/
MBR0530 Schottky Diode	https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=snap	https://www.snapeda.com/parts/MBR0530/ON%20Semiconductor/datasheet/
ESP32 WROVER MCP73831 Power Management	]https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home	https://www.snapeda.com/parts/MCP73831T-2ACI/OT/Microchip/datasheet/
PFMF.050.1	https://ro.mouser.com/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D	https://www.tdk-electronics.tdk.com/inf/75/db/CTVS_14/Surge_protection_series.pdf
PGB1010603MR	https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda	https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/
QWIIC_RIGHT_ANGLE CONNECTOR	https://ro.mouser.com/ProductDetail/SparkFun/PRT-14417?qs=wd5RIQLrsJhgdz%2FpmZ%2F3GQ==	https://ro.mouser.com/datasheet/2/813/Qwiic_Connector_Datasheet-1223982.pdf
Rezistență R0402	https://grabcad.com/library/resistor-0402-1)	https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf
SD0805S020S1R0	https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D	https://ro.mouser.com/datasheet/2/40/schottky-3165252.pdf
Si1308EDL-T1-GE3 MOSFET	https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay+Siliconix/view-part/?welcome=home&ref=eda	https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay%20Siliconix/datasheet/
USB4110-GF-A	https://ro.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D	https://ro.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf
USBLC6-2SC6Y	https://ro.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y?qs=gNDSiZmRJS%2FOgDexvXkdow%3D%3D	https://ro.mouser.com/datasheet/2/389/usblc6_2sc6y-1852505.pdf
W25Q512JVEIQ	]https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda)	https://www.winbond.com/resource-files/W25Q512JV%20SPI%20RevB%2006252019%20KMS.pdf)
XC6220A331MR-G	https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex	https://product.torexsemi.com/system/files/series/xc6220.pdf
744043680 BOBINA	https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D	https://www.we-online.com/components/products/datasheet/744043680.pdf
   
5. Functionalitatea hardware
ESP32-C6 reprezinta componenta principala a proiectului OpenBook, oferind conectivitate Wi-Fi 6 si Bluetooth 5.0 LE. Datorita conectivitatii wireless integrate si a numarului mare de pini GPIO, microcontrollerul permite interfatarea cu diverse componente periferice, asigurand flexibilitate si performanta ridicata.
Afisajul e-paper este conectat la ESP32-C6 prin interfata SPI si utilizeaza driver-ul BD5229G-TR pentru a gestiona tensiunile necesare functionarii. Alimentarea afisajului este controlata prin MOSFET-uri, permitand oprirea completa a acestuia atunci cand nu este utilizat, ceea ce contribuie la eficienta energetica a dispozitivului.
Pentru monitorizarea conditiilor de mediu, proiectul utilizeaza senzorul BME688, capabil sa masoare temperatura, umiditatea, presiunea si calitatea aerului (VOC). Acesta comunica cu ESP32-C6 prin intermediul interfetei I2C si functioneaza la o tensiune de 3.3V, oferind date precise.
Gestionarea energiei este realizata printr-un circuit de incarcare bazat pe MCP73831, care permite incarcarea bateriei cu un curent de pana la 500mA. Starea bateriei este monitorizata cu modulul MAX17048G+T10, care comunica prin aceeasi interfata I2C si furnizeaza informatii detaliate despre nivelul de incarcare si starea bateriei.

6. Alocarea pinilor ESP32-C6
Componenta	Pini ESP32	Interfata	Observatii
Afisaj E-Paper	IO12, IO11, IO5, IO4	SPI	Control si resetare afisaj
Senzor BME688	IO8, IO10	I2C	Date de mediu (temperatura, umiditate)
Card SD	IO7	SPI	Stocare externa
Modul RTC	IO8, IO10	I2C	Ceas in timp real, partajeaza I2C
Serial USB	IO16, IO17	UART	Programare si depanare

7. Informatii suplimentare relevante
TP-urile au fost plasate in mod optim langa marginile placii si in apropierea componentelor esentiale pentru a permite acces facil la depanare si testare.
Pentru diodele montate pe suprafata, dimensiunea initiala a pad-urilor era prea mica, ceea ce putea crea probleme la lipire. Dimensiunea a fost ajustata pentru a asigura o conexiune electrica fiabila si o asamblare mai usoara.
Rutarea traseelor a fost realizata pe ambele straturi ale PCB-ului (superior si inferior), asigurand o distributie eficienta a semnalelor si a alimentarii. Planul de masa (GND) a fost aplicat pe ambele straturi pentru a optimiza performanta electrica.
