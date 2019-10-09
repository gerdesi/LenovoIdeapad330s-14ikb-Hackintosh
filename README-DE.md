# Lenovo Ideapad 330s-14IKB Hackintosh
Ein vollständiger Guide zum aufsetzen eines Lenovo Ideapad 330s-14IKB Hackintosh.

### Unterstützt mich gerne mit einer kleinen Spende ganz unten. :)

## WICHTIG: Bitte lest euch die Info über macOS Updates am ende der Seite durch!

#### Der Guide ist verfügbar auf...

[English](README.md) | [Deutsch](README-DE.md)

***DISCLAIMER***
Dieses Projekt ist noch in der beta/testphase.
Ihr macht das auf eigene Gefahr, ich übernehme keine Verantwortung für Schäden die auftreten könnten.

## Konfiguration meines Ideapad:
- CPU: i3-8130U @ 2.21GHz
- 4GB RAM
- Intel UHD 620
- Display: HD 1366 x 768
- 128 GB SSD
- WiFi and Bluetooth card: Lenovo Branded Broadcom BCM94352Z

## Probleme
- Manchmal funktioniert der Ruhezustand nicht richtig, wenn man den deckel zu macht (Extrem zufällig und unregelmäßig)
- Tastatur Mute Shortcut (Zeigt zwar an, dass der ton aus ist, ist er aber nicht)
- iMessage und Facetime (Funktioniert mittlerweile... Keine Ahnung warum...)
- Trackpad Gesten funktionieren (noch) nicht richtig. Vielleicht finde ich einen Fix dafür
- Ein ACPI Error beim booten. Kann ignoriert werden. (Vielleicht kann den jemand fixen?) | Einfach ohne Verbose mode (-v) booten, dann sieht man es nicht.

## Fangen wir an!

### Was du brauchst:
- Lenovo Ideapad 330s-14IKB (i3 or i5 Model)
- macOS oder OS X heruntergeladen aus dem Mac App Store
- 8GB USB Stick
- Tastatur, Maus und einen USB Hub (Die eingebauten Sachen funktionieren nach der Installation)

### BIOS Einstellungen
- Auf aktuellstes BIOS updaten
- Wenn deins mit einer Intel Optane verbaut ist, muss diese deaktiviert werden und der AHCI Legacy mode verwendet werden (NICHT RST!).
- Secureboot deakivieren und Optimized defaults für Windows 10 entfernen
- Virtualisierung ausschalten

## 1. Installationsstick erstellen (Du brauchst einen Mac dafür. | Du hast keinen Mac? [Schau dir dieses Tutorial an](MacVM.md))
Als erstes den 8GB (oder mehr) Stick am Mac anstecken.

Diskutil öffnen und den Stick zu macOS Journaled formatieren und "install_osx" nennen.

macOS Mojave aus dem Mac App Store herunterladen. Wenn es heruntergeladen ist, den Install-Stick mit folgendem Command erstellen:

``` sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction ```

Das wars schon mit Teil 1!

