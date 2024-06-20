Bootstrap: docker
From: continuumio/miniconda3

%post
    # Mise à jour et installation de dépendances
    apt-get update && apt-get install -y wget bzip2

    # Téléchargement et installation de micromamba
    curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest | tar -xvj bin/micromamba

    # chemins
    MICROMAMBA_BIN="bin/micromamba"

    # Vérifier si micromamba existe et est exécutable
    if [ ! -x "$MICROMAMBA_BIN" ]; then
      echo "micromamba binary not found or not executable"
      exit 1
    fi
    ls -l $MICROMAMBA_BIN
    # initialisation du shell pour micromamba
    ./bin/micromamba shell init -s bash -p ~/micromamba
    source ~/.bashrc

    # Copie du fichier index.qmd
    mkdir -p /project
    cp index.qmd /project/

%environment
    micromamba activate myenv

%runscript
    # Commande à exécuter lorsque le conteneur est lancé
    exec quarto render /project/index.qmd