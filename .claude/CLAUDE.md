# Les Éditions du Guetteur — site vitrine et vente

> Ce fichier s'adresse à **Claude Code**, sur le PC de Thierry Perret. Il est rangé dans
> `.claude/CLAUDE.md`. Le dépôt est **privé**, mais n'écris jamais ici de secret
> (clé, mot de passe, identifiant FTP, chiffre de vente, donnée client).

## Qui est qui

- **Thierry Perret** : éditeur, propriétaire du projet, 80 ans. Il dirige la publication du site, qui
  appartient à sa société **Europera**. C'est lui qui décide du contenu et des livres.
- **Martin Guilbaud** (GitHub : `martinguilbaud`) : un ami informaticien qui l'aide, *Owner* de
  l'organisation GitHub. Il peut relire, corriger et publier. Ce que Martin a commité est fiable.

**Avec Thierry** : il ne code pas et **n'utilise jamais de terminal ni PowerShell**. Fais toutes les
manipulations techniques toi-même (fichiers, git, vérifications). Explique en français simple, sans
jargon. Demande-lui seulement les textes, les images, les prix et les décisions. Une question à la fois.

**Quand renvoyer vers Martin** : nom de domaine et DNS, réglages OVH, droits GitHub, déploiement qui
échoue, ou tout changement de structure du site. Pour le contenu (ajouter un livre, changer un texte),
Thierry et toi vous débrouillez seuls.

## Début et fin de séance

- **`/bonjour`** (`.claude/skills/bonjour/`) : récupère le travail de Martin, signale ce qui n'est pas
  encore enregistré sur GitHub, fait le point sur ce qui reste et demande par quoi commencer.
- **`/ciao`** (`.claude/skills/ciao/`) : résume la journée, met à jour les listes à cocher de ce fichier,
  demande s'il faut enregistrer sur GitHub (donc mettre en ligne une fois OVH branché), puis note dans
  la mémoire où on s'est arrêté.

Les listes « État de l'hébergement » et « Reste à faire avant le lancement » ci-dessous sont l'état du
projet partagé avec Martin : les tenir à jour à chaque `/ciao`.

## Comptes

| Service | Titulaire | Rôle |
|---|---|---|
| GitHub, organisation `editions-du-guetteur` (compte `thierryperret` + `martinguilbaud`, tous deux *Owner*) | Thierry et Martin | Stocke le code, historique, travail à deux. Dépôt **privé** |
| OVH (hébergement web + nom de domaine + e-mail de contact) | Europera | **Héberge le site en ligne** |
| Stripe | Europera (Thierry seul) | Encaisse les paiements. Martin n'y a pas accès |

Le site n'utilise **pas** GitHub Pages.

## Comment est fait le site

Un site **statique**, volontairement simple : des pages HTML, une feuille de style, aucune base de
données, aucun CMS, aucun outil de compilation, pas de PHP. Il peut donc tourner sur l'offre
d'hébergement OVH la moins chère.

| Fichier | Rôle |
|---|---|
| `index.html` | Accueil : titre « Notre dernière publication » + **dernière parution** (bloc `a-la-une`, un seul livre) |
| `catalogue.html` | Catalogue en trois rubriques : **Arts**, **Nouvelles et récits**, **Documents** (une fiche `<a class="fiche">` par livre, le plus récent en premier ; « Prochainement » si la rubrique est vide) |
| `livres/<titre>.html` | Une page par livre, avec le bouton « Acheter » |
| `a-propos.html` | La maison + contact |
| `cgv.html`, `mentions-legales.html` | Obligatoires pour vendre en ligne |
| `style.css` | Le seul fichier de style |
| `img/` | Couvertures et photos |

Le paiement passe par un **Payment Link Stripe** par livre : le bouton « Acheter » pointe vers une URL
`https://buy.stripe.com/…`. Stripe gère la carte, l'adresse de livraison, les frais de port, la facture
et l'e-mail de confirmation. Le site ne voit jamais un paiement et ne stocke rien.

