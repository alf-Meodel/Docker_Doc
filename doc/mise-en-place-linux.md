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

- Main PID: Le processus principal du démon Docker (dockerd) est identifié par le numéro de processus 1652.
- Tasks: Docker gère actuellement 14 tâches ou threads.
- Memory: Docker utilise 100.2 Mo de mémoire.
- CPU: Il a consommé 536 ms de temps processeur jusqu'à présent.

<a href="#sommaire">
  <img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_l.png)
