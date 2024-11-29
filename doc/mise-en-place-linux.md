 <a href="../README.md">
  <img src="../assets/button/home_page.png" alt="Home page" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_rt.png)

# Mise en place Linux

![border](../assets/line/line-pink-point_l.png)

## Sommaire

- [Introduction](#introduction)

![border](../assets/line/border_deco_rb.png)

# Introduction

![border](../assets/line/line-pink-point_r.png)

```
sudo apt update
sudo apt upgrade
```

- Dans un premier temps nous allons mettre à jour nos paquets

- Puis nous allons installer les dépendances nécessaires

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

- Ajouter la clé GPG officielle de Docker

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

- Ajouter le dépôt Docker à nos sources

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- et enfin nous allons instalelr docker

```
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

- Vérifer l'installation

```
sudo docker --version
```

Ajouter votre utilisateur au groupe Docker (facultatif)

```
sudo usermod -aG docker $USER
newgrp docker

```

## Vérifiez que Docker est en cours d’exécution

Dans le terminal, nosu executons :

```
sudo systemctl status docker
```

ce qui nous donne le resultat suivant

```
docker.service - Docker Application Container Engine
    Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: e>
    Active: active (running) since Fri 2024-11-29 13:40:46 CET; 9min ago
TriggeredBy: ● docker.socket
      Docs: https://docs.docker.com
  Main PID: 1652 (dockerd)
     Tasks: 14
    Memory: 100.2M (peak: 102.6M)
       CPU: 536ms
    CGroup: /system.slice/docker.service
            └─1652 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/cont
```

- **Loaded**: Cela signifie que le fichier de configuration du service Docker a été trouvé et chargé depuis /usr/lib/systemd/system/docker.service.

- **enabled:** Le service est configuré pour démarrer automatiquement au démarrage du système.

- **Active**: active (running) since Fri 2024-11-29 13:40:46 CET; 9min ago

- **Main PID:** Le processus principal du démon Docker (dockerd) est identifié par le numéro de processus 1652.
- **Tasks:** Docker gère actuellement 14 tâches ou threads.
- **Memory:** Docker utilise 100.2 Mo de mémoire.
- **CPU:** Il a consommé 536 ms de temps processeur jusqu'à présent.

### EXCECUTER DOCKER

- Nous allons l'exécuter avec sudo

- Vous pouvez exécuter Docker avec sudo pour vérifier que cela fonctionne avec les privilèges administratifs :

```
sudo docker run hello-world
```

## Explications détaillées

### Téléchargement de l'image "hello-world" :

Docker a cherché l'image hello-world localement. Comme elle n'était pas présente, Docker l'a téléchargée depuis Docker Hub, le registre d'images par défaut.

### Création d'un conteneur :

Une fois l'image téléchargée, Docker a créé un conteneur basé sur cette image.

### Exécution du conteneur :

Le conteneur a exécuté un petit programme qui produit le message "Hello from Docker!".

Affichage de la sortie : Docker a redirigé la sortie de ce programme vers votre terminal, confirmant que tout fonctionne correctement.

## Lancer un conteneur interactif Ubuntu :

- à présent nous allons Tester un environnement Ubuntu isolé :

```
docker run -it ubuntu bash
```

- Mais cela nes sembe pas focntionner alors nous allons passer par quelques étapes subsidiaires

### Etape 1 : Ajouter l'utilisateur au groupe Docker

Ajouter votre utilisateur au groupe docker :

```
sudo usermod -aG docker $USER
```

- Confirmez que le groupe Docker existe : si nous voulons etre sur que le groupe docker est actif

```
❯ getent group docker
docker:x:995:meodel
```

- Puis pour que les changements soient pris en compte nous allons deconnecter notre session et la relancer

- Vérifier les permissions sur le socket Docker

```
ls -l /var/run/docker.sock
```

- ce qui nous donne en sortie :

```
srw-rw---- 1 root docker 0 nov.  29 13:40 /var/run/docker.sock
```

- Les permissions srw-rw---- signifient que seuls root et les membres du groupe docker peuvent accéder au socket.

### Détail :

- **srw-rw---- :** Les permissions du fichier. Cela signifie :
- **Le propriétaire** (ici root) peut lire et écrire sur ce fichier.
- **Le groupe (ici docker)** peut lire et écrire sur ce fichier.
- **Les autres** (les utilisateurs qui ne sont ni root ni membres du groupe docker) n'ont aucun accès.
- **root docker :** Le fichier appartient à l'utilisateur root et au groupe docker.

Ensuite nous allons vérifier le nom d'user de notre environnement actuel :

```
whoami
```

- Par exemple,comme notre nom d'utilisateur est meodel, la commande devient

```
sudo usermod -aG docker meodel
```

- Après avoir exécuté la commande pour ajouter votre utilisateur au groupe docker, nous pouvons vérifier cela avec :

```
groups
```

- La commande groups a affiché la liste des groupes auxquels notre utilisateur (meodel) appartient:

- mais dans notre cas CELA n'a pas focntionné >>>
- Nous allons donc forcer en Utilisant la commande suivante pour recharger notre session utilisateur dans le terminal en utilisant:

```
newgrp docker
```

- Et enfin

```
groups
```

ce qui nous donne

```
docker adm cdrom sudo dip plugdev lpadmin lxd sambashare meodel
```

Les lignes suivantes montrent les groupes auxquels appartient notre utilisateur (meodel) sur votre système Linux.

## Tester Docker

- Nous allons donc lancer un test pour confirmer que Docker focntionne correctement

```
docker run hello-world
```

#### Les commandes de base de Docker

### Télécharger une image

Les images sont les "templates" à partir desquels les conteneurs sont créés. Par exemple :

Télécharge une image Ubuntu officielle depuis Docker Hub.

```
docker pull ubuntu
```

### Lancer un container Ubuntu

```
docker run -it ubuntu bash
```

### Lancer un Container

- Pour lancer un conteneur Ubuntu en mode interactif :

```
docker run -it ubuntu bash
```

- **-it :** Mode interactif avec accès au terminal.
- **ubuntu :** Nom de l'image utilisée.
- **bash :** Commande à exécuter dans le conteneur.

### Lister les container actifs :

```
docker ps
```

#### Lister Tous les conteneurs (y compris ceux arrêtés) :

```
docker ps -a

```

sortie :

```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
❯ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED             STATUS                         PORTS     NAMES
fe69df639ca0   hello-world   "/hello"   8 minutes ago       Exited (0) 8 minutes ago                 strange_mcclintock
541b2c3a3d46   hello-world   "/hello"   About an hour ago   Exited (0) About an hour ago             sad_lamarr
```

### détail :

#### Explication de la sortie :

**CONTAINER ID :** Chaque conteneur a un identifiant unique. Par exemple :

fe69df639ca0
541b2c3a3d46
**IMAGE :** Les conteneurs utilisent une image comme modèle. Ici, l'image est hello-world.

**COMMAND :** La commande qui a été exécutée dans le conteneur. Dans le cas de hello-world, c'est "/hello".

**STATUS :**

Exited (0) signifie que le conteneur a terminé son exécution sans erreur.
8 minutes ago et About an hour ago indiquent depuis combien de temps les conteneurs sont arrêtés.

**NAMES :** Docker attribue des noms aléatoires aux conteneurs si vous ne spécifiez pas un nom. Par exemple :

<a href="#sommaire">
  <img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_l.png)
