# Phase 4 : L'Investigation 🔍

## 🎯 Objectif

Découvrir que Git ne perd **jamais** rien. Vous allez enquêter sur la branche d'un autre étudiant pour retrouver un commit "supprimé", décoder un secret, et prouver vos talents de détective Git !

## 🕵️ La Mission

Vous avez supprimé votre commit avec le `.env` dans la Phase 4... mais Git garde trace de **tout** dans le reflog !

Dans cette phase, vous allez :
1. Recevoir l'assignation de la branche d'un autre étudiant (l'instructeur vous la donnera)
2. Fouiller dans son historique pour trouver le commit "disparu"
3. Récupérer le fichier `.env`
4. Décoder la clé API (encodée en base64)
5. Vérifier qu'elle correspond bien au nom de l'étudiant

---

## 📋 Consignes

### 1. Récupérer votre assignation

L'instructeur va vous attribuer la branche d'un autre étudiant. Notez bien son nom !

**Exemple** : Vous êtes Alice et on vous demande d'analyser la branche de `student/bob-martin`

---

### 2. Récupérer la branche

**À faire** :
- Récupérez toutes les branches depuis le dépôt distant
- Listez les branches distantes pour voir celle qui vous a été assignée
- Basculez sur la branche de l'étudiant assigné

💡 Cherchez comment récupérer les branches distantes et comment basculer vers une branche.

---

### 3. Utiliser le reflog

Le **reflog** (reference log) est l'historique de **tous** les mouvements de HEAD, y compris les commits supprimés !

**À faire** :
- Consultez le reflog de la branche actuelle
- Cherchez une entrée mentionnant "reset" ou le message `chore: add API configuration`
- Notez le hash du commit supprimé

🔍 **Ce que vous allez trouver** :
- L'état actuel (après le reset) avec mention "reset: moving to HEAD~1"
- Juste avant : le commit supprimé avec le message `chore: add API configuration`
- Notez bien le hash de ce commit !

💡 Cherchez comment afficher le journal de référence Git.

---

### 4. Récupérer le commit perdu

Maintenant que vous avez le hash du commit, vous pouvez consulter son contenu.

**À faire** :
- Affichez le contenu complet du commit perdu (avec son hash)
- Ou mieux : extrayez directement le fichier `.env` de ce commit

**Résultat attendu** :
Vous devriez voir un fichier `.env` contenant :
```
API_KEY=<chaîne_base64>
```

💡 Cherchez comment afficher le contenu d'un commit spécifique ou extraire un fichier d'un commit.

---

### 5. Décoder la clé API

La clé est encodée en **base64**. Vous devez la décoder.

**À faire** :
- Copiez la valeur de `API_KEY` (la chaîne encodée en base64)
- Décodez-la depuis le base64 vers du texte normal

**Résultat attendu** : Le nom de l'étudiant au format `prenom-nom`

✅ Si le nom décodé correspond au nom de la branche (ex: `student/bob-martin` → `bob-martin`), vous avez réussi !

💡 Cherchez comment décoder du base64 en ligne de commande.

---

### 6. Valider avec l'instructeur

Allez voir l'instructeur et annoncez-lui :

> "J'ai retrouvé le secret de [Nom de l'étudiant] : la clé décode en [nom-décodé]"

---

## 🧠 Comprendre le Reflog

### Qu'est-ce que le reflog ?

Le reflog est un **journal local** qui enregistre tous les mouvements de HEAD :
- Commits
- Checkouts
- Resets
- Rebases
- Merges
- etc.

### Pourquoi c'est utile ?

- 🛟 **Récupération de désastre** : Annuler un reset/rebase raté
- 🔍 **Investigation** : Comprendre ce qui s'est passé
- 🕐 **Machine à remonter le temps** : Revenir à n'importe quel état passé

### Combien de temps Git garde les commits ?

- **Commits référencés** : Pour toujours
- **Commits "perdus" dans le reflog** : ~90 jours par défaut
- Après 90 jours : Git garbage collector les supprime définitivement

---

## 💡 Techniques Avancées

### Naviguer dans le reflog

Vous pouvez :
- Voir tout le reflog
- Limiter le nombre d'entrées affichées (ex: les 10 dernières)
- Afficher le reflog avec plus de détails

### Récupérer un commit perdu

Plusieurs options possibles :
- **Créer une branche** pointant vers le commit perdu
- **Checkout** directement le commit (mode detached HEAD)
- **Cherry-pick** le commit sur votre branche actuelle

### Consulter un commit sans checkout

Vous pouvez :
- Voir tous les changements d'un commit
- Extraire un fichier spécifique d'un commit
- Lister l'arbre des fichiers d'un commit

💡 Ces techniques sont utiles pour explorer l'historique sans modifier votre état actuel.

---

## 🎓 Ce qu'il Faut Retenir

### Git ne supprime (presque) jamais rien

- Reset et rebase ne **suppriment pas** les commits
- Ils les **déréférencent** (plus pointés par une branche)
- Les commits restent accessibles via le reflog pendant ~90 jours

### Implications de sécurité

Si vous avez commité un **vrai** secret (mot de passe, clé API, token) :

1. ❌ Le supprimer de l'historique n'est **pas suffisant**
2. ❌ Il reste dans le reflog local et distant
3. ❌ Il peut avoir été cloné par d'autres
4. ✅ **Solution** : Considérer le secret comme **compromis** et le changer immédiatement !

### Outils pour nettoyer réellement

Pour supprimer définitivement un fichier de tout l'historique, des outils spécialisés existent :
- **filter-branch** (ancien, déprécié)
- **filter-repo** (recommandé actuellement)
- **BFG Repo-Cleaner** (le plus rapide)

⚠️ Ces outils réécrivent **tout** l'historique du projet !

---

## ✅ Vérification

Votre phase 4 est réussie si :

- ✓ Vous avez trouvé le commit "disparu" avec le reflog
- ✓ Vous avez extrait le fichier `.env`
- ✓ Vous avez décodé la clé base64
- ✓ Le nom décodé correspond au nom de l'étudiant
- ✓ Vous avez validé avec l'instructeur

---

## 🎉 Félicitations !

Vous avez terminé le TD Git ! Vous maîtrisez maintenant :

- ✅ La création et gestion de branches
- ✅ Les Git Hooks pour automatiser la qualité
- ✅ La réécriture d'historique (reset, rebase)
- ✅ La récupération de commits perdus (reflog)
- ✅ Les bonnes pratiques de sécurité avec Git

### 🚀 Pour aller plus loin

Consultez la section [Ressources Additionnelles](../README.md#-ressources-additionnelles) du README pour approfondir vos connaissances !

**Bravo !** 👏