Les commentaires HTML `À FOURNIR`, `À COMPLÉTER` et `STRIPE` repèrent ce qui reste à remplir.

## Hébergement OVH et mise en ligne

**Principe** : la branche `main` de GitHub est la vérité. OVH récupère `main` grâce à son
**intégration Git native** (Mes sites › ⁝ › « Associer Git »), et un **webhook GitHub** déclenche le
déploiement à chaque push. Il n'y a ni FTP manuel, ni GitHub Actions, ni secret à stocker côté GitHub.

- Offre visée : la plus petite offre d'hébergement web OVH (Starter ou Perso). Elle inclut l'intégration
  Git (un dépôt) et suffit pour un site statique.
- Dépôt privé : OVH s'y connecte en SSH (`git@github.com:editions-du-guetteur/<depot>.git`). La clé
  publique fournie par OVH est ajoutée côté GitHub, de préférence comme *Deploy key* du dépôt, en
  lecture seule.
- Le répertoire OVH associé doit être vide au moment de l'association. Les fichiers du dépôt sont
  servis tels quels : `index.html` doit rester à la racine du dépôt.
- Webhook : URL copiée depuis le formulaire OVH, ajoutée dans GitHub › Settings › Webhooks, format
  `application/json`, événement `push`. Un `ping` doit répondre 200.
- En cas d'échec : OVH › Mes sites › détails du dernier déploiement, ou « Déployer Git » à la main.
  C'est le domaine de Martin.
- HTTPS : certificat SSL gratuit Let's Encrypt, à activer dans l'espace client OVH.
- Doc OVH : https://docs.ovhcloud.com/fr/guides/web-cloud/web-hosting/git-integration-webhosting

**Tant que l'hébergement n'existe pas**, un push ne fait qu'enregistrer le travail sur GitHub. **Une fois
le webhook en place, chaque push sur `main` est en ligne en quelques instants.**

### État de l'hébergement (à tenir à jour)

- [ ] Commander le nom de domaine + l'hébergement (Europera)
- [ ] Créer l'adresse e-mail de contact sur le domaine (ex. contact@…), puis la mettre dans `a-propos.html`,
      `mentions-legales.html` et `cgv.html`
- [ ] Associer Git dans OVH (dépôt privé, branche `main`, Deploy key) — Martin
- [ ] Webhook GitHub → OVH, test `ping` OK — Martin
- [ ] Activer le SSL (HTTPS)
- [ ] Mettre l'URL `https://<domaine>/` dans les liens Stripe (redirection après paiement) si besoin

## Règles

- **Git** : commit et push directement sur `main`, sans branche ni pull request. Toujours `git pull`
  en début de session, car Martin peut avoir poussé des changements. Messages de commit courts, en français.
- **Toujours vérifier avant de pousser** : ouvre la page modifiée pour contrôler le rendu sur ordinateur
  et sur mobile. Montre ou décris le résultat à Thierry, et **attends son accord** avant le push, puisque
  le push met en ligne.
- **Jamais de secret dans le dépôt** : aucune clé Stripe (`sk_…`, `rk_…`), aucun mot de passe ni
  identifiant OVH/FTP. Un Payment Link n'est pas un secret, il peut aller dans le HTML.
- **Garder la simplicité** : pas de framework, pas de npm, pas de JavaScript sans nécessité réelle, pas de
  PHP. Si un besoin dépasse ce cadre (panier multi-livres, stock automatique…), en parler à Martin avant.
- **Pas de ressources externes** (polices Google, scripts tiers, traceurs), pour ne pas avoir besoin de
  bandeau cookies.
- **Le prix est fixé par l'éditeur** (loi sur le prix unique du livre). TVA du livre : **5,5 %**, prix
  affichés TTC.
- **Phase maquette** : chaque page porte `<meta name="robots" content="noindex">`. À retirer de toutes les
  pages le jour du lancement, et pas avant.
- Les **CGV** et les **mentions légales** sont des modèles : ne pas les présenter comme définitives tant
  qu'elles n'ont pas été relues. Hébergeur à indiquer dans les mentions légales : OVH SAS, 2 rue
  Kellermann, 59100 Roubaix.

## Ajouter un livre

Demander à Thierry : titre, auteur, prix TTC, tirage, ISBN, couverture (image), texte de présentation, quelques lignes sur l'auteur, des extraits (texte et/ou image d'une double page), la bibliographie de l'auteur (« Du même auteur »),
et le lien Stripe (ou le créer avec lui, voir plus bas).

1. Copier `livres/les-aquarellistes-anonymes.html` vers `livres/<titre-en-minuscules-avec-tirets>.html`
   *Livre à paraître* : partir plutôt de `livres/repas-de-dessins.html` (encart `parution` avec la date au lieu du bloc d'achat, fiche avec « Parution » ; ne mettre que les lignes connues).
   et remplacer tout le contenu (titre, `<title>`, `description`, texte, fiche, prix, lien Stripe).
2. Déposer la couverture dans `img/` (JPG ou WebP, environ 1 000 px de haut au maximum, la compresser si
   besoin) et remplacer la couverture dessinée en CSS par un `<img>` avec un `alt`.
3. Demander la rubrique (Arts, Nouvelles et récits ou Documents) et ajouter un bloc `<a class="fiche">` **en tête** de cette rubrique dans `catalogue.html` (retirer « Prochainement » si elle était vide).
3 bis. Si c'est la dernière parution : remplacer le livre du bloc `a-la-une` dans `index.html` (lien, couverture, titre, auteur, rubrique, citation `citation-une`, tirage et prix `rarete`, bouton « Acheter ») et l'image du lien `feuilleter` (double page).
4. Vérifier dans le navigateur, sur mobile et sur ordinateur, montrer à Thierry, puis commit et push.

## Créer le lien Stripe d'un livre (Thierry le fait, tu le guides pas à pas)

Dans Stripe, compte Europera : *Liens de paiement → Nouveau*.
- Produit : le titre du livre, au prix TTC, avec un taux de TVA de **5,5 % inclus**.
- Cocher « Permettre au client d'ajuster la quantité ».
- Cocher « Collecter l'adresse de livraison » et ajouter un tarif de livraison.
- Après paiement : cocher « Créer une facture ».
- Options avancées : « Limiter le nombre de paiements » au tirage disponible.
- Copier l'URL `https://buy.stripe.com/…` dans le bouton « Acheter » de la page du livre.

Faire un premier essai en **mode test** de Stripe avant d'utiliser le vrai lien.

## Reste à faire avant le lancement

- [x] Vraie couverture des *Aquarellistes Anonymes* (`img/aquarellistes-couverture.jpg`)
- [x] *Aquarellistes Anonymes* : texte de présentation (brouillon n° 1 choisi le 9 nov. 2026), texte « L'auteur » et « Bibliographie » (6 nov. 2026), ISBN : 979-10-984927-0-9
- [x] *Aquarellistes Anonymes* : section « Extraits » (double page `img/aquarellistes-pages.jpg` + trois courts textes)
- [x] Nouvelle structure : menu Accueil / Les Éditions du Guetteur / Catalogue, accueil = dernière publication, `catalogue.html` en trois rubriques (à faire relire par Martin)
- [x] Accueil : encadré « Prochaine publication » (*Repas de Dessins*, Jean-Marie Leydier, Arts, image `img/repas-de-dessins-couverture.jpg`, sortie le 15 déc. 2026)
- [ ] *Repas de Dessins* : page `livres/repas-de-dessins.html` créée (modèle « à paraître », 6 nov. 2026) ; reste prix TTC, tirage, format, ISBN, présentation, lien Stripe
- [ ] **Le 15 déc. 2026 (avec Thierry)** : *Repas de Dessins* devient la dernière publication (bloc `a-la-une` de `index.html`), sa fiche de `catalogue.html` perd la classe `fiche-a-paraitre` et le bandeau, sa page remplace l'encart `parution` par le bloc `achat` (prix, Stripe), et l'encadré `a-venir` est retiré ou remplacé. Décision du 4 nov. 2026 : bascule faite à la main, sans JavaScript
- [ ] *La Saga Guilbaud* (Jean-Jacques Guilbaud, Nouvelles et récits, à paraître le 1er févr. 2027) : fiche « À paraître » en place dans `catalogue.html` avec couverture dessinée provisoire ; récit ; page `livres/la-saga-guilbaud.html` créée (modèle « à paraître ») ; reste couverture, prix, format, pages, tirage, ISBN. À la parution, même bascule à la main que *Repas de Dessins*
- [x] Texte de présentation de la maison (`a-propos.html`, texte de Thierry du 4 nov. 2026)
- [x] `a-propos.html` : page réorganisée en deux volets « Aux lecteurs » / « Aux auteurs », avec l'encadré « Envoyer un manuscrit » dans le volet auteurs (9 nov. 2026) : envoi par courriel (adresse de contact à venir), réponse sous deux mois environ
- [x] Accueil enrichi (6 nov. 2026) : citation du livre, « 100 exemplaires numérotés · 25 € », boutons Découvrir puis Acheter, double page « Feuilleter », nom du domaine agrandi ; boutons des domaines agrandis sur `a-propos.html`
- [x] Mentions légales : Europera SARL au capital de 7 622 €, RCS Paris, SIRET 401 458 641 00016, TVA FR73 401 458 641, hébergeur OVH (6 nov. 2026) ; reste à faire relire, et l'e-mail de contact
- [ ] CGV : livraison (fait : 8 € par Colissimo, France métropolitaine uniquement ; reste le délai et « par commande ou par livre » ; le lien Stripe devra limiter la livraison à la France), médiateur de la consommation (obligatoire ; choix du 6 nov. 2026 : **CM2C**, Thierry doit adhérer pour Europera sur cm2c.net, puis reporter ses coordonnées officielles dans `cgv.html`), relecture
- [ ] Compte Stripe Europera + lien de paiement du premier livre
- [ ] Hébergement OVH en place (voir « État de l'hébergement »)
- [ ] Retirer les **livres tests** fictifs de `catalogue.html` (bandeau « Exemple », commentaires `LIVRES TESTS` ; garder *La Saga Guilbaud*) et les styles `.fiche-test`, `.bandeau-test`, `.teinte-*` de `style.css`
- [ ] Retirer les `noindex`

### Pour Martin (4 nov. 2026)

- Thierry a réorganisé le site : menu Accueil / Les Éditions du Guetteur / Catalogue ; l'accueil ne montre
  plus que la dernière publication (bloc `a-la-une`) ; nouvelle page `catalogue.html` en trois rubriques ;
  la page du livre a des sections « L'auteur » et « Extraits ». Animations d'apparition de l'accueil en CSS
  seul (pas de JavaScript), désactivées si `prefers-reduced-motion`. À relire quand tu as un moment.
- Constaté au passage, non corrigé : toutes les pages chargent les polices Google Fonts (EB Garamond, Inter),
  ce qui contredit la règle « pas de ressources externes ». À trancher : héberger les polices dans le dépôt
  ou passer aux polices du système.
- **Demande de Thierry : une « fiche unique » par livre.** Il voudrait saisir un livre une seule fois
  (titre, auteur, rubrique, prix, tirage, pages, date de sortie, couverture) et qu'il apparaisse à la fois
  dans `catalogue.html` et sur l'accueil (« Prochaine publication » puis « Dernière publication »), la
  mention « À paraître » disparaissant d'elle-même à la date de sortie. Aujourd'hui c'est fait à la main
  dans les deux pages (rappel du 15 déc. 2026 pour *Repas de Dessins*). Cela demanderait un petit
  JavaScript (ex. une liste de livres en JSON lue par les deux pages) ou une étape de génération :
  ton avis et ton accord avant toute chose. En attendant, on continue à la main.
