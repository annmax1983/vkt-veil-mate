# VKT VeilMate

[English](../README.md) | [中文](README_zh.md) | [Deutsch](README_de.md) | [Español](README_es.md) | [日本語](README_ja.md) | Français

Un rideau pour le navigateur : un clic couvre tous les onglets, et au déverrouillage tout redevient exactement comme avant — aucun rechargement, aucun formulaire perdu, aucune vidéo interrompue.

> Chrome · Edge · Firefox · Manifest V3 · Autorisations minimales · Aucune analyse · 100 % local

---

## Pourquoi VKT VeilMate ?

Vous allez chercher un café. Quelqu'un jette un œil à votre écran : un e-mail à moitié écrit, un onglet bancaire, un message privé. Vous voulez une couverture à jeter sur le navigateur, pas un produit de sécurité.

Les extensions de « verrouillage du navigateur » ratent en général l'un des deux points suivants :

| Leur approche | Ce qui casse |
|---|---|
| Rediriger chaque onglet vers une page de verrouillage | Au déverrouillage, tout se recharge : formulaires perdus, vidéo relancée, état de la SPA détruit |
| Promettre d'« empêcher tout accès non autorisé » | Un nouveau profil, une fenêtre privée ou le gestionnaire de tâches passent outre, et les avis le disent |

VKT VeilMate prend la position inverse :

| Notre approche | Résultat |
|---|---|
| **Couvrir, jamais rediriger** — une couche de shadow DOM est injectée dans chaque page | Le déverrouillage est instantané et sans perte |
| **Dire ce qu'il ne peut pas faire** — sur la page de réglages et dans la fiche du magasin | Pas d'attentes déçues, pas d'avis à une étoile pour une promesse intenable |
| **Aucun chemin de retour** — pas de code de récupération, pas d'API de réinitialisation, et le verrouillage survit au redémarrage | Un rideau contournable n'est pas un rideau ; oublier son mot de passe impose de supprimer l'extension, et chaque écran le rappelle |

---

## Fonctionnalités

### 🆓 Gratuit pour toujours

| Fonction | Détail |
|---|---|
| Verrouillage en un clic | Bouton de la barre d'outils — aucun raccourci clavier n'est enregistré |
| Liste d'exceptions | Jusqu'à 10 domaines restent lisibles, tout le reste est couvert |
| Couche sans perte | Chaque onglet http/https est couvert sur place ; rien ne se recharge |
| Blocage des interactions | Sur une page couverte, clics, défilement, clavier, glisser, copie et menu contextuel sont stoppés ; au verrouillage, le focus revient sur la couche pour que les frappes ne partent pas dans un éditeur en iframe |
| Nouveaux onglets et barre d'adresse | Les nouveaux onglets, fenêtres et adresses saisies sont interceptés pendant le verrouillage |
| Déverrouillage par mot de passe | PBKDF2-SHA256, 310 000 itérations, sel aléatoire, comparaison à temps constant |
| Verrouillage persistant | L'état vit dans `storage.local` ; redémarrer le navigateur ne le lève pas |
| Aucune récupération | Supprimer l'extension dans `chrome://extensions` est la seule issue en cas de mot de passe oublié |
| Verrouillage automatique | Utilise la détection d'inactivité du navigateur |
| Attente croissante | Cinq échecs → 30 secondes, puis 2 minutes, 10 minutes, 30 minutes et enfin une heure. Toute vérification du mot de passe — déverrouillage comme changement — compte sur le même compteur |
| Titres d'onglet masqués | Pendant le verrouillage, la barre d'onglets et le titre de la fenêtre affichent un nom neutre au lieu de la page que vous lisiez |
| Menu contextuel | Tout verrouiller ou garder le site courant lisible, sans ouvrir le panneau |
| Grande horloge | Grande horloge sur l'écran de verrouillage, 12/24 h, date facultative |
| Six langues | English, 中文, 日本語, Deutsch, Español, Français |

### ⭐ Pro (licence requise)

