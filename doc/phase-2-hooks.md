# Phase 2 : Git Hooks 🪝

## 🎯 Objectif

Créer un hook Git qui valide automatiquement le format des messages de commit. Votre Senior ne veut plus voir de messages de commit sales dans l'historique !

## 📋 Le Problème

Votre équipe veut adopter les **Conventional Commits** pour avoir un historique propre et générer automatiquement des changelogs. Mais certains développeurs oublient de respecter le format...

Votre mission : créer un hook `commit-msg` qui bloque les commits non conformes.

## 🔧 Consignes

### 1. Comprendre les Git Hooks

Les Git Hooks sont des **scripts** qui s'exécutent automatiquement lors d'événements Git (commit, push, merge, etc.).

Ils se trouvent dans : `.git/hooks/`

Le hook `commit-msg` s'exécute **avant** qu'un commit soit créé. Il reçoit le message de commit en paramètre et peut :
- ✅ Accepter le commit (exit code 0)
- ❌ Rejeter le commit (exit code != 0)

---

### 2. Créer le hook commit-msg

**Emplacement** : `.git/hooks/commit-msg`

Votre hook doit :
1. Lire le message de commit (passé en premier argument)
2. Vérifier qu'il commence par `feat:`, `fix:`, ou `chore:`
3. Si oui → exit 0 (commit accepté)
4. Si non → afficher un message d'erreur et exit 1 (commit rejeté)

💡 **Indices** :
- Le message de commit est dans le fichier dont le chemin est `$1`
- Utilisez `grep` pour chercher un pattern au début du message
- N'oubliez pas le shebang en début de fichier
- Le script doit être exécutable

---

### 3. Structure du hook

Votre script doit :
- Commencer par un shebang bash
- Lire le fichier contenant le message de commit (argument `$1`)
- Vérifier le format avec une regex ou grep
- Retourner 0 si valide, 1 si invalide
- Afficher un message d'erreur clair en cas de rejet

---

### 4. Tester votre hook

Testez votre hook avec plusieurs scénarios :

**Test 1** : Essayez de faire un commit vide avec un message commençant par `feat:`
- Le commit doit **réussir** ✅

**Test 2** : Essayez de faire un commit vide avec un message qui ne respecte pas le format
- Le commit doit **échouer** ❌
- Votre message d'erreur doit s'afficher

**Test 3** : Testez les autres préfixes valides (`fix:` et `chore:`)
- Les commits doivent **réussir** ✅

💡 Cherchez comment faire un commit vide pour tester sans créer de fichiers.

---

## 💡 Astuces

- Le message de commit peut avoir plusieurs lignes, vérifiez uniquement la première
- Utilisez `^` dans votre regex pour matcher le début de la ligne
- Pour débugger, ajoutez des `echo` dans votre script
- Si le hook ne s'exécute pas, vérifiez les permissions avec `ls -la .git/hooks/`

---

## ⚠️ Attention

- Le hook est **local** à votre machine (dans `.git/hooks/`)
- Il ne sera **pas** partagé via Git (le dossier `.git/` n'est jamais commité)
- En entreprise, on utilise des outils comme Husky pour partager les hooks

---

## ✅ Vérification

Votre phase 2 est réussie si :

- ✓ Le fichier `.git/hooks/commit-msg` existe et est exécutable
- ✓ Les commits avec `feat:`, `fix:`, `chore:` passent
- ✓ Les commits sans ces préfixes sont rejetés
- ✓ Un message d'erreur clair s'affiche en cas de rejet

---

## 🚀 Prochaine Étape

Bravo ! Votre hook fonctionne. 

⚠️ **Pause** : Attendez que l'instructeur vous indique de passer à la suite. Un "mystère" va apparaître dans votre historique...

Une fois prêt, passez à la [Phase 3 : Nettoyer l'Historique](phase-3-history.md) ! 🧹
