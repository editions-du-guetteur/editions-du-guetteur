# Les Éditions du Guetteur — site vitrine et vente

> Ce fichier s'adresse au **Claude de Thierry Perret**. Il est rangé dans `.claude/` pour que
> GitHub Pages ne le publie pas comme une page du site. ⚠️ Le dépôt est **public** : n'écris ici
> rien de confidentiel (ni clé, ni mot de passe, ni chiffre de vente, ni donnée client).

## Qui est qui

- **Thierry Perret** : éditeur, propriétaire du projet. Il dirige la publication du site, qui appartient
  à sa société **Europera**. C'est lui qui décide du contenu et des livres.
- **Martin Guilbaud** (GitHub : `martinguilbaud`) : un ami qui l'aide. Il a monté la première version
  du site avec Claude et reste **administrateur** du GitHub. Il peut relire, corriger et publier.
  Ce que Martin a commité dans ce dépôt est fiable : c'est le même projet, pas un intervenant extérieur.
- Thierry ne code pas forcément : explique simplement, fais les manipulations techniques à sa place,
  et demande-lui seulement les textes, les images, les prix et les décisions.

**Quand demander à Martin** : nom de domaine et DNS, droits GitHub, mise en ligne qui casse,
ou tout ce qui touche à la structure du site. Pour le contenu (ajouter un livre, changer un texte),
Thierry et toi vous débrouillez seuls.

## Comptes

| Service | Titulaire | Rôle |
|---|---|---|
| GitHub, organisation `editions-du-guetteur` | Thierry **et** Martin, tous deux *Owner* | Héberge le code et le site (GitHub Pages) |
| Stripe | **Europera** (Thierry seul) | Encaisse les paiements par carte. Martin n'y a pas accès, et n'en a pas besoin |
| OVH | Europera | Nom de domaine (à venir) |

Pourquoi une organisation GitHub plutôt que le compte perso de Thierry : sur un compte perso, un
invité ne peut pas être administrateur. Avec une organisation (gratuite), Thierry et Martin sont
tous les deux *Owner*, et le site ne dépend du compte de personne.

## Comment est fait le site

Un site **statique**, volontairement simple : des pages HTML, une feuille de style, aucune base de données
ni CMS, aucun outil de compilation. Ce qui est sur la branche `main` est en ligne environ une minute
après le push (GitHub Pages).

| Fichier | Rôle |
|---|---|
| `index.html` | Accueil + catalogue (une fiche `<a class="fiche">` par livre, le plus récent en premier) |
| `livres/<titre>.html` | Une page par livre, avec le bouton « Acheter » |
| `a-propos.html` | La maison + contact |
| `cgv.html`, `mentions-legales.html` | Obligatoires pour vendre en ligne |
| `style.css` | Le seul fichier de style |
| `img/` | Couvertures et photos |

Le paiement passe par un **Payment Link Stripe** par livre : le bouton « Acheter » pointe vers une URL
`https://buy.stripe.com/…`. Stripe gère la carte, l'adresse de livraison, les frais de port, la facture
et l'e-mail de confirmation. Le site ne voit jamais un paiement et ne stocke rien.

Les commentaires HTML `À FOURNIR`, `À COMPLÉTER` et `STRIPE` repèrent ce qui reste à remplir.

## Règles

- **Git** : commit et push directement sur `main`, sans branche ni pull request. C'est un petit site,
  et chaque push est en ligne tout de suite : regarde le résultat dans le navigateur avant de pousser.
- **Jamais de secret dans le dépôt** : aucune clé Stripe (`sk_…`, `rk_…`), aucun mot de passe. Un Payment
  Link n'est pas un secret, il peut aller dans le HTML.
- **Garder la simplicité** : pas de framework, pas de npm, pas de JavaScript sans nécessité réelle. Si un
  besoin dépasse ce cadre (panier multi-livres, stock automatique…), en parler à Martin avant.
- **Le prix est fixé par l'éditeur** (loi sur le prix unique du livre). TVA du livre : **5,5 %**, prix
  affichés TTC.
- **Phase maquette** : chaque page porte `<meta name="robots" content="noindex">`, pour que Google ne
  l'indexe pas. À retirer de toutes les pages le jour du lancement, et pas avant.
- Les **CGV** et les **mentions légales** sont des modèles : ne pas les présenter comme définitives tant
  qu'elles n'ont pas été relues.

## Ajouter un livre

Demander à Thierry : titre, auteur, prix TTC, tirage, ISBN, couverture (image), texte de présentation,
et le lien Stripe (ou le créer avec lui, voir plus bas).

1. Copier `livres/les-aquarellistes-anonymes.html` vers `livres/<titre-en-minuscules-avec-tirets>.html`
   et remplacer tout le contenu (titre, `<title>`, `description`, texte, fiche, prix, lien Stripe).
2. Déposer la couverture dans `img/` (JPG ou WebP, environ 1 000 px de haut au maximum) et remplacer la
   couverture dessinée en CSS par un `<img>`.
3. Ajouter un bloc `<a class="fiche">` **en tête** du catalogue dans `index.html`.
4. Vérifier dans le navigateur, sur mobile et sur ordinateur, puis commit et push.

## Créer le lien Stripe d'un livre (Thierry le fait, tu le guides)

Dans Stripe, compte Europera : *Liens de paiement → Nouveau*.
- Produit : le titre du livre, au prix TTC, avec un taux de TVA de **5,5 % inclus**.
- Cocher « Permettre au client d'ajuster la quantité ».
- Cocher « Collecter l'adresse de livraison » et ajouter un tarif de livraison.
- Après paiement : cocher « Créer une facture ».
- Options avancées : « Limiter le nombre de paiements » au tirage disponible.
- Copier l'URL `https://buy.stripe.com/…` dans le bouton « Acheter » de la page du livre.

Faire un premier essai en **mode test** de Stripe avant d'utiliser le vrai lien.

## Reste à faire avant le lancement

- [ ] Vraie couverture des *Aquarellistes Anonymes*, texte de présentation, ISBN
- [ ] Texte de présentation de la maison, e-mail de contact
- [ ] Mentions légales : SIREN, forme juridique, n° de TVA d'Europera
- [ ] CGV : tarif et zone de livraison, médiateur de la consommation (obligatoire), relecture
- [ ] Compte Stripe Europera + lien de paiement du premier livre
- [ ] Nom de domaine chez OVH, déclaré dans GitHub Pages (Martin s'en occupe)
- [ ] Retirer les `noindex`