| Fonction | Détail |
|---|---|
| Verrouillage ciblé | Passer la liste de domaines en « couvrir seulement… » : verrouiller l'intranet, laisser le reste lisible. Aussi depuis le menu contextuel. La version gratuite est limitée à 10 domaines et fonctionne toujours en « couvrir tout sauf… » |
| Verrouillage à heure fixe | Tout couvrir à l'heure choisie, chaque jour ou du lundi au vendredi. Une alarme unique qui se replanifie après chaque déclenchement ; une échéance manquée pendant que le navigateur était fermé ne verrouille pas au démarrage |
| Fenêtre sans mot de passe | Quelques minutes après un vrai déverrouillage, un nouveau verrouillage peut être levé sans saisir le mot de passe. Le raccourci ne se prolonge pas tout seul, un redémarrage du navigateur le redemande toujours, et changer le mot de passe l'annule aussitôt |
| Déverrouillage biométrique | Windows Hello / Touch ID via WebAuthn, le mot de passe restant toujours disponible. **Un raccourci pour éviter de taper, pas une seconde clé** : la vérification se fait sur l'écran de verrouillage, et qui ouvre les DevTools là peut envoyer le même message — le même niveau que quelqu'un devant le clavier. La limite reste la vérification du mot de passe |
| Verrouillage à la perte de focus | Verrouille quelques secondes après le passage à une autre application |
| Lien avec le verrouillage du système | Suit le verrouillage d'écran du système d'exploitation |
| Verrouillage au démarrage | Demande le mot de passe à la première ouverture du navigateur |
| Rideau de confidentialité | Floute la page courante sans verrouiller ; un clic la révèle |
| Page leurre | Les pages couvertes ressemblent à un banal « Ce site est inaccessible » plutôt qu'à un écran de verrouillage évident ; « Recharger » mène à l'écran de verrouillage |
| Journal des verrouillages | Historique local des tentatives de déverrouillage sur cet appareil, y compris les vérifications faites depuis le formulaire de changement de mot de passe |
| Fond d'écran et message | Six dégradés intégrés ou votre image, plus une ligne personnalisée sur l'écran de verrouillage |
| Synchronisation entre appareils | L'apparence de l'écran de verrouillage, l'horloge, les préférences de verrouillage automatique **et la liste de domaines** passent par `chrome.storage.sync` (Chrome via Google, Edge via Microsoft, Firefox via Firefox Sync). Les changements sont envoyés seuls un instant après l'enregistrement et récupérés dès que l'autre appareil écrit. Le mot de passe n'est jamais synchronisé ; une image importée dépasse le quota de 8 Ko par élément, seuls les dégradés intégrés voyagent |

---

## Aperçu

> 📸 Les visuels du magasin et les captures sont dans [`screenshots/`](../screenshots/) : six captures 1280×800, plus les visuels 1400×560 et 440×280.

| Capture | Contenu |
|---|---|
| [`01-lock-all-tabs.png`](../screenshots/01-lock-all-tabs.png) | Un clic couvre tous les onglets de toutes les fenêtres |
| [`02-lock-screen.png`](../screenshots/02-lock-screen.png) | Déverrouillage sur l'écran de verrouillage avec la grande horloge |
| [`03-popup.png`](../screenshots/03-popup.png) | La fenêtre contextuelle : verrouiller, définir le mot de passe, état Pro |
| [`04-auto-lock-scope.png`](../screenshots/04-auto-lock-scope.png) | Verrouillage automatique et portée du verrouillage (liste de domaines) |
| [`05-honest.png`](../screenshots/05-honest.png) | Le tableau « il peut / il ne peut pas » |
| [`06-security.png`](../screenshots/06-security.png) | Réglages du mot de passe et de la biométrie |

---

## Navigateurs pris en charge

| Navigateur | État | Version minimale | Remarques |
|---------|-------|------------------|-----------|
| Google Chrome | ✅ Entièrement pris en charge | Chrome 116+ | Manifest V3, service worker |
| Microsoft Edge | ✅ Entièrement pris en charge | Edge 116+ | Même build, basé sur Chromium |
| Autres navigateurs Chromium (Brave, Vivaldi, Opera) | ⚠️ Au mieux | Chromium 116+ | Non testé ; mêmes API |
| Mozilla Firefox | ✅ Pris en charge | Firefox 121+ | Build MV3 maintenu dans le dépôt Firefox dédié |
| Navigateurs mobiles | ❌ Non pris en charge | — | Pas de barre d'outils à cliquer ni de modèle de fenêtres à couvrir |

> **Windows Hello / Touch ID** dépendent de WebAuthn sur la plateforme : Windows 10 1903+ avec un code PIN ou une empreinte configurés, ou macOS avec Touch ID. Le mot de passe reste toujours disponible : une machine sans biométrie ne perd que le confort.

---

## Installation

