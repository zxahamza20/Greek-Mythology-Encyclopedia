# 🏛️ Greek Mythology Encyclopedia

An interactive encyclopedia of Greek mythology, built with a **graph database (Neo4j)** and a modern web stack. Explore gods, heroes, titans, monsters, artifacts, and weapons. Every entity page contains bidirectional hyperlinks (e.g., Zeus ⇄ Thunderbolt) and interactive family trees.

[![FastAPI](https://img.shields.io/badge/FastAPI-0.115.0-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-14.2.0-000000?logo=next.js)](https://nextjs.org/)
[![Neo4j](https://img.shields.io/badge/Neo4j-5.20-008CC1?logo=neo4j)](https://neo4j.com/)
[![Tailwind](https://img.shields.io/badge/Tailwind-3.4.0-06B6D4?logo=tailwindcss)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📖 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture Overview](#architecture-overview)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Backend Setup (FastAPI + Neo4j)](#2-backend-setup-fastapi--neo4j)
  - [3. Frontend Setup (Next.js)](#3-frontend-setup-nextjs)
  - [4. Running with Docker Compose (Optional)](#4-running-with-docker-compose-optional)
- [Environment Variables](#environment-variables)
- [Database Schema (Neo4j)](#database-schema-neo4j)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
  - [Backend (Railway / Fly.io)](#backend-railway--flyio)
  - [Frontend (Vercel)](#frontend-vercel)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

---

## ✨ Features

- **6 Main Categories** – Gods, Heroes, Titans, Monsters, Artifacts, Weapons.
- **Picture Grid Lists** – Each category shows a responsive grid of entity cards with images.
- **Entity Detail Pages** – Rich information, descriptions, attributes, and bidirectional links.
- **Bidirectional Hyperlinks** – Clicking “thunderbolt” on Zeus’s page takes you to the Thunderbolt page, which links back to Zeus automatically.
- **Interactive Family Tree** – Visual graph using Cytoscape.js (dagre layout) showing relationships.
- **Global Search** – Instant search from the navbar; redirects to exact matches or shows results.
- **Random Page** – Discover a random entity with one click.
- **Dark / Light Mode** – Theme toggle powered by `next-themes`.
- **Responsive Design** – Tailwind CSS flexbox/grid works on all devices.
- **Optional Redis Caching** – Cache API responses for performance (can start without).

---

## 🧰 Tech Stack

| Layer          | Technology                                                                 |
|----------------|----------------------------------------------------------------------------|
| **Database**   | Neo4j (AuraDB free tier or local Docker container) – Graph database        |
| **Query Lang** | Cypher                                                                     |
| **Backend**    | FastAPI (Python), Uvicorn, neo4j Python driver (async), Redis (optional)   |
| **Frontend**   | Next.js 14+ (App Router), React, TypeScript, Tailwind CSS                  |
| **Visualization** | Cytoscape.js + cytoscape-dagre                                           |
| **Theming**    | next-themes                                                                |
| **Data Fetching** | SWR (optional) or native `fetch`                                         |
| **Deployment** | Vercel (frontend), Railway / Fly.io (backend), Neo4j Aura                  |
| **Dev Tools**  | Poetry (Python), pnpm/npm, Docker, GitHub Actions (optional)               |

> **Minimal Viable Version** (without optional extras)  
> Neo4j + FastAPI + Next.js + Tailwind + Cytoscape.js + Vercel/Railway

---

## 🧱 Architecture Overview
User Browser
│
▼
[Vercel – Next.js Frontend]
│
│ (REST API calls)
▼
[Railway/Fly.io – FastAPI Backend]
│
│ (Cypher queries)
▼
[Neo4j Aura – Graph Database]


- The **frontend** is a static + server‑rendered Next.js app.
- The **backend** provides REST endpoints for entities, categories, search, and relationship graphs.
- **Neo4j** stores entities as nodes (with labels like `:God`, `:Hero`, `:Weapon`) and relationships like `[:WIELDS]`, `[:PARENT_OF]`, `[:DEFEATED_BY]`.
- Bidirectional links are handled by the backend returning both `outgoing_links` and `incoming_links` for each entity.

---

## 📁 Project Structure
greek-mythology-encyclopedia/
├── .github/workflows/ # CI/CD (optional)
├── backend/ # FastAPI application
│ ├── app/
│ │ ├── api/ # Routes & dependencies
│ │ ├── config.py # Settings (Neo4j URI, Redis, etc.)
│ │ ├── database/ # Neo4j & Redis clients
│ │ ├── main.py # FastAPI app entry point
│ │ ├── models/ # Pydantic models
│ │ ├── repositories/ # Cypher queries
│ │ ├── services/ # Business logic
│ │ └── utils/ # Helpers
│ ├── tests/
│ ├── pyproject.toml # Poetry dependencies
│ ├── Dockerfile
│ └── .env.example
├── frontend/ # Next.js application
│ ├── app/
│ │ ├── (categories)/ # Route groups: gods, heroes, etc.
│ │ ├── entity/[slug]/ # Dynamic entity page
│ │ ├── family-tree/
│ │ ├── search/
│ │ ├── layout.tsx
│ │ └── page.tsx # Homepage with 6 flexbox containers
│ ├── components/
│ │ ├── navbar/ # Navbar, search bar, theme toggle
│ │ └── ui/ # EntityGrid, EntityCard, FamilyGraph, HyperlinkText
│ ├── lib/ # API client, types, constants
│ ├── hooks/ # useDebounce, useEntity
│ ├── public/ # Static images
│ ├── tailwind.config.ts
│ └── .env.local.example
├── docker-compose.yml # Local Neo4j + Redis + backend
├── .gitignore
└── README.md
---

## 🔧 Prerequisites

- **Node.js** 18+ and **pnpm** / npm / yarn
- **Python** 3.10+ and **Poetry** (recommended) or pip
- **Docker** (optional, for local Neo4j)
- A **Neo4j Aura** free instance or local Docker Neo4j container

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/greek-mythology-encyclopedia.git
cd greek-mythology-encyclopedia
```

To be continued
