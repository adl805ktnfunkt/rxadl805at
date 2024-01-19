---

---
Erstellt von OE8CXC
--- 
# Vorraussetzungen
- [Raspberry PI 4](https://www.amazon.de/s?k=Raspberry+PI+4) inklusive Netzteil für die Stromversorgung
- [SDR-Stick](https://www.amazon.de/s?k=SDR+Stick)
- Stabile und möglichst dauerhafte Internetverbindung (mittels LAN-Kabel oder WLAN)
- Stromversorgung (230V Steckdose) am Ort, wo das *Software Defined Radio* aufgestellt wird
- [MicroSD-Karte](https://www.amazon.de/s?k=micro+sd+16+gb) mit mindestens 16 Gigabyte Speicherkapazität
	  ![Pasted image 20240119142426.png](Pasted image 20240119142426.png)
- [Adapter (Speicherkartenleser)](https://www.amazon.de/s?k=micro+sd+adapter+usb) für das Aufspielen des Systems

>[!info] Ungefährer Gesamtpreis
>~120€

---
# Weitere Informationen
- Für das Aufspielen der Image Datei (dem Linux-System inklusive vorinstalliertem OpenWebRx) eignet sich jeder gewöhnliche PC
  Die Installation dieser Anleitung wird mit Windows 10/11 durchgeführt
  - Als Antenne eignet sich jeder beliebige Draht, Gummiwurst (Stangerl) oder Stationsantenne
	  - Wenn man die Stationsantenne verwenden möchte und sich das Umstecken sparen möchte, eignet sich hierfür ein [Antennenumschalter](https://www.amazon.de/Albrecht-Antennenumschalter-7401-Metallgeh%C3%A4use-Koaxialsplitter-Schwarz/dp/B000VBE144/) am besten
- Die meisten SDR-Sticks haben einen *SMA-Male* Anschluss. [Entsprechende Adapter gibt es ebenfalls auf Amazon](https://www.amazon.de/s?k=SMA+Adapter)
- Man muss für die Portfreigabe (dass der SDR-Stick aus dem Internet erreichbar ist auf sein Router-Panel zugreifen können)
	  Anleitungen:
	- [FritzBox](https://avm.de/service/wissensdatenbank/dok/FRITZ-Box-7590/1_Benutzeroberflache-der-FRITZ-Box-aufrufen/)
	- [A1](https://www.a1.net/handyhilfe/device/modem/a1-wlan-box-zte-h268n/topic/einstellungen/zugriff-auf-die-administrationsseite)
- In dieser Anleitung wird immer wieder der Platzhalter **RUFZEICHEN** verwendet. Diesen bitte duch das eigene ersetzen! z. B. OE8CXC
- Diese Anleitung richtet sich primär an FritzBox Nutzer.
  Falls das Internet von wo anders bezogen wird, muss man selbst etwas nachschlagen.

---
# Anleitung
## 1. PI-Imager am PC installieren
https://www.raspberrypi.com/software/

## 2. Micro-SD-Karte mittels Adapter mit PC verbinden

## 3. Download des Images
https://github.com/luarvique/openwebrx/releases/
Die aktuellste Version auswählen und die .ZIP Datei downloaden.
Danach die ZIP-Datei entpacken um nun eine .ISO Datei zu haben.

## 4. PI-Imager starten und Image flashen
### Raspberry Pi Device
Hier auf **CHOOSE DEVICE** klicken und das jeweilige Modell auswählen

### Operating System
Auf **CHOOSE OS** klicken, ganz runterscrollen und **USE custom** auswählen

Nun die jeweilige .iso-Datei auswählen

### Storage
Hier sollte nun die SD-Karte erscheinen. Diese auswählen

>[!warning] Achtung!
>Unbedingt doppelt überprüfen, ob die ausgewählte SD-Karte tatsächlich die leere ist, da ansonsten alle Daten von einem anderen Speichermedium gelöscht werden könnten

### Nun auf NEXT klicken
![[Pasted image 20240119145459.png|400]]
Hier auf **EDIT SETTINGS** klicken

#### General
1. Set hostname
   **AKTIVIEREN**
   Auf **sdr-RUFZEICHEN** setzen z. B. sdr-oe8cxc
2. Set username and password
   **AKTIVIEREN**
   Benutzername: **RUFZEICHEN**
   beliebig (am besten notieren)
4. Falls eine Drahtlose Verbindung (WLAN) gewünscht ist, anhaken und hier die entsprechenden Daten eintragen
   Falls dieses Feld schon ausgefüllt und korrekt ist, besteht kein Handlungsbedarf
5. Set locale settings
   Muss nicht aktiviert werden

#### SERVICES
- Enable SSH: **AKTIVIEREN**
	- Use password authentication auswählen

#### OPTIONS
Die Standardwerte übernehmen (nichts ändern)

### Auf SAVE klicken
![[Pasted image 20240119150402.png|400]]
Hier **YES** auswählen

![[Pasted image 20240119150433.png|400]]
>[!danger] Überprüfen, ob dies **DEFINITIV** die leere MicroSD-Karte ist!
>>[!success] Falls dies der Fall ist
>>**YES** anklicken

Falls sich irgend ein Explorerfenster von Windows öffnet mit irgend einer Meldung, dies einfach ignorieren und warten, bis der PI-Imager sagt, dass man nun die MicroSD Karte entfernen kann

## 5. SD-Karte entfernen und in den Raspberry stecken
1. Zuerst die SD-Karte reinstecken
2. SDR-Stick in beliebigen USB-Port stecken
3. *Gegebenenfalls LAN-Kabel anschließen (bei drahtloser Verbindung nicht nötig!*
4. Netzteil beim Raspberry anschließen


## 6. Ca. 5 Minuten warten
Nun installiert sich das System und OpenWebRX+

*Man könnte diese Zeit für ein QSO z.B. am Dobratsch nutzen.

## 7. Mit Raspberry verbinden und Grundkonfiguration vornehmen
### Sicherstellen, das SSH am PC aktiviert ist
„Einstellungen“ > „Apps“ > „Apps & Features“ > „Optionale Features“ aufrufen und prüfen, ob der **OpenSSH Client** installiert ist – ggf. über „Feature hinzufügen“ installieren

### CMD öffnen
[WINDOWS TASTE]+[R]
"cmd" eingeben
[OK]

![Image](Pasted image 20240119151345.png)

### SSH-Verbindung aufbauen
```console
Microsoft Windows [Version 10.0.22621.3007]
(c) Microsoft Corporation. All rights reserved.

C:\Users\kamer>ssh oe8cxc@sdr-oe8cxc
The authenticity of host 'sdr-oe8cxc (192.168.178.56)' can't be established.
ED25519 key fingerprint is SHA256:FFwOCTweAFNxUqGfRJL7K8slPda50X6FwYdY/ZBiRs8.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
Hier `yes` eingeben und **ENTER** drücken

Nun das festgelegte Passwort eingeben (es wird nicht angezeigt)

Dann mit **ENTER** bestätigen

Nun sollte ganz unten `oe8cxc@sdr-oe8cxc:~ $` stehen

### Digimodes aktivieren
Dazu einfach `sudo install-softmbe.sh` in die Konsole eingeben, mit **ENTER** bestätigen und warten, bis der *Progress* bei 100% ist bzw. abgeschlossen ist

Nun sollte dort `Please reboot.` stehen

Dazu einfach `sudo reboot` eingeben und mit **ENTER** bestätigen

>[!warning] Konsolenfenster nicht schließen!

### Erneut einloggen
Etwa 2-3 Minuten warten und dann einfach die Pfeiltaste nach oben drücken, um wieder den Verbindungsbefehl erneut einzugeben und mit **ENTER** bestätigen

Falls dort "Connection timed out" steht, einfach noch ein paar Minuten warten

Nun wieder das Passwort eingeben und mit **ENTER** bestätigen

### OpenWebRX+ Benutzer anlegen
`sudo openwebrx admin adduser RUFZEICHEN` eingeben

Bei "Please enter the new password for RUFZEICHEN" ein sicheres Passwort auswählen (es kann auch das gleiche wie für das Login sein) und mit **Enter** bestätigen

Passwort erneut eingeben und mit **ENTER** bestätigen

## 8. Mit dem WebRX über den Browser verbinden
Dazu einfach einen beliebigen Browser öffnen (Chrome, Firefox, etc.) und in der URL-Leiste `http://sdr-RUFZEICHEN` eingeben

Nun sollte es so aussehen:
![[Pasted image 20240119153949.png]]

>[!info] Das Schlimmste ist geschafft!
>Nun könnte man schon lokal von seinem eigenen Netzwerk auf das SDR zugreifen.
>Natürlich wollen wir aber auch anderen Leuten, die außerhalb unseres Netzwerkes sind, den Zugriff gewähren.

## 9. Statische lokale IP für SDR vergeben
Für das Gerät **sdr-RUFZEICHEN**
- [Anleitung Fritzbox](https://avm.de/service/wissensdatenbank/dok/FRITZ-Box-7590/201_Netzwerkgerat-immer-die-gleiche-IP-Adresse-von-FRITZ-Box-zuweisen-lassen/)
- Bei A1 sollte dies auch unter den Einstellungen zu finden sein. Ansonsten ist dieser Schritt zwingend notwendig

## 10. Port freigeben (öffentliche IP)
Nun müssen wir unterscheiden, ob wir eine *reale, statische* (ohne NAT) oder eine *dynamische* IP-Adresse haben.
In den allermeisten Fällen ist es eine *dynamische* IP

>[!todo] Falls eine statische, öffentliche IPv4 Adresse besteht, kann dieser Link ignoriert werden.
>https://at.avm.de/service/wissensdatenbank/dok/FRITZ-Box-7590/30_Dynamic-DNS-in-FRITZ-Box-einrichten/

Nun den HTTP (80) Port freigeben: https://avm.de/service/wissensdatenbank/dok/FRITZ-Box-7490/893_Statische-Portfreigaben-einrichten/
Beim Gerät einfach **sdr-RUFZEICHEN** auswählen

## 11. Mittels externer IP versuchen, auf das SDR zuzugreifen
Auf diese Seite navigieren: https://www.wieistmeineip.at/
Beim Feld "Ihre IP-Adresse lautet:" die IP kopieren und oben in das URL-Feld des Browsers eingeben

Beispiel: `http://185.68.251.71/`
>[!warning] Unbedingt `http://` verwenden, da wir keine Verschlüsselung haben!

Nun sollte das gleiche Fenster wie bei `http://sdr-RUFZEICHEN` erscheinen

>[!success] Falls dies der Fall ist
>Ist alles fertig aufgesetzt.
>Jeder, der nun die öffentliche IP-Adresse weiß, kann auf das SDR zugreifen.

## 12. Am Web-Panel Einloggen und Einstellungen vornehmen
Oben rechts auf **Settings** klicken

Mit dem Rufzeichen und Passwort einloggen

Nun:
- General settings -> Hier die Einstellungen vornehmen, so wie sie dastehen und unten auf **Apply and save** klicken
- Background decoding -> "Enable background decoding services" aktivieren und unten auf **Apply and save** klicken
