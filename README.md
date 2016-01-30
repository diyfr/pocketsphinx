# pocketsphinx
Ou comment donner une oreille à votre rapsberry  

### Mise à jour des dépendances

`sudo su`
`apt-get upgrade`

Perso je préferre lancer dans un process à part vu que je suis en SSH. J'utilise screen (screen -r pour récupérer une vue en cours et Ctrl+A+D pour passer de la vue courante à la sortie principale)   

`apt-get install screen`  

Dépendances pour le build  
`sudo apt-get install bison libasound2-dev swig python-dev`

On récupère sphinx base et on le build (depuis screen)
```
wget http://sourceforge.net/projects/cmusphinx/files/sphinxbase/5prealpha/sphinxbase-5prealpha.tar.gz
tar -zxvf ./sphinxbase-5prealpha.tar.gz
mv sphinxbase-5prealpha sphinxbase
cd ./sphinxbase
./configure --enable-fixed
make clean all
make check
sudo make install
```
On récupère pocketsphinx  
```
wget http://sourceforge.net/projects/cmusphinx/files/pocketsphinx/5prealpha/pocketsphinx-5prealpha.tar.gz
tar -zxvf pocketsphinx-5prealpha.tar.gz
mv pocketsphinx-5prealpha pocketsphinx
cd ./pocketsphinx
./configure
make clean all
make check
sudo make install
```

A suivre...... en français bien sûr

```
pocketsphinx_continuous -dict /home/pi/pocketsphynx/usr/local/share/pocketsphinx/model/fra-fr/frenchWords62K.dic -lm  /home/pi/pocketsphynx/usr/local/share/pocketsphinx/model/fra-fr/french3g62K.lm.dmp -adcdev plughw:1,0 -verbose yes -samprate 16000 -inmic yes -hmm /home/pi/pocketsphynx/usr/local/share/pocketsphinx/model/fra-fr/fra-fr/

```


sources

[http://wiki.labomedia.org/index.php/Reconnaissance_vocale_avec_sphinx]  
[http://cmusphinx.sourceforge.net/wiki/raspberrypi]  
[http://sourceforge.net/projects/cmusphinx/files]  

Pour plus tart avec la ps3Eye  
[https://me.m01.eu/blog/2014/07/an-asoundrc-alsa-config-for-the-ps3-eye/]

