---
name: ciao
description: Termine la séance de travail sur le site des Éditions du Guetteur. Résume la journée, demande à Thierry s'il faut mettre en ligne, met à jour les listes de CLAUDE.md et enregistre la mémoire. À lancer seulement quand Thierry tape /ciao ou dit qu'il arrête pour aujourd'hui.
disable-model-invocation: true
---

# Ciao : terminer la séance

Thierry ne lit pas les sorties techniques. Parle-lui en français simple, sans jargon, une question à la
fois.

## 1. Résumer la journée

- Regarde `git status` et `git diff` : qu'est-ce qui a changé aujourd'hui ?
- Dis-le à Thierry en 2 ou 3 lignes (« Aujourd'hui, on a ajouté le texte du livre et la couverture »).

## 2. Mettre à jour les listes du projet

Dans `.claude/CLAUDE.md`, coche ce qui est terminé dans « État de l'hébergement » et « Reste à faire
avant le lancement », et ajoute ce qui est apparu. C'est là que Martin voit où on en est : tout ce qui
concerne le projet va ici, pas seulement dans la mémoire.

Jamais de secret dans ce fichier (clé, mot de passe, identifiant, chiffre de vente, donnée client).

## 3. Mettre en ligne ? (demander à Thierry)

S'il y a des modifications :

- Avant de demander, vérifie que les pages modifiées s'affichent bien (ordinateur et mobile), comme
  l'exigent les règles du projet.
- Pose **une** question claire : « Voulez-vous enregistrer ce travail sur GitHub ? » Précise ce que ça
  implique : tant que l'hébergement OVH n'est pas branché, c'est seulement une sauvegarde ; une fois
  branché, **ça met le site en ligne aussitôt**.
- **Oui** : `git add` des fichiers concernés, commit court en français, `git push` sur `main`. Confirme
  que c'est fait. Si le push échoue, ne force rien et propose d'en parler à Martin.
- **Non** : ne rien envoyer. Dis-lui que le travail reste sur son ordinateur et qu'on le retrouvera à
  la prochaine séance (`/bonjour` le signalera).

S'il n'y a aucune modification, dis-le simplement et passe à la suite.

## 4. Enregistrer la mémoire

Note dans la mémoire ce qui servira la prochaine fois et qui n'est **ni** dans le dépôt **ni** dans
`CLAUDE.md` :

- où on s'est arrêté et ce qu'on comptait faire ensuite ;
- les décisions ou préférences exprimées par Thierry (ton, choix éditoriaux, façon de travailler) ;
- ce qu'on attend de quelqu'un (« Thierry doit envoyer la couverture », « question posée à Martin sur… »).

Mets à jour une note existante plutôt que d'en créer une en double, et supprime ce qui est devenu faux.

## 5. Au revoir

Termine par un message très court : ce qui est fait, ce qui attend pour la prochaine fois, et un mot
pour dire au revoir. Pas de question.
