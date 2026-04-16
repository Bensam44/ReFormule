# ReFormule: projet de BACKEND 0 FAIRE:


# 🚀 Reformule — Backend Architecture (Plan & Roadmap)

Ce document décrit l’architecture prévue du backend de Reformule.  
Il servira de base pour la future implémentation (Render → Base44 → DeepSeek).

---

## 🧱 1. Objectifs du backend

- Servir d’intermédiaire sécurisé entre l’extension / web app et le moteur IA.
- Appliquer toutes les protections anti‑abus :
  - Anti‑bot
  - Anti‑boucle
  - Anti‑spam
  - Rate‑limit
  - Quotas Free / Pro / Business
  - Soft‑limit Business
- Protéger la clé API et le budget IA.
- Préparer la migration future vers DeepSeek.

---

## 🏗️ 2. Architecture générale
Extension / Web App
↓
Backend (Render)
↓
Base44 (temporaire)
↓
DeepSeek (plus tard)

Le backend sera hébergé sur **Render (Starter)** pour commencer.

---

## 📡 3. Endpoints prévus

### `POST /reformulate`
- Reçoit le texte à reformuler.
- Vérifie l’utilisateur (token / clé).
- Applique toutes les protections.
- Appelle Base44 (temporairement).
- Renvoie la reformulation.

### `GET /health`
- Vérifie que le backend fonctionne.
- Utilisé pour le monitoring.

### `GET /usage`
- Retourne les quotas et l’usage de l’utilisateur.

---

## 🛡️ 4. Système de protection (anti‑abus)

### ✔️ Rate‑limit
- 1 requête toutes les 2 secondes par utilisateur.
- 30 requêtes par minute maximum.

### ✔️ Limite de requêtes simultanées
- 1 requête active par utilisateur.

### ✔️ Anti‑boucle
- Blocage si 10 requêtes identiques consécutives.
- Blocage si 50 requêtes en 5 minutes.
- Blocage si 200 requêtes en 1 heure.

### ✔️ Anti‑bot
Détection automatique :
- Requêtes trop régulières.
- Activité 24/7.
- Requêtes identiques répétées.
- Volume anormal.

### ✔️ Validation du contenu
- Refus des requêtes vides.
- Refus des requêtes > 5000 caractères.

---

## 📊 5. Quotas & Plans

# 🎛️ Plans ReFormule — Quotas & Prix (Backend Officiel)

| Plan       | Prix / mois                 | PC inclus        | Tokens visibles | Tokens internes (backend) | Vitesse / Priorité        |
|------------|------------------------------|------------------|-----------------|----------------------------|----------------------------|
| **Free**   | 0 €                          | 1                | 6 000 / mois    | 6 000 / mois               | Lent                       |
| **Pro**    | 5 €                          | 1                | Illimité        | 400 000 / jour             | Normal                     |
| **Business** | 20 € pour 5 PC + 3 €/PC sup | 5 (extensible)   | Illimité        | 400 000 / jour             | Prioritaire (plus rapide)  |


---

## 🧩 6. Logs & Monitoring

- Logs des requêtes (user, timestamp, longueur, plan, résultat).
- Détection automatique des anomalies.
- Endpoint `/health` pour Render.

---

## 🧨 7. Fail‑safe global

Si le backend reçoit un volume anormal :
- > 200 000 requêtes / heure → mode sécurité.
- Réponses temporaires : “Maintenance automatique”.

---

## 🔧 8. Technologies prévues

- Node.js + Express
- Hébergement : Render (Starter)
- Base de données : à définir (PostgreSQL ou Redis)
- Appels IA :
  - Base44 (temporaire)
  - DeepSeek (plus tard)

---

## 🛠️ 9. Structure du projet (prévue)
/src
/routes
reformulate.js
health.js
usage.js
/services
base44.js
deepseek.js
/middleware
rateLimit.js
antiLoop.js
antiBot.js
validateInput.js
auth.js
/utils
logger.js
quota.js
softLimit.js
index.js

---

## 🗺️ 10. Roadmap

### Phase 1 — Mise en place du backend (Render)
- Créer le serveur Node.js
- Ajouter l’endpoint `/reformulate`
- Ajouter les protections anti‑abus
- Connecter Base44

