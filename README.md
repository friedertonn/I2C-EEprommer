# I2C-EEprommer für den AC1

![Chipkartenleser](https://github.com/friedertonn/I2C-EEprommer/blob/main/Eagle_und_Fotos/Chipkartenleser.jpg?raw=true)

Gerd Staffen hat für den AC1-Computer eine Bibliothek in Z80-Assembler geschrieben, die eine universelle
I2C-Schnittstelle für verschiedene Programmiersprachen (Z80-Assembler, Basic, Pascal) bereitstellt.
Am AC1 werden die bislang nicht genutzten PIO-Pins B1 (SCL) und B4 (SDA) an der PIO 1, Port B genutzt. 
Bei einer Modifikation des Quelltextes können abweichende I/O-Adressen verwendet werden.

Die Bibliothek stellt folgende Funktionen bereit:

* INIT: Initialisierung der PIO und Software-Reset auf dem I2C-Bus 
* STARTB: Senden einer Startbedingung auf den I2C-Bus
* STOPB: Senden einer Stopbedingung auf den I2C-Bus
* TXBYTE: Senden eines Bytes auf den I2C-Bus und Empfang des ACK-Bits
* RXBYTE: Empfang eines Bytes vom I2C-Bus und Senden des ACK-Bits

Für den Anschluss von I2C-Komponenten wird eine Außenbeschaltung der PIO mit 
4 Widerständen empfohlen:

![Schaltplan](https://github.com/friedertonn/I2C-EEprommer/blob/main/Eagle_und_Fotos/i2c_eeprommer.png?raw=true)

Auf der Basis dieser Bibliothek wurde ein Programmiersoftware für I2C-EEproms in Z80-Assembler
geschrieben, welches sich in der Bedienung an den EEprommer von Bernd Jahn
[http://bernd-jahn.de](http://bernd-jahn.de)
anlehnt. Es werden I2C-EEproms von 128 Byte bis 32 KByte unterstützt:

<table style="border-collapse: separate;
  border-spacing: 0;
  padding: 5px;">
    <tbody>
    <tr style="background-color: lightblue" align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;"><b>lfd. Nr.</b></td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2"><b>EEPROM Typ</b> </td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2"><b>Speicherkapazität</b> </td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2"><b>Anzahl der Pages</b> </td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2"><b>Page-Größe</b> </td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">1</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C01</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">128 Byte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">128</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">1 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">2</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C02</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256 Byte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">1 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">3</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C04</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">512 Byte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">2 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">4</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C08</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">1 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">4 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">5</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C16</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">2 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">8 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">6</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C32</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">4 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">128</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">32 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">7</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C64</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">8 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">32 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">8</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C128</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">16 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">64 Byte</td>
    </tr>
    <tr align="center">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">9</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">AT24C256</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">32 KByte</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">512</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">64 Byte</td>
    </tr>
    </tbody>
</table>

Folgende Funktionen sind implementiert:

* Schreiben eines EEproms ab einer vorgegebenen RAM-Adresse
* Lesen eines EEproms in einen RAM-Adressbereich
* Vergleichendes Lesen mit einem RAM-Adressbereich
* Feststellung der EEprom-Adresse, falls sie von 50h abweicht
* Memory-Dump auf dem Bildschirm

Die Startadresse des Programms ist 2000h. Sie kann bei Bedarf im Quellcode geändert werden.
Getestet wurde mit I2C-EEproms im DIP-8 Gehäuse und als Chipkarte.
Für 2 MHz CPU-Takt liegt die Schreib- und Lesegeschwindigkeit bei 1,5 KByte/Sekunde.
Ein 32 KByte EEPROM wird in zirka 21 Sekunden geschrieben bzw. gelesen. 

Programme und Dateien:

<table style="border-collapse: separate;
  border-spacing: 0;
  padding: 5px;">
    <tbody>
    <tr style="background-color: lightblue">
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;"><b>Name</b></td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2"><b>Beschreibung</b> </td>
    </tr>
    <tr>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">EEPR13-2.Z80</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">EEprommer V1.3 Programm mit Z80-Header</td>
    </tr>
    <tr>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">EEPR13-2.BIN</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">EEprommer V1.3 Programm, Startadresse 2000h</td>
    </tr>
    <tr>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">EEPR13-6.Z80</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">EEprommer V1.3 EDAS*4-Quellcode mit Z80-Header</td>
    </tr>
    <tr>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">EEPR13-6.BIN</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">EEprommer V1.3 EDAS*4-Quellcode, Adresse 6000h</td>
    </tr>
    <tr>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;">EEPR13-6.LST</td>
        <td style="border: 1px solid #bbb; border-bottom: 1px solid #bbb; padding: 10px 15px 10px 15px;" colspan="2">EEprommer V1.3 EDAS*4-Quellcode als ASCII-Text</td>
    </tr>
    </tbody>
</table>
