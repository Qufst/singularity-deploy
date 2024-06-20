Bootstrap: docker
From: continuumio/miniconda3

%post
    # Mise à jour et installation de dépendances
    apt-get update && apt-get install -y wget bzip2

    # Téléchargement et installation de micromamba
    wget -qO- https://micromamba.snakepit.net/api/micromamba/linux-64/latest | tar -xvj -C /usr/local/bin

    # chemins
    MICROMAMBA_DIR="$HOME/micromamba-bin"
    MICROMAMBA_BIN="$MICROMAMBA_DIR/micromamba"
    MICROMAMBA_ROOT="$HOME/micromamba"
    BASHRC="$HOME/.bashrc"

    # Vérifier si micromamba existe et est exécutable
    if [ ! -x "$MICROMAMBA_BIN" ]; then
      echo "micromamba binary not found or not executable"
      exit 1
    fi
    
    # initialisation du shell pour micromamba
    eval "$("$MICROMAMBA_BIN" shell hook -s bash)"

    # Création de l'environnement conda
    micromamba create -y -n myenv -f /environment.yml
    micromamba clean --all --yes

    # Copie du fichier index.qmd
    mkdir -p /project
    cp index.qmd /project/

%environment
    # Activation de l'environnement micromamba
    export PATH=/micromamba/envs/myenv/bin:$PATH
    export MICROMAMBA_PREFIX=/micromamba/envs/myenv
    micromamba activate myenv

%runscript
    # Commande à exécuter lorsque le conteneur est lancé
    exec quarto render /project/index.qmd