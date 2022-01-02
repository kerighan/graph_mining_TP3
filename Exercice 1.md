Exercice 1
==========

Le fichier `twitter.gexf` est le graphe suivant :
* les noeuds sont des utilisateurs sur Twitter
* les arêtes correspondent à une mention d'un utilisateur par un autre (les tweets @...)
* chaque noeud contient un attribut `country` renseignant l'origine de l'utilisateur

L'objectif de ce TP est de créer un classifieur probabiliste relationnel (voir cours) permettant de classifier les utilisateurs selon leur pays en se basant exclusivement sur la topologie du graphe.


1. Coder une fonction créant un training set (un dict faisant un mapping node->country) à partir du graphe et d'un entier déterminant la taille du training set
2. Dans cette question, nous allons coder le classifieur probabiliste relationnel. Cette fonction a un paramètre `n_iter` contrôlant le nombre d'itérations de l'algorithme. **Dans cette fonction** :

    a. créer un `set` Python contenant l'ensemble des labels distincts du training set, une variable `n` contenant le nombre de noeuds et la variable `n_labels` contenant le nombre de labels distincts

    b. créer les mappings `node2id`, `label2id` et `id2label` permettant de traduire les différentes valeurs en entier

    c. construire une matrice de probabilité des labels `X` de taille `(n, n_labels)` : chaque sample du training set est un vecteur one-hot avec un 1 à l'index de son label, tous les autres noeuds ont une valeur initiale uniforme de `1/n_labels`.

    d. créer une matrice de transition `T` correspondant à la matrice d'adjacence l1-normalisée sur les lignes.

    e. coder la boucle permettant la mise à jour des probabilités dans `X` (indication : ```X[i] = T[i] @ X```). Bien penser à __ne pas__ mettre à jour les probabilités des noeuds du training set.

    f. retourner un mapping node->country prédisant le pays pour chaque utilisateur
3. Evaluer la qualité de la prédiction en calculant la proportion des labels correctement attribués aux noeuds n'appartenant pas au training set