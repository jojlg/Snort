# Qu'est ce que `Snort`

Snort est le premier système de prévention des intrusions (IPS) open source au monde. Snort IPS utilise une série de règles qui aident à définir l’activité réseau malveillante et utilisent ces règles pour trouver les paquets qui leur correspondent, et génère des alertes pour les utilisateurs.

Snort peut également être déployé en ligne pour arrêter ces paquets. Snort a trois utilisations principales : En tant que renifleur de paquets comme tcpdump, en tant qu’enregistreur de paquets — ce qui est utile pour le débogage du trafic réseau, ou il peut être Utilisé comme un système complet de prévention des intrusions sur le réseau. Snort peut être téléchargé et configuré pour et à des fins professionnelles.



# Étape 1 :
## Installer les dépendances nécessaires :

```bash
sudo apt update
sudo apt upgrade -y
```

```bash
sudo apt install -y build-essential libpcap-dev libpcre3-dev zlib1g-dev \
libluajit-5.1-dev libtins-dev libhwloc-dev cmake pkg-config git flex bison \
libdumbnet-dev libssl-dev libnghttp2-dev libcurl4-openssl-dev \
libgoogle-perftools-dev libhs-dev libsafec-dev uuid-dev libunwind-dev \
liblzma-dev libnetfilter-queue-dev libmnl-dev autotools-dev autoconf libtool
```

# Étape 2 : Installation de la bibliothèque libdnet

* Cloner et installer libdnet :

```bash
git clone https://github.com/dugsong/libdnet.git
cd libdnet
./configure
make
sudo make install
sudo ldconfig
```

# Étape 3 : Installation de DAQ (Data Acquisition Library)
* Cloner et installer DAQ :
```bash

git clone https://github.com/snort3/libdaq.git
cd libdaq
./bootstrap
./configure
make
sudo make install
sudo ldconfig
```

# Étape 4 : Installation de Snort 3
* Cloner le dépôt Snort 3 :

```bash
cd ~
git clone https://github.com/snort3/snort3.git
cd snort3
```

## Configurer Snort 3 :

```bash
./configure_cmake.sh --prefix=/usr/local --enable-tcmalloc
```
* Si vous rencontrez des erreurs liées à TCMalloc, vous pouvez omettre --enable-tcmalloc : 

```bash
./configure_cmake.sh --prefix=/usr/local
```

## Compiler Snort 3 :

```bash
cd build
make -j$(nproc)
```
## Installer Snort 3 :

```bash
sudo make install
```

# Étape 5 : Post-installation
* Mettre à jour le cache des bibliothèques partagées :

```bash
sudo ldconfig
```

## Vérifier l'installation de Snort :

```bash
snort -V
```