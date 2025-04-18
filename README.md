# TSC

Schema:

![Diagrama Bloc](Images/SCHEMA.png)


Proiectul a început cu realizarea schemei electrice, folosind componentele din biblioteca pusă la dispoziție. După conectare și etichetare, am rulat ERC, corectând majoritatea erorilor (etichete greșite, pini suprapuși), rămânând cu una nedetectată de Fusion.
După finalizarea schemei, am trecut la PCB, decupând placa conform cerințelor și amplasând componentele. Cea mai mare provocare a fost identificarea pieselor și ajustarea unor footprint-uri, precum cel al bobinei L1. După rutare și verificare DRC, am completat cu planurile de masă pe ambele straturi.

Arhitectură Generală a Sistemului
Modulul ESP32-C6-WROOM-1-N8 servește drept unitate principală de control, gestionând comunicația cu celelalte module prin protocoale standard precum I2C, SPI și GPIO. Alimentarea este oferită de o baterie Li-Po, gestionată de un sistem de încărcare și monitorizare a nivelului energetic.

Specificații Hardware

Modul principal – ESP32-C6

Microcontroler cu arhitectură RISC-V, suport Wi-Fi 6 și Bluetooth Low Energy

Interfețe suportate: SPI, I2C, UART, GPIO

Tensiune de alimentare: 3.3V

Sistem de alimentare și monitorizare

MCP73831 – controller pentru încărcarea bateriei Li-Po

MAX17048 – circuit pentru monitorizarea nivelului bateriei (fuel gauge) cu ieșire de alertă

XC6220A331MR – regulator de tensiune pentru stabilizarea la 3.3V

Senzori și ceas de timp real

BME688 – senzor multifuncțional pentru temperatură, umiditate, presiune și compuși volatili (VOC), comunicare I2C

DS3231SN – modul RTC cu funcție de alarmă, conectat prin I2C


Afișaj și memorie
Display e-paper – eficient energetic, ideal pentru afișarea informațiilor statice

W25Q512JVEIQ – memorie SPI externă de tip NOR, capacitate 64Mbit

Slot pentru card SD – conectare opțională prin magistrala SPI partajată

Protecție și comunicație

USBLC6 – protecție ESD pentru liniile USB

Diode Schottky – protecție împotriva supratensiunii

Conector USB-C – folosit atât pentru alimentare, cât și pentru comunicație serială

Elemente de interacțiune cu utilizatorul

Buton de resetare (RESET)

LED indicator – semnalizează starea încărcării




Configurația Pinilor ESP32-C6
Componentă	Pin ESP32	Funcție

BME688 – SDA	IO8	Linie date I2C

BME688 – SCL	IO9	Linie ceas I2C

DS3231SN – INT	IO10	Semnal întrerupere RTC

W25Q512 – CS	IO4	Selectare chip SPI Flash

E-paper – CS	IO3	Selectare chip SPI Display

SPI – CLK	IO5	Semnal ceas SPI

SPI – MOSI	IO6	Date de la master la slave

SPI – MISO	IO7	Date de la slave la master

MAX17048 – ALERT	IO11	Semnal alertă baterie

Buton RESET	IO0	Reset / Boot

SD Card – CS	IO2	Selectare chip card SD


## BOM (Bill Of Materials)