## 2. Clover installieren
Neuste Clover version von [hier](https://sourceforge.net/projects/cloverefiboot/) herunterladen.<br>
Den Clover Bootloader installer öffnen, auf Continue klicken, zustimmen, Continue. Wenn du zum "Installation Type" Screen kommst, auf "Change Install Location" klicken.<br>
Hier den USB Stick auswählen, der jetzt normalerweise "install_osx" heißen sollte.<br>
Dann auf "Customize" klicken. Bitte überprüfen, ob diese optionen ausgewählt sind:<br>
- Clover for UEFI booting only
- Install Clover in the ESP
- Themes
- UEFI Drivers (Under Drivers, uncheck SMCHelper-64, as we will be using VirtualSMC)
**Installieren drücken**

## 3. Wichtige Treiber und Kexts übertragen (Geh zu den releases für alle Dateien)
Kopiere die Dateien aus dem "Drivers64UEFI" (NvmExpressDxe-64 wird nur benötigt wenn ein NVMe Drive vorhanden ist) und "kexts" auf den USB stick wo clover installiert wurde.<br>
Ersetze die config.plist mit der aus meinen Dateien

## 4. Installation

### Schritt 1:
Schließe den USB Stick and den Laptop an, schalte ihn an. Wen der Laptopbildschirm angeht, ganz oft F1 drücken um ins BIOS zu kommen.<br>
Ändere die Bootreihenfolge so, dass der Stick an erster Stelle geht. Speichern und BIOS verlassen. <br>
Jetzt sollte dich das Gerät zum Clover Bootloader Menü bringen. Hier Install macOS Mojave (USB Drive) auswählen und Enter drücken. <br>
Jetzt sollte der Installer booten und dich ins Installer Menü bringen.

### Schritt 2:
Im Installer Menü, Diskutility auswählen und die Festplatte auswählen, auf der macOS installiert werden soll, diese zu Mac OS Journaled formatieren und diese zu "macOS" umbenennen. Wenn der vorgang abgeschlossen ist, Disktutility verlassen.<br>
Jetzt macOS Mojave installieren klicken, den Lizenzbestimmungen zustimmen, die Festplatte zur installation auswählen. Jetzt beginnt der 1. Teil der installation. Dieser sollte um die 5 Minuten dauern.

### Schritt 3:
Der Laptop wird automatisch neustarten, wenn Teil 1 abgeschlossen ist. Sobald Clover wieder erscheint, diesmal die "macOS" Partition auswählen. Hier wird dann mit Teil 2 der installation fort gefahren. Es wird dann eine Leiste mit der Verbleibenden Zeit angezeigt.<br>
Info: Manchmal kann es sein, dass sobald die verbleibende Zeit unter dem Apple Logo angezeigt wird, der Laptop automatisch neustartet. Wenn das passiert, einfach wieder "macOS" zum booten verwenden.<br>
Wenn die installation abgeschlossen ist, kommst du zu Teil 3 der installation. - Dem First Boot User setup.

### Schritt 4:
Sprache auswählen, Fortfahren, Verbindung zum Internet ist erst mal optional.<br>
Wenn der Teil zum einloggen in iCloud kommt, das noch überspringen, wenn du iMessage und FaceTime einstellen willst.

## 5. Post Installation
### Schritt 1:
Terminal öffnen und folgenden Befehl eingeben:

``` sudo spctl --master-disable ```

Das ermöglicht es dir, Apps auserhalb des Appstores zu installieren.

### Schritt 2:
Clover Bootloader installer öffnen und Clover auf der macOS Platte installieren.<br>
Der Vorgang ist genau der gleiche wie beim Installer, außer dass diesmal statt dem USB Stick, die macOS Platte gewählt wird. Außerdem müssen die Dateien aus "Drivers64UEFI" vom Stick in den "Drivers64UEFI" auf der Platte geschoben werden.

### Schritt 3:
Jetzt müssen die ganzen benötigten Kexts installiert werden.
Alle kexts sollten nach "/Library/Extension" installiert werden. Der einfachste Weg dafür ist mit HackinTool. [Guide](https://www.tonymacx86.com/threads/guide-installing-3rd-party-kexts-el-capitan-sierra-high-sierra-mojave.268964/). Die Kexts sind im "Library/Extensions" ordner in meinem Download.<br>
Die Kexts AppleIntelLpssI2C.kext und AppleIntelLpssI2CController.kext aus dem /System/Library/Extensions Ordner löschen oder mit Clover Configurator deaktivieren. (Cache Rebuilden mit HackinTool).<br>
Neustarten und F4 bzw. Fn+F4 im Bootloader drücken. (Das generiert deine DSDT und SSDT files)<br>
Starte macOS und kopiere meine DSDT und SSDT-PNLF aus meinem Clover Ordner nach EFI/CLOVER/ACPI/patched (Du solltest am besten deine eigenen erstellen, aber meine sollten auch funktionieren.)<br>

Das wars! Optimalerweiße, wenn du die selbe Konfiguration wie ich hast, bist du fertig. Aber wenn Probleme auftreten würde ich den Vanilla Weg nehmen und jeden Fehler einzeln Fixen (Guides sind in meinem Ordner).

### Schritt 4:
HackinTool verwenden um Hibernation zu fixen und USB Port patching durchzuführen. (Guide im Ordner)

## macOS Updaten
Falls Apple mal wieder ein neues Mojave Update veröffentlicht (was sie gerade gemacht haben), wie z.B. macOS 10.14.6 Supplimental Update, einfach installieren. Wenn das Update fertig ist, kann es sein, dass das Trackpad nicht mehr funktioniert. Falls das der Fall ist, einfach Schritt 2 und 3 der Post Installation durchführen. Nach einem Neustart sollte dann alles wieder funktionieren.

## macOS Mojave Supplemental Update 2
Dieses Update scheint das Trackpad inkompatibel zu machen. Ich habe das update getestet, aber es hat nicht mehr funktioniert, obwohl ich auch meine Update schritte durchgeführt habe.

**Bitte Updatet macOS nicht auf diese Version bis ein Fix gefunden wurde!**

Wenn ihr dennoch updaten wollt, macht bitte ein Time Machine Backup vor dem Update, um Datenverlust bzw. die Funktionalität nicht zu verlieren!

## Credits:
- Danke an [RehabMan](https://www.tonymacx86.com/members/429483/) für seine Guides.
- Danke an [muchmore](https://www.tonymacx86.com/members/698774/) für seinen Battery Patch und [Whab](https://www.tonymacx86.com/members/2096263/) für seine emfehlungen im 15IKB Thread auf tonymacx86.
- Danke an [Sniki](https://www.tonymacx86.com/members/1501160/) für seinen V330 Guide.

## Haste mal 'n Euro?
- [PayPal](https://www.paypal.com/paypalme2/quiiddev)
