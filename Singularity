Bootstrap: docker
From: continuumio/miniconda3

%post
    # Mise à jour et installation de dépendances
    apt-get update && apt-get install -y wget bzip2

    # Téléchargement et installation de micromamba
    wget -qO- https://micromamba.snakepit.net/api/micromamba/linux-64/latest | tar -xvj -C /usr/local/bin

    # Création de l'environnement conda
    micromamba create -y -n myenv -f /environment.yml
    micromamba clean --all --yes

    # Copie du fichier index.qmd
    mkdir -p /project
    cp index.qmd /project/

%environment
    # Activation de l'environnement micromamba
    micromamba activate myenv

%runscript
    # Commande à exécuter lorsque le conteneur est lancé
    exec quarto render /project/index.qmd