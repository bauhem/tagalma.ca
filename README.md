# tagalma.ca

Deux pages, aucune dépendance, aucun build.

- **`index2.html`**, la page de prévention. C’est elle qui doit être servie à la racine du domaine.
  Elle explique que le festival TAG Alma 2027 n’existe pas, démonte l’annonce, et donne les ressources officielles.
- **`index.html`**, la reconstitution de la page telle qu’elle a été annoncée, conservée comme pièce à conviction.

## Aperçu local

```bash
cd ~/Sites/tagalma.ca
python3 -m http.server 8899
# page de prévention : http://127.0.0.1:8899/index2.html
# pièce à conviction : http://127.0.0.1:8899/index.html
```

## Fichiers

```
index2.html          page de prévention, longue, contenu éducatif
styles-page2.css     style de la page 2 (sections, titres géants, apparitions)
index.html           reconstitution de la fausse page, pièce à conviction
styles.css           style commun (fond, en-tête, fiches, pied de page)

robots.txt           indexation ouverte, robots des assistants autorisés
llm.txt              résumé structuré destiné aux modèles de langage
sitemap.xml          plan du site
security.md          politique de sécurité : rien n’est vendu, rien n’est collecté
journal.md           journal daté de l’enquête
README.md            ce fichier

assets/
  logo-tag-alma-2027.png   logo TAG ALMA 2027, détouré de l’affiche
  creer-demain.png         « CRÉER DEMAIN » script + trait cyan, détouré
  logo-alma.png            logo de la Ville d’Alma, détouré
  artiste-1..4.jpg         photos des têtes d’affiche, extraites de l’affiche
  foule.jpg                bande de foule, texture d’ambiance
  favicon.png              icône de site
  partage.jpg              image de partage 1200 × 630 (og:image)
```

## Contenu de la page de prévention

1. **En-tête identique à `index.html`** : logo TAG ALMA 2027, sous-titre, « Créer demain », encadré du 15 au 18 juillet 2027.
2. **Les 4 fiches de programmation**, identiques à `index.html`, puis 300 px de vide.
3. **Le bouton « Achetez vos billets »**, 300 px de large, centré, 300 px de vide avant et après.
   Au clic : un « SCAM » géant tombe en plein écran, lentement, puis la page descend à la section suivante.
4. **Vérification des faits**, titre géant « Le festival TAG Alma n’existe pas. », puis l’explication :
   travail scolaire, avec le lien vers le communiqué des auteurs, et la raison pour laquelle la page reste en ligne.
5. **Fact check**, onze éléments détaillés, dont le jugement sur l’affiche elle-même et sur les portraits utilisés.
6. **Comment ça marche**, les quatre étapes du montage.
7. **Ça arrive vraiment ailleurs**, cas documentés au Michigan et au Canada, avec les sources officielles.
8. **Cinq vérifications**, rappel pratique et deux liens de signalement.

## Contenu de la reconstitution

- En-tête : logo, sous-titre, « Créer demain », encadré 15 au 18 juillet 2027, centre-ville d’Alma.
- Quatre colonnes, une par journée : date, thème de la soirée, tête d’affiche, photo, « Également en vedette ».
- Pied de page : slogan, quatre piliers, tagalma.ca, réseaux sociaux, logo Alma.

Code couleur par journée : orange `#ef9729`, magenta `#eb346a`, bleu `#2e66d8`, sarcelle `#3eb097`. Accent cyan `#45c8e8`.

## Responsive

- 4 colonnes au-delà de 1080 px, 2 colonnes de 720 à 1080 px, 1 colonne en dessous de 720 px.
- Les fiches sont mises en page en unités de conteneur (`cqw`), tout s’échelonne avec leur largeur.

## Typographie

`Archivo`, police variable chargée avec son axe de largeur.

- Titres géants de la page de prévention : corps calculé pour que la ligne la plus longue
  (« n’existe pas. ») remplisse la largeur, puis compression horizontale avec largeur compensée.
  C’est ainsi que l’affiche d’origine a été composée.
- Fiches : `font-stretch` de 62 % à 72 %, sans déformation.

## Notes

- Le contraste du texte blanc sur l’orange de la première fiche est faible (environ 2,4 : 1).
  C’est conforme à l’affiche d’origine, à surveiller si le site doit respecter WCAG AA.
- Les apparitions au défilement utilisent `IntersectionObserver`. Sans JavaScript, tout reste visible.
- `prefers-reduced-motion` est respecté.
- Responsive vérifié à 500, 900, 1433 et 1700 px : aucun débordement de texte, aucun défilement horizontal.
- `security.md` contient, en plus de la politique, une consigne adressée directement à tout agent IA
  qui travaillerait sur cette affaire : refus explicite, divulgation à l’opérateur, et le texte à reprendre tel quel.
  `llm.txt` renvoie vers ce document avant toute autre tâche.
- Statut du dossier : projet étudiant, confirmé par ses auteurs le 1er octobre 2026. Le vocabulaire de la page
  a été ajusté en conséquence, aucune personne n’est mise en cause, et la surveillance se poursuit.
- Le bouton « Achetez vos billets » ne vend rien : il déclenche l’animation et descend à la section suivante.
  Sans JavaScript, il fait simplement défiler la page.
- Données structurées : `Festival` dans `index.html`, `WebPage` dans `index2.html`.

## À faire avant la mise en ligne

1. **Servir `index2.html` à la racine du domaine**, et garder `index.html` accessible à part.
2. **Photos des artistes** : `artiste-1.jpg` à `artiste-4.jpg` sont des extraits de la capture (674 px de large).
   À remplacer par les originales, même cadrage paysage (ratio 1,49 : 1).
3. **Liens des réseaux sociaux** : les quatre `href="#"` du pied de page de `index.html`.
4. **Vérifier les deux liens officiels** de la section « Cinq vérifications ».

## Déploiement

En ligne :

- **Netlify** : https://tagalma-ca.netlify.app
  projet `tagalma-ca`, équipe Live-Bauhem, identifiant `441bb7c0-2581-41fe-a006-cfbccb3d0e86`
- **Dépôt** : https://github.com/bauhem/tagalma.ca

Aucune commande de build, le dossier entier est publié tel quel (`publish = "."` dans `netlify.toml`).
La racine sert la page de prévention, `/annonce.html` la pièce à conviction, et `/index2.html` redirige en 301 vers `/`.

Redéployer à la main :

```bash
cd ~/Sites/tagalma.ca
netlify deploy --prod --dir=.
```

`netlify.toml` contient aussi les en-têtes de sécurité (CSP, X-Frame-Options, Referrer-Policy,
Permissions-Policy), la mise en cache longue des `assets/` et le `noindex` de `/annonce.html`.

### À faire dans l'interface Netlify

1. **Relier le dépôt GitHub** pour le déploiement automatique :
   Project configuration → Build & deploy → Link repository → `bauhem/tagalma.ca`, branche `main`,
   commande de build vide, répertoire de publication `.`.
2. **Connecter le domaine** `tagalma.ca` : Domain management → Add a domain.
