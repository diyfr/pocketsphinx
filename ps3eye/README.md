#MEMO DES COMMANDES
[LE lien pour arecord](http://xmodulo.com/how-to-capture-microphone-input-to-wav-format-file.html)  
Liste des périphériques USB    
```
$lsusb
.....
Bus 001 Device 003 : ID 1415:2000 Nam Tai E&E Products Ltd. or OmniVision Technologies, Inc. Sony 
```

Liste des cartes sons  
```
cat /proc/asound/cards   
 0 [ALSA           ]: bcm2835 - bcm2835 ALSA   
                      bcm2835 ALSA   
 1 [CameraB409241  ]: USB-Audio - USB Camera-B4.09.24.1   
                      OmniVision Technologies, Inc. USB Camera-B4.09.24.1 at usb-20980000.usb-1.3, hi   
```

Liste des devices d'enregistrement audio  
```
$arecord --list-devices
**** Liste des Périphériques Matériels CAPTURE ****
carte 1: CameraB409241 [USB Camera-B4.09.24.1], pÃ©riphÃ©rique 0: USB Audio [USB Audio]
  Sous-périphériques: 1/1
  Sous-périphérique #0: subdevice #0
```


On teste l'enregistrement ici 10secondes dans le fichiers test wav  
```
arecord -d 10 -D plughw:1,0 test.wav
```  
On règle le volume de la sortie audio (ici jack =1 ) puis on écoute notre fichier wav
```
$amixer cget numid=3 1
$aplay test.wav
```
Niveau enregistrement  
```
arecord -vv /dev/null -r 16000 -f S16_LE -c 4 -D plughw:1,0 /dev/null < /dev/null
```  

pssshhhhhhhh !!! ;(  
dmesg  
```
[ 1641.442745] usb 1-1.2: new high-speed USB device number 5 using dwc_otg
[ 1641.545766] usb 1-1.2: New USB device found, idVendor=1415, idProduct=2000
[ 1641.545806] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=0
[ 1641.545829] usb 1-1.2: Product: USB Camera-B4.09.24.1
[ 1641.545846] usb 1-1.2: Manufacturer: OmniVision Technologies, Inc.
[ 1641.561380] gspca_main: ov534-2.14.0 probing 1415:2000
[ 1643.546187] usb 1-1.2: current rate 17250 is different from the runtime rate 16000
[ 1643.549029] usb 1-1.2: 3:1: cannot get min/max values for control 2 (id 3)
```
!!!! cannot get min/max values for control 2   
TODO :
Bon on essaye avec pulseaudio suivant ce tuto  
[https://coderwall.com/p/_a_scg/how-to-setup-speech-recognition-using-a-raspberrypi-pocketsphinx-ps3eye]  
```
$apt-get install pulseaudio
```
ensuite on crée le fichier de configuration  alsa pour pulseaudio
```

sudo \cp -pf /etc/asound.conf /etc/asound.conf.ORIG 
sudo echo 'pcm.pulse {
    type pulse
}

ctl.pulse {
    type pulse
}

pcm.!default {
    type pulse
}

ctl.!default {
    type pulse
}' > /etc/asound.conf

reboot

pactl set-card-profile alsa_card.usb-OmniVision_Technologies__Inc._USB_Camera-B4.09.24.1-01-CameraB409241 input:analog-4-channel-input
```
tiens ce fichier me parait bien rempli 
/usr/share/pulseaudio/alsa-mixer/profile-sets/default.conf 
```

[Mapping analog-4-channel-input]
# Alsa doesn't currently provide any better device name than "hw" for 4-channel
# input. If this causes trouble at some point, then we will need to get a new
# device name standardized in alsa.
device-strings = hw:%f
channel-map = aux0,aux1,aux2,aux3
priority = 1
direction = input
```
donc normalement cela devrait fonctionner

```
alsamixer
```

deux voies ...   







see /usr/share/alsa/conf.d  ../cards     
to read  
[http://www.pobot.org/Son-et-image-avec-la-Sony-PS3-Eye.html]  
[https://github.com/tdicola/DemoManMonitor]  
[http://renatocunha.com/blog/2012/04/playstation-eye-audio-linux/]  
[https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/886449]  
[https://www.raspberrypi.org/forums/viewtopic.php?f=38&t=15851&p=160394#p160394]  
[https://coderwall.com/p/_a_scg/how-to-setup-speech-recognition-using-a-raspberrypi-pocketsphinx-ps3eye]  

Localisation par microphone : [http://www.pobot.org/Localisation-du-son-sur-Raspberry-Pi.html]  
Un truc de malade hark mais en japonais [http://www.hark.jp/wiki.cgi?page=PlayStationEyeMain]  


