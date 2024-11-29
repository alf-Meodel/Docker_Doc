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

Dans le terminal, exécutez :

```
sudo systemctl status docker
```

<a href="#sommaire">
  <img src="../assets/button/back_to_top.png" alt="Back to top" style="width: 150px; height: auto;">
</a>

![border](../assets/line/border_deco_l.png)