| Magasin | Lien |
|---|---|
| Chrome Web Store | 🔜 En cours d'examen — le lien sera ajouté à la publication |
| Microsoft Edge Add-ons | 🔜 En cours d'examen — le lien sera ajouté à la publication |
| Firefox Add-ons (AMO) | [Installer pour Firefox](https://addons.mozilla.org/firefox/addon/vkt-veilmate/) |

> Installez uniquement depuis les magasins officiels ci-dessus.

---

## Utilisation

### Première configuration

1. Cliquez sur l'icône de la barre → **Définir un mot de passe**. Il n'y a pas de code de récupération : notez le mot de passe lui-même en lieu sûr.
2. Cliquez sur **Verrouiller maintenant** quand vous quittez votre poste.
3. Déverrouillez sur l'écran de verrouillage avec le mot de passe ou, en Pro, la biométrie.

### Configurer la portée du verrouillage

Les domaines sont comparés sur le suffixe avec frontière de point : `example.com` couvre `example.com`, `www.example.com` et `a.b.example.com`, mais pas `notexample.com`. Le schéma, le `www.` initial, le chemin, le port et un préfixe générique sont retirés automatiquement ; un `com` seul est refusé.

Les pages sans nom d'hôte (`chrome://`, `file://`, `about:blank`, PDF locaux, pages d'extension) sont toujours couvertes, quoi que dise la liste : celle-ci ne s'applique qu'à http et https.

### Mot de passe oublié

Il n'existe qu'une issue : **supprimer l'extension dans `chrome://extensions` puis la réinstaller.**

Cela efface aussi le fond d'écran et tous les réglages. Il n'y a ni code de récupération, ni API de réinitialisation, ni support capable de vous déverrouiller — un verrou avec une porte dérobée n'est pas un verrou. Fermer le navigateur n'aide pas non plus : l'état vit dans `storage.local` et reste après un redémarrage.

Le panneau « mot de passe oublié » de l'écran de verrouillage renvoie directement à `chrome://extensions/?id=<cette extension>` : vous n'êtes jamais sans issue, seulement sans raccourci.

---

## Comment ça marche

```
Déclencheur (bouton / menu contextuel / inactivité / perte de focus / verrouillage système / démarrage / heure fixe)
  → état de verrouillage écrit dans storage.local (survit au redémarrage du navigateur)
  → pour chaque onglet http(s) : tabs.sendMessage({type:'veil:lock'}) → couche injectée
  → pour les onglets non injectables : mémoriser l'URL, tabs.update(lock.html)
  → tabs.onCreated / tabs.onUpdated continuent d'intercepter tout ce qui apparaît
  → windows.onCreated couvre Ctrl+N, « ouvrir dans une nouvelle fenêtre » et les fenêtres privées
  → chrome://extensions/?id=<soi-même> est la seule page interne autorisée, pour que
    l'extension puisse toujours être supprimée
Déverrouillage
  → mot de passe / WebAuthn vérifiés sur la page de l'extension
  → état effacé, couches retirées, onglets remplacés restaurés sur place
```

Décisions de conception à connaître :

- **Les mots de passe ne se saisissent que sur les pages de l'extension.** Le JavaScript d'un site ne voit jamais le champ : aucun site ne peut l'espionner.
- **Le hachage se fait dans le service worker.** Seul `{salt, iter, hash}` est stocké ; le mot de passe lui-même n'est jamais écrit.
- **Comparaison à temps constant.** La comparaison des empreintes ne fuit aucune information de temps.
- **La couche vit dans une shadow root fermée.** Les scripts de la page n'y entrent pas et ne peuvent pas restyler l'intérieur. L'élément hôte, lui, est dans le document : une feuille de style du site peut le cibler — c'est pourquoi les propriétés critiques sont écrites en `!important` inline, et qu'une garde remet la couche en place si elle est supprimée ou masquée.

---

## Questions fréquentes

**Le verrouillage survit-il à la fermeture du navigateur ?** Oui. L'état est écrit dans `storage.local` : le navigateur s'ouvre verrouillé jusqu'au déverrouillage.

**Est-ce un produit de sécurité ?** Non. Il cache les onglets à ceux qui passent. Quelqu'un qui contrôle la machine peut le désactiver dans `chrome://extensions`, utiliser un autre profil ou fermer le navigateur depuis le gestionnaire de tâches. Tout cela figure aussi dans la fiche du magasin.

**Pourquoi aucune récupération de mot de passe ?** Un code de récupération est une seconde clé, et une seconde clé est une porte dérobée. La seule issue est de supprimer l'extension, ce qui est écrit sur l'écran de verrouillage lui-même.

**La biométrie est-elle une seconde entrée ?** C'est un raccourci, pas une seconde clé. La vérification du mot de passe vit dans le service worker, et les deux endroits où un mot de passe est soumis — déverrouillage et changement de mot de passe — passent par le même compteur et la même attente. La fenêtre sans mot de passe ne vérifie aucun mot de passe : elle ne vaut que quelques minutes après un vrai déverrouillage et laisse une entrée `quick` dans le journal. Mais qui peut ouvrir les DevTools sur une page de l'extension peut piloter l'API de messages de l'extension, et aucune extension ne l'empêche. Voyez la biométrie comme « taper moins », pas comme « plus sûr ».

