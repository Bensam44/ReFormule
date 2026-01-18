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




