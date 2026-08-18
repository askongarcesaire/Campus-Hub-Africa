# CampusHub Africa

Réseau social académique connectant les étudiants d'Afrique francophone. La plateforme centralise les opportunités — bourses d'études, offres de stage, logement étudiant, conseils d'orientation — et facilite la connexion entre étudiants via un fil d'actualité, une messagerie instantanée, un annuaire par école/pays, et un espace de partage de ressources pédagogiques.

**Objectif :** faciliter la mobilité et la réussite académique des étudiants d'Afrique francophone.

**Stack :** Next.js (TypeScript) · Node.js / Express (TypeScript) · PostgreSQL · Socket.io

## Fonctionnalités

- **Authentification** — inscription/connexion sécurisée (JWT, mots de passe hashés)
- **Fil d'actualité** — publications catégorisées (bourses, stages, logement, général), likes, commentaires
- **Messagerie temps réel** — conversations privées instantanées via Socket.io, indicateurs de messages non lus
- **Annuaire** — recherche d'étudiants par nom, école, pays ou filière
- **Ressources pédagogiques** — partage de cours, anciens sujets d'examen et guides, filtrable par école/filière

## Architecture

```
campushub-africa/
├── backend/                 # API REST + WebSocket (Express + TypeScript)
│   ├── src/
│   │   ├── routes/          # auth, publications, utilisateurs, messages, ressources
│   │   ├── middleware/      # authentification JWT
│   │   ├── sockets/         # messagerie temps réel (Socket.io)
│   │   ├── types/           # types TypeScript partagés
│   │   ├── db.ts
│   │   └── server.ts
│   └── database/
│       └── schema.sql
└── frontend/                 # Interface Next.js (App Router, TypeScript)
    ├── app/
    │   ├── connexion/ inscription/
    │   ├── fil/ annuaire/ messagerie/ ressources/
    │   └── globals.css
    ├── components/
    └── lib/                  # client API, client Socket.io, types
```

## Installation

### Prérequis
- Node.js ≥ 18
- PostgreSQL ≥ 14

### 1. Base de données

```bash
createdb campushub
psql -d campushub -f backend/database/schema.sql
```

### 2. Backend

```bash
cd backend
cp .env.example .env
# Éditer .env avec vos identifiants PostgreSQL et un JWT_SECRET solide
npm install
npm run dev
```

L'API (REST + WebSocket) démarre sur `http://localhost:4000`.

### 3. Frontend

```bash
cd frontend
cp .env.local.example .env.local
npm install
npm run dev
```

L'application est disponible sur `http://localhost:3000`.

## Choix techniques

- **TypeScript de bout en bout** — cohérence des types entre le contrat d'API et l'interface
- **Socket.io** pour la messagerie temps réel, avec authentification par JWT sur le handshake WebSocket et gestion multi-appareils par utilisateur
- **Transactions et contraintes SQL** (clés étrangères, `CHECK`) pour garantir l'intégrité des données (catégories de publications, types de ressources)
- **Architecture REST classique** pour tout ce qui ne nécessite pas de temps réel (fil d'actualité, annuaire, ressources), Socket.io réservé à la messagerie

## Roadmap

- [ ] Upload direct de fichiers pour les ressources (actuellement liens externes)
- [ ] Notifications push pour les nouveaux messages
- [ ] Système de bourses avec dates limites et alertes
- [ ] Tests automatisés (Jest côté backend, Vitest côté frontend)
- [ ] Déploiement (Render/Railway pour le backend, Vercel pour le frontend)

## Auteur

Développé par Cesaire — [GitHub](https://github.com/) · [LinkedIn](https://linkedin.com/)

## Licence

MIT