| Componenta                        | Link Cumparare                                                                                                   | Datasheet                                                                                          
|-----------------------------------|------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------
| 112A-TAAR-R03 ATTEND              | https://store.comet.srl.ro/Catalogue/Product/43497/                                                              | https://www.snapeda.com/parts/112A-TAAR-R03/Attend/datasheet/                                    
| BD5229G-TR                        | https://www.digikey.com/en/products/detail/rohm-semiconductor/BD5229G-TR/3663792                                 | https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf    
| ESP32 WROVER BME680 Sensor        | https://store.comet.srl.ro/Catalogue/Product/50164/                                                              | https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf   
| LED CHG_LED                       | https://ro.mouser.com/ProductDetail/Kingbright/KP-1608SURCK?qs=2JU0tDl2GZ3FuyEWfBV1%2Fg==                        | https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/datasheet/                                 
| Condensator C0402                 | https://ro.mouser.com/c/passive-components/capacitors/ceramic-capacitors/?q=CC0402                               | https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf                             
| Condensator Tant                  | https://ro.mouser.com/ProductDetail/KYOCERA-AVX/TAJW107M010RNJ?qs=Wtp%252Bf%2FAeVqIH8v1VxV%252B1Rg%3D%3D         | https://ro.mouser.com/datasheet/2/40/TAJ-3165264.pdf                                             
| Q1 DMG2305UX-7                    | https://www.digikey.com/en/products/detail/diodes-incorporated/DMG2305UX-7/4340666                               | https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf                                           
| RTC MODULE DS3231SN#              | https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda                                      | https://www.snapeda.com/parts/DS3231SN%23/Analog%20Devices/datasheet/                            
| ESP32 C6 WROOM-1-N8               | https://ro.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8?qs=8Wlm6%252BaMh8ST02Gmwp74cw%3D%3D    | https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif%20Systems/datasheet/                 
| FH34SRJ-24S-0.5SH(99)             | https://ro.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-24S-0.5SH99?qs=vcbW%252B4%252BSTIpKBl5ap9J8Fw%3D%3D | https://www.snapeda.com/parts/FH34SRJ-24S-0.5SH(99)/Hirose%20Connector/datasheet/                
| MAX 17048G+T10                    | https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda                                    | https://www.snapeda.com/parts/MAX17048G+T10/Analog%20Devices/datasheet/                          
| MBR0530 Schottky Diode            | https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=snap                                                 | https://www.snapeda.com/parts/MBR0530/ON%20Semiconductor/datasheet/                              
| MCP73831 Power Management         | https://www.snapeda.com/parts/MCP73831T-2ACI/OT/Microchip/datasheet/                                             | https://www.snapeda.com/parts/MCP73831T-2ACI/OT/Microchip/datasheet/                             
| PFMF.050.1                        | https://ro.mouser.com/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D                  | https://www.tdk-electronics.tdk.com/inf/75/db/CTVS_14/Surge_protection_series.pdf                
| PGB1010603MR                      | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda                                         | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/                          
| QWIIC_RIGHT_ANGLE CONNECTOR       | https://ro.mouser.com/ProductDetail/SparkFun/PRT-14417?qs=wd5RIQLrsJhgdz%2FpmZ%2F3GQ==                           | https://ro.mouser.com/datasheet/2/813/Qwiic_Connector_Datasheet-1223982.pdf                      
| Rezistenta R0402                  | https://grabcad.com/library/resistor-0402-1)                                                                     | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf
| SD0805S020S1R0                    | https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D               | https://ro.mouser.com/datasheet/2/40/schottky-3165252.pdf                                        
| Si1308EDL-T1-GE3 MOSFET           | https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay+Siliconix/view-part/?welcome=home&ref=eda                  | https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay%20Siliconix/datasheet/                     
| USB4110-GF-A                      | https://ro.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D                           | https://ro.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf       
| USBLC6-2SC6Y                      | https://ro.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y?qs=gNDSiZmRJS%2FOgDexvXkdow%3D%3D            | https://ro.mouser.com/datasheet/2/389/usblc6_2sc6y-1852505.pdf                                   
| W25Q512JVEIQ                      | https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda)                               | https://www.winbond.com/resource-files/W25Q512JV%20SPI%20RevB%2006252019%20KMS.pdf               
| XC6220A331MR-G                    | https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex                                                 | https://product.torexsemi.com/system/files/series/xc6220.pdf                                     
| 744043680 BOBINA                  | https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D               | https://www.we-online.com/components/products/datasheet/744043680.pdf                            

---