### Phase 2 — Intégration avec l’extension
- Modifier l’extension pour appeler le backend
- Tester les quotas et protections

### Phase 3 — Migration vers DeepSeek
- Remplacer l’appel Base44 → DeepSeek
- Optimiser les coûts

### Phase 4 — Scalabilité
- Monitoring avancé
- Optimisation des performances
- Passage éventuel à Vercel Pro

---

## 📌 Statut actuel
Backend non implémenté — ce document sert de plan officiel pour la future mise en place.


---
Bien sûr Sam — je te prépare un **README.md** propre, clair, structuré, prêt à être collé dans GitHub.  
C’est un **plan d’architecture backend** pour Reformule, version “à implémenter plus tard”, mais déjà parfaitement organisé.

Tu peux le copier‑coller tel quel dans ton repo GitHub.

---

# 📄 **README.md — Backend Reformule (Plan d’Architecture & Roadmap)**

```markdown
# 🚀 Reformule — Backend Architecture (Plan & Roadmap)

Ce document décrit l’architecture prévue du backend de Reformule.  
Il servira de base pour la future implémentation (Render → Base44 → DeepSeek).

---

## 🧱 1. Objectifs du backend

- Servir d’intermédiaire sécurisé entre l’extension / web app et le moteur IA.
- Appliquer toutes les protections anti‑abus :
  - Anti‑bot
  - Anti‑boucle
  - Anti‑spam
  - Rate‑limit
  - Quotas Free / Pro / Business
  - Soft‑limit Business
- Protéger la clé API et le budget IA.
- Préparer la migration future vers DeepSeek.

---

## 🏗️ 2. Architecture générale

```
Extension / Web App
        ↓
     Backend (Render)
        ↓
     Base44 (temporaire)
        ↓
     DeepSeek (plus tard)
```

Le backend sera hébergé sur **Render (Starter)** pour commencer.

---

## 📡 3. Endpoints prévus

### `POST /reformulate`
- Reçoit le texte à reformuler.
- Vérifie l’utilisateur (token / clé).
- Applique toutes les protections.
- Appelle Base44 (temporairement).
- Renvoie la reformulation.

### `GET /health`
- Vérifie que le backend fonctionne.
- Utilisé pour le monitoring.

### `GET /usage`
- Retourne les quotas et l’usage de l’utilisateur.

---

## 🛡️ 4. Système de protection (anti‑abus)

### ✔️ Rate‑limit
- 1 requête toutes les 2 secondes par utilisateur.
- 30 requêtes par minute maximum.

### ✔️ Limite de requêtes simultanées
- 1 requête active par utilisateur.

### ✔️ Anti‑boucle
- Blocage si 10 requêtes identiques consécutives.
- Blocage si 50 requêtes en 5 minutes.
- Blocage si 200 requêtes en 1 heure.

### ✔️ Anti‑bot
Détection automatique :
- Requêtes trop régulières.
- Activité 24/7.
- Requêtes identiques répétées.
- Volume anormal.

### ✔️ Validation du contenu
- Refus des requêtes vides.
- Refus des requêtes > 5000 caractères.

---

## 📊 5. Quotas & Plans

### Free
- 100 reformulations / mois.

### Pro
- 300 reformulations / mois.

### Business
- Illimité (officiel).
- Soft‑limit interne :
  - 5000 / jour
  - 50 000 / mois

---

## 🧩 6. Logs & Monitoring

- Logs des requêtes (user, timestamp, longueur, plan, résultat).
- Détection automatique des anomalies.
- Endpoint `/health` pour Render.

---

## 🧨 7. Fail‑safe global

Si le backend reçoit un volume anormal :
- > 200 000 requêtes / heure → mode sécurité.
- Réponses temporaires : “Maintenance automatique”.

---

## 🔧 8. Technologies prévues

- Node.js + Express
- Hébergement : Render (Starter)
- Base de données : à définir (PostgreSQL ou Redis)
- Appels IA :
  - Base44 (temporaire)
  - DeepSeek (plus tard)

---

## 🛠️ 9. Structure du projet (prévue)

```
/src
  /routes
    reformulate.js
    health.js
    usage.js
  /services
    base44.js
    deepseek.js
  /middleware
    rateLimit.js
    antiLoop.js
    antiBot.js
    validateInput.js
    auth.js
  /utils
    logger.js
    quota.js
    softLimit.js
  index.js
```

---

## 🗺️ 10. Roadmap

### Phase 1 — Mise en place du backend (Render)
- Créer le serveur Node.js
- Ajouter l’endpoint `/reformulate`
- Ajouter les protections anti‑abus
- Connecter Base44

### Phase 2 — Intégration avec l’extension
- Modifier l’extension pour appeler le backend
- Tester les quotas et protections

### Phase 3 — Migration vers DeepSeek
- Remplacer l’appel Base44 → DeepSeek
- Optimiser les coûts

### Phase 4 — Scalabilité
- Monitoring avancé
- Optimisation des performances
- Passage éventuel à Vercel Pro

---

## 📌 Statut actuel
Backend non implémenté — ce document sert de plan officiel pour la future mise en place.

```

---

Si tu veux, je peux aussi te générer :

- un **CONTRIBUTING.md**  
- un **diagramme d’architecture**  
- un **plan de fichiers complet**  
- un **template de backend Node.js prêt à coller**
_______________________________________________________________________________________________________________________________________________________________________________________
                                                                    RESUME de ce qu'il reste à faire:
_________________________________________________________________________________________________________________________________________________________________________________________
Voici ce qu’il reste à faire, dans l’ordre le plus intelligent et le plus léger pour toi.

🧱 1. Créer la structure du backend dans ton repo GitHub
On prépare juste les dossiers vides, sans code pour l’instant.

Structure prévue :

Code
/src
  /routes
  /services
  /middleware
  /utils
index.js
package.json
.gitignore
C’est une étape rapide, propre, qui prépare le terrain.

🟦 2. Initialiser un projet Node.js minimal
On va créer un package.json propre, avec juste ce qu’il faut :

express

dotenv

cors

axios

Rien de plus pour l’instant.

🟩 3. Créer les endpoints vides
Juste les fichiers, sans logique :

/reformulate

/health

/usage

Ça te donne une base claire.

🟧 4. Héberger le backend sur Render (Starter)
On crée :

un service Web

on connecte ton repo GitHub

Render déploie automatiquement

tu obtiens ton URL publique (ex : https://reformule-backend.onrender.com)

Ton backend existe officiellement.

🟥 5. Connecter l’extension à TON backend
On change juste une ligne dans ton extension :

Avant :
→ l’extension appelle Base44

Après :
→ l’extension appelle ton backend

Ton backend appelle Base44 à ta place.

🟨 6. Ajouter les protections anti‑abus
On ajoute progressivement :

rate‑limit

anti‑boucle

anti‑bot

quotas Free / Pro / Business

soft‑limit Business

logs

monitoring

Tu seras blindé.

🟪 7. Migrer vers DeepSeek (plus tard)
Quand tu seras prêt, on change juste :

Code
services/base44.js → services/deepseek.js
Et ton backend devient 10× moins cher.

🎯 Résumé clair
Tu as déjà fait :

✔️ Création du repo
✔️ Ajout du README
✔️ Plan d’architecture validé

Il reste :

Créer la structure du backend

Initialiser Node.js

Ajouter les endpoints vides

Déployer sur Render

Connecter l’extension

Ajouter les protections

Migrer vers DeepSeek plus tard

----------------------------------------------------------------------------------------------------------------------------------------------------------

               NOUVEAU PLAN REFORMULE

------------------------------------------------------------------------------------------------------------------------------------------------------

# 🎛️ Plans ReFormule — Quotas & Prix (Backend Officiel)

| Plan       | Prix / mois                 | PC inclus        | Tokens visibles | Tokens internes (backend) | Vitesse / Priorité        |
|------------|------------------------------|------------------|-----------------|----------------------------|----------------------------|
| **Free**   | 0 €                          | 1                | 6 000 / mois    | 6 000 / mois               | Lent                       |
| **Pro**    | 5 €                          | 1                | Illimité        | 400 000 / jour             | Normal                     |
| **Business** | 20 € pour 5 PC + 3 €/PC sup | 5 (extensible)   | Illimité        | 400 000 / jour             | Prioritaire (plus rapide)  |


