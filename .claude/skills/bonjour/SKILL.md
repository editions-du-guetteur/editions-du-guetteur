---
name: bonjour
description: Démarre une séance de travail sur le site des Éditions du Guetteur. Récupère les changements de Martin, fait le point sur le projet et propose par quoi commencer. À lancer quand Thierry tape /bonjour ou dit bonjour en début de séance.
---

# Bonjour : démarrer la séance

Thierry ne lit pas les sorties techniques. Fais tout toi-même, en silence, puis présente-lui un point
**court, en français simple, sans jargon** (pas de « commit », « push », « branche » : dis « enregistré
sur GitHub », « mis en ligne », etc.).

## 1. Récupérer le travail de Martin

- `git pull` sur `main`.
- Si Martin a poussé des changements, regarde `git log` depuis la dernière séance et résume-les en une
  ou deux phrases (« Martin a corrigé… »).
- Si le pull échoue (conflit, réseau, droits) : ne force rien, dis-le simplement à Thierry et propose
  d'en parler à Martin.

## 2. État de l'enregistrement

- `git status` : y a-t-il des modifications pas encore enregistrées sur GitHub ? Si oui, dis lesquelles
  en une phrase (« la page du livre a été modifiée la dernière fois mais pas encore mise en ligne »).
- Commits locaux pas encore envoyés (`git log origin/main..main`) : le signaler de la même façon.

## 3. Point sur le projet

- Relis dans `.claude/CLAUDE.md` les listes « État de l'hébergement » et « Reste à faire avant le
  lancement ».
- Repère dans les pages HTML les commentaires `À FOURNIR`, `À COMPLÉTER` et `STRIPE`.
- Consulte la mémoire (notes de la dernière séance, s'il y en a).

## 4. Ce que tu dis à Thierry

Un message bref, dans cet ordre :

1. **Bonjour** et ce qui a changé depuis la dernière fois (Martin, ou rien de neuf).
2. **Ce qui est fait** (2 ou 3 lignes au plus).
3. **Ce qui manque de son côté** : textes, images, prix, décisions. Liste numérotée courte.
4. **Ce qui relève de Martin**, s'il y a lieu (OVH, nom de domaine, déploiement).

Termine par **une seule question** : par quoi veut-il commencer aujourd'hui ? Propose ton conseil en
premier.
