# Créer son conda privé 

## Récupérer et installer conda_ifremer

- Récupérer le dossier conda.zip ICI.
- Extraire le dossier dans votre root "Dossier personnel" (vous devez maintenant avoir un dossier conda_ifremer, un fichier environment.yml et un fichier chaché .condarc dans votre dossier personnel)

## Comment utiliser conda_ifremer 

- Ouvrir le terminal
- Vous pouvez maintenant créer votre environnement `conda env create -f environment.yml`
- Vous pouvez installer des packages :
	- `conda install PACKAGE` cette commande permet de télécharger le package sur conda-forge
	- `conda install -c ~\conda_ifremer PACKAGE` cette commande permet de télécharger le package sur notre conda privé conda_ifremer
	
## Ajouter des packages sur conda_ifremer

- Construire la recette conda (meta.yaml) du package avec le doc conda.md.
- Ouvrir le terminal 
- Si vous n'avez pas conda build `conda install conda-build`
- `conda build "/home/user/PACKAGE"` cette commande permet de construire le package (vous pourrez trouver ou il est avec les indications du terminal)
- Copier le package dans conda_ifremer `cp /home/user/lieudupackage/PACKAGE-version-py39_0.tar.bz2 /home/user/conda_ifremer/linux-64`
- `conda index conda_ifremer/` permet de générer les métadata. La commande est à faire à chaque changement de package. 

 
