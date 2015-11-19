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
