# Phase 3 : Nettoyer l'Historique 🧹

## 🎯 Objectif

Supprimer le commit contenant le fichier `.env` de votre historique Git. Ce fichier contient des secrets et ne devrait **jamais** être dans l'historique !

## ⚠️ Le Problème

Un fichier `.env` avec une clé API s'est retrouvé dans votre historique. C'est une **violation de sécurité grave** :

- 🚨 Les secrets ne doivent **jamais** être versionnés
- 🚨 Même si vous supprimez le fichier, il reste dans l'historique
- 🚨 N'importe qui peut consulter l'historique et récupérer la clé

**Votre mission** : Effacer ce commit comme s'il n'avait jamais existé.

---

## 📋 Consignes

### 1. Vérifier l'état actuel

Avant de modifier l'historique, examinez votre situation :

**À faire** :
- Consultez l'historique des derniers commits
- Vérifiez que le fichier `.env` existe bien dans votre répertoire de travail
- Identifiez le commit qui contient ce fichier (message : `chore: add API configuration`)

---

### 2. Choisir votre méthode

Vous avez **deux options** pour supprimer ce commit. Choisissez celle qui vous convient :

#### Option A : Reset Hard 🔨

**Simple et rapide** - Supprime le dernier commit

**Principe** :
- Déplace HEAD vers le commit précédent (`HEAD~1` = "le commit avant HEAD")
- Le mode "hard" supprime aussi les changements dans les fichiers
- Tout est perdu : commit + modifications

⚠️ **Attention** : Cette méthode est destructive !

**Quand utiliser** : Pour supprimer rapidement les 1-2 derniers commits

💡 Cherchez comment "réinitialiser fortement" l'historique Git.

---

#### Option B : Rebase Interactif 📝

**Plus flexible** - Réécrire l'historique interactivement

**Principe** :
- Lance un rebase en mode interactif avec une référence incluant les commits à modifier
- Un éditeur s'ouvre avec la liste des commits
- Devant chaque commit, vous pouvez choisir une action : `pick`, `drop`, `edit`, `reword`, `squash`

**Pour supprimer un commit** :
1. Changez `pick` en `drop` (ou supprimez la ligne entière)
2. Sauvegardez et fermez l'éditeur
3. L'historique sera réécrit automatiquement

**Quand utiliser** : Pour modifier plusieurs commits, en réorganiser, fusionner, etc.

💡 Vous devez inclure au moins 2 commits pour voir celui à supprimer. Cherchez la syntaxe du rebase interactif.

---

### 3. Vérifier la suppression

**Confirmez que le commit a bien disparu** :
- Consultez à nouveau l'historique des commits
- Le commit `chore: add API configuration` ne doit plus apparaître
- Vérifiez que le fichier `.env` n'existe plus dans votre répertoire

Si le fichier n'existe plus, c'est parfait ! ✅

---

### 4. Forcer le push

Comme vous avez réécrit l'historique local, vous devez **forcer le push** vers GitHub.

**Deux options de force push** :
- **Force simple** : Force brutale qui écrase l'historique distant
- **Force avec bail** (`with-lease`) : **Recommandé** - Vérifie que personne n'a poussé entre temps

⚠️ **DANGER** : Le force push écrase l'historique distant. À utiliser avec précaution !

💡 Préférez toujours l'option "with-lease" en production, c'est plus sûr. Cherchez comment forcer un push.

---

## 🤔 Comprendre la Différence

### Reset vs Rebase

| Aspect | Reset Hard | Rebase Interactif |
|--------|-----------|---------------|
| **Simplicité** | ✅ Très simple | 🔶 Plus complexe |
| **Flexibilité** | ❌ Limité aux derniers commits | ✅ Modifier n'importe quel commit |
| **Cas d'usage** | Annuler 1-2 derniers commits | Nettoyer tout l'historique |
| **Contrôle** | Tout ou rien | Granulaire (drop, edit, reword, squash) |

### Quand utiliser quoi ?

**Utilisez le reset si** :
- Vous voulez juste supprimer les 1-2 derniers commits
- Vous voulez faire vite
- Vous n'avez pas besoin de modifier les commits du milieu

**Utilisez le rebase si** :
- Vous devez modifier un commit au milieu de l'historique
- Vous voulez réorganiser plusieurs commits
- Vous voulez fusionner des commits entre eux

---

## 💡 Ce qu'il Faut Retenir

### Git ne supprime rien vraiment

Même après un `reset` ou `rebase`, Git conserve les commits dans le **reflog** pendant ~90 jours. Vous verrez ça dans la Phase 4 ! 👀

### Les bonnes pratiques

1. ✅ Ajoutez `.env` dans `.gitignore` **avant** de le créer
2. ✅ Ne committez **jamais** de secrets
3. ✅ Utilisez des variables d'environnement ou des gestionnaires de secrets
4. ✅ Si un secret est commité, considérez-le comme **compromis** et changez-le

---

## ✅ Vérification

Votre phase 3 est réussie si :

- ✓ Le commit avec `.env` n'apparaît plus dans l'historique
- ✓ Le fichier `.env` n'existe plus dans votre répertoire de travail
- ✓ Votre historique a été poussé sur GitHub (avec force)
- ✓ Vous comprenez la différence entre reset et rebase

---

## 🚀 Prochaine Étape

Le commit a disparu... ou pas ? Direction la [Phase 4 : L'Investigation](phase-4-recovery.md) pour découvrir que Git garde trace de tout ! 🔍
