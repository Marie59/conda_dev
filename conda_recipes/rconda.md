# Créer un package Conda

Ceci est un guide rapide pour créer une "recette" conda. Vous aurez besoin d'avoir installé conda sur votre machine. 

## 1. CRAN

Vérifier si votre package est sur CRAN.

## 2. Créer la recette avec CRAN

Aller sur le lien suivant <https://github.com/bgruening/conda_r_skeleton_helper> télécharger et dézipper le code, puis suivre les instructions du README.md.

## 2. Créer la recette sans CRAN (à la main)

Récupérer le template meta.yaml et le placer dans un nouveau dossier (nommer ce dossier avec le nom du package).

Avec le template :
- Remplir la 1ère ligne avec la version du package entre les quotes
- Remplir la 6ème ligne avec le nom du package après le `r-`
- Remplir la 10ème ligne :
	- Aller sur le github/gitlab de développement du package.
	- Aller dans tag ou release copier le tar.gz et coller le dans url: et remplacer dans cette url le numéro de verion par `{{ version }}`
- Remplir la 11ème ligne :
	- Ouvrir le terminal 
	- Installer openssl : `conda install openssl -c conda-forge`
	- Taper `curl sL tar.gz | openssl sha256`
- Remplir la 16ème ligne : si votre code est en R uniquement (avec la même indentation que la ligne 15) laisser `noarch: generic`, sinon suppirmer cette ligne.
- Remplir les requirements :
	- Vérifier que les dépendances du package sont elles-même sur Conda
	- Ajouter toutes les dépendances de développement dans build et de run dans host et run.
	Exemple :
		- r-base >=3.6
		- r-package-dependance >=0.0.0,<1.0.0 (ne pas écrire avec des majuscules et généralment ce sont des "-" et pas "_". Ne pas oublier `r-` pour les packages R)
- Remplir le test : mettre le nom du package lignes 32 et 33 entre les quotes.
- Remplir le about : 
	- home : mettre l'url du git de développement
	- license : mettre le SPDX correspondant de la license (liste des spdx <https://spdx.org/licenses/>)
	- license_file : mettre le nom (ou le chemin) du fichier de license présent dans le git de développement (souvent LICENSE ou LICENSE.txt)
	- summary : description de ce que fait le package
- Remplir recipe-maintainers : en dessous `- conda-forge/r` mettre votre identifiant github.

## 3. Mettre la recette sur conda

- Aller sur <https://github.com/conda-forge/staged-recipes>
- Fork le repository
- Créer une nouvelle branche avec le nom de votre package
- Dans le dossier recipe (attention de ne pas être dans example) cliquer sur upload files
- Ajouter le DOSSIER (nom-package/meta.yaml)
- Commit et Pull request mettre un titre compréhensible "Add my_package recipe"
- Vérifier que les checks se passent bien. Erreurs fréquentes : 
	- sha256 pas bon, copier coller le bon du message d'erreur 
	- Vérifier que les noms de dépendences sont bien ecrits et les versions disponibles sur conda (il faut peut-être ajouter une version pour r-base)
	- Si vous avez besoin d'aide vous pouvez poser vos question sur <https://gitter.im/conda-forge/conda-forge.github.io> (à privilégier) ou pinger @conda-forge/help-r et poser vos questions.
	- Quand la recette laisser un commentaire : "@conda-forge/help-r my recipe is ready !" et attendre la review, d'éventuels commentaires et/ou que la recette soient merger.

## 4. Faire une mise à jour de package

- Aller sur le feedstock conda (la ou se trouve la recette actuelle) de la recette à mettre à jour. Vous pouvez aller sur <https://conda-forge.org/feedstock-outputs/>, rechercher votre package et cliquer sur nompackage-feedstock.
- Fork le repository
- Créer une nouvelle branche
- Faites vos modifications sur le meta.yaml
- Si c'est une nouvelle version mettre number: 0 sinon ajouter 1 au number déjà inscrit
- Commit et pull request 
- Quand votre mise à jour a passé tous les checks laisser en commentaire "@conda-forge-admin, please rerender"

## 5. Liens utiles
- <https://conda-forge.org/#contribute>
- <https://conda-forge.org/docs/maintainer/adding_pkgs.html#the-recipe-meta-yaml>