**Que se passe-t-il après le cinquième échec ?** Une pause de 30 secondes, puis 2 minutes, 10 minutes, 30 minutes et enfin une heure entre les tentatives. Le compteur est propre à l'appareil et visible dans le journal.

**Est-ce que quelque chose est envoyé ?** Ni contenu de page, ni URL, ni frappes, ni capture d'écran. La seule requête sortante est l'activation ou la validation de licence.

**Pourquoi la liste est-elle limitée à 10 domaines en gratuit ?** Le mode gratuit est « couvrir tout sauf… » : une liste courte couvre le cas réaliste (webmail, agenda, la page en cours de lecture). Le mode inverse, « couvrir seulement… », est ce dont un portable de travail a besoin et fait partie de Pro.

**Une licence pour deux navigateurs ?** Oui, une licence active deux navigateurs ; la retirer de l'un libère cette place.

---

## Confidentialité

- Aucune analyse, aucune télémétrie, aucune publicité, aucun compte.
- Aucun contenu de page, URL, titre ou frappe ne quitte le navigateur.
- Le fond d'écran et le message restent sur votre appareil : les images importées sont redimensionnées et conservées dans ce profil du navigateur, jamais envoyées.
- La synchronisation entre appareils (Pro) utilise `chrome.storage.sync`, le canal propre au navigateur. Il n'y a aucun serveur de notre côté sur ce chemin et nous ne pouvons pas le lire. Le mot de passe en est volontairement exclu, et les images importées dépassent le quota : seuls les champs de préférences voyagent.
- La seule requête réseau est l'activation ou la validation de licence, et uniquement si vous collez une clé.

- [Politique de confidentialité complète](https://annmax1983.github.io/vkt-veil-mate/privacy-policy.html)

### Autorisations

| Autorisation | Pourquoi |
|---|---|
| `storage` | Enregistrer les réglages (empreintes uniquement), l'état persistant du verrouillage et les données Pro via `storage.sync` |
| `tabs` | Couvrir les onglets, intercepter les nouveaux onglets et les adresses saisies pendant le verrouillage |
| `windows` | Réagir aux changements de focus pour le verrouillage à la perte de focus |
| `idle` | Verrouillage automatique en cas d'inactivité |
| `alarms` | Le verrouillage à heure fixe et le verrouillage différé à la perte de focus, sans dépendre du service de fond |
| `contextMenus` | Le menu contextuel (tout verrouiller / garder ce site lisible) |
| `https://api.annmax1983.com/*` | Uniquement l'activation et la validation de licence |

Les content scripts s'exécutent sur `http://*/*` et `https://*/*` et ne font qu'une chose : peindre la couche quand le service worker le demande.

---

## Droits d'auteur

1. VKT VeilMate couvre les pages du navigateur sur votre propre appareil et ne modifie, ne stocke ni ne transmet le contenu d'aucun site.
2. Les droits d'auteur du contenu couvert appartiennent à leurs éditeurs ; VKT VeilMate n'en revendique aucun.
3. L'utilisation de cette extension implique le respect des lois locales et des politiques d'appareil et d'usage acceptable de votre organisation.

---

## Avis sur le code source

> ⚠️ **Ce dépôt sert au développement et à l'empaquetage des versions.** Le code est propriétaire et ne peut être redistribué ni réempaqueté. L'extension est distribuée via les magasins officiels de navigateurs (Chrome Web Store, Microsoft Edge Add-ons, Firefox Add-ons (AMO)) ; aucun paquet d'installation hors ligne n'est fourni aux utilisateurs finaux.

---

## Licence

Copyright © 2026 VKT VeilMate. Tous droits réservés.

Ce logiciel est un logiciel propriétaire à code fermé. Sans autorisation écrite officielle, il est strictement interdit de :
- Décompiler, cracker ou modifier le code du programme
- Réempaqueter, redistribuer, partager ou revendre à des fins commerciales
- Intégrer le programme dans un autre logiciel pour une distribution groupée

---

## ❤️ Soutien

Si VKT VeilMate vous est utile, offrez un café au développeur !

**[👉 Obtenir une licence](https://annmax1983.com/extensions/veilmate)** · **[☕ M'offrir un café](https://ko-fi.com/annmax?ref=vkt-veil-mate)** · [Code sur GitHub](https://github.com/annmax1983/vkt-veil-mate) · [Site officiel](https://annmax1983.com/)
