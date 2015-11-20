Liste des périphériques USB   
```
$lsusb
.....
Bus 001 Device 003 : ID 1415:2000 Nam Tai E&E Products Ltd. or OmniVision Technologies, Inc. Sony 
```
Liste des devices d'enregistrement audio  
```
$arecord —list-devices
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
$amixer cset numid=3 1
$aplay test.wav
```



to read  
[https://github.com/tdicola/DemoManMonitor]  
[http://renatocunha.com/blog/2012/04/playstation-eye-audio-linux/]  


