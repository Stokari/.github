# 📦 Stokari

**Keep track of your shop's stock and sales, even when the internet isn't there.**

<p align="center">
  <img src="https://placehold.co/160x160/png?text=Stokari+logo" alt="Stokari logo" width="140" height="140" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-early%20development-orange" alt="Early development" />
  <img src="https://img.shields.io/badge/approach-offline--first-blue" alt="Offline first" />
  <img src="https://img.shields.io/badge/app-installable%20PWA-purple" alt="Installable PWA" />
</p>

## Why Stokari?

Imagine running a small shop in Merkato. You track your stock in a notebook or an Excel sheet. When the internet goes down, you still need to sell products, record deliveries, and know what is left.

Now imagine you have an affordable Android phone, an unreliable internet connection, and inventory software that assumes you are always online.

**Stokari is being built for that reality.**

Stokari is an offline-first inventory and sales management application designed for small retailers. It aims to make everyday stock management simpler, even with unreliable connectivity.

> **Project status:** Stokari is in early development. The Software Requirements Specification (SRS v0.5) and Software Design Document (SDD v0.2) have been prepared, but most of the application code has not yet been written. Features described here are planned, not necessarily implemented.

## What We're Building

- **Record sales anywhere:** Record sales even when the internet is unavailable and synchronize them when connectivity returns.
- **Track deliveries:** Record incoming stock and keep inventory quantities up to date.
- **Understand stock history:** Keep a history of stock movements so changes can be traced.
- **Get low-stock warnings:** Identify products that need restocking and view daily sales summaries.
- **Manage attendants:** Give shop owners a way to manage attendants and control their permissions.
- **Handle offline conflicts:** Preserve offline sales and flag inventory conflicts for review instead of silently losing transactions.

### What happens when two devices sell the same stock offline?

Suppose a shop has 10 units of a product. Two devices go offline and sell some of those units independently. When they reconnect, the server may discover that the combined sales exceed the available stock.

Stokari is designed to preserve both sales and flag the resulting discrepancy for the owner to review.

| Scenario                                   | Intended behavior                                                                                      |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| Starting stock: 10; offline sales: 2 and 3 | Both sales are synchronized; 5 units remain.                                                           |
| Starting stock: 10; offline sales: 7 and 6 | Both sales are preserved and flagged for review because the combined sales exceed the available stock. |

The owner can then resolve the discrepancy, for example by cancelling an erroneous sale or correcting the stock count. Stock changes should be recorded rather than silently rewriting or deleting transaction history.

*These are planned behaviors; they have not yet been verified in a working implementation.*

## Built With

| Component                                 | Technology                                                                 |
| ----------------------------------------- | -------------------------------------------------------------------------- |
| Web application                           | React, TypeScript, Vite                                                    |
| Local storage                             | IndexedDB, Dexie                                                           |
| Data fetching and server-state management | TanStack Query                                                             |
| Backend API                               | Python, Django, Django REST Framework                                      |
| Database                                  | PostgreSQL                                                                 |
| Authentication                            | Google Sign-In using OpenID Connect (planned)                              |
| Offline support                           | Progressive Web App (PWA), Service Worker, IndexedDB, transactional outbox |
| Deployment                                | To be finalized                                                            |

### Architecture Overview

Stokari is planned as an offline-first Progressive Web App (PWA).

- **React + TypeScript** provides the user interface.
- **IndexedDB + Dexie** stores local data so supported workflows can continue while offline.
- **A Service Worker** supports the installable PWA experience and caching of the application shell.
- **TanStack Query** manages server-state fetching and synchronization with the API.
- **Django REST Framework** provides the backend API and handles business rules, inventory operations, and synchronization.
- **PostgreSQL** stores the authoritative shared inventory and transaction records.
- **Google Sign-In** is planned for user identity. Offline authorization must be handled separately so that previously authorized users can continue working during temporary connectivity loss.

The offline synchronization design is intended to use a transactional outbox, stable operation IDs, and idempotent server processing to reduce duplicate operations and preserve transactions across retries.

## Project Structure

The project is organized into separate repositories for the web application and backend API.

| Repository                                       | Description               |
| ------------------------------------------------ | ------------------------- |
| [`web`](https://github.com/ORG_NAME/web)         | React PWA frontend        |
| [`backend`](https://github.com/ORG_NAME/backend) | Django REST Framework API |

Replace `ORG_NAME` with the actual GitHub organization name if these repository URLs differ.

## Development Plan

The initial development plan spans four weeks.

| Week   | Focus                                                                                  |
| ------ | -------------------------------------------------------------------------------------- |
| Week 1 | Project setup, authentication foundation, database models, and core product management |
| Week 2 | Sales, stock movements, and inventory business rules                                   |
| Week 3 | Offline workflows, synchronization, and conflict handling                              |
| Week 4 | Testing, integration, usability improvements, and deployment preparation               |

The schedule is a target for the initial MVP, not a guarantee that every planned feature will be complete by the end of the fourth week.

## Contributing

Stokari is currently in early development. If you're interested in contributing, start by exploring the project repositories and reviewing the requirements and design documents.

Before implementing a feature, please coordinate with the team so that the implementation remains consistent with the planned architecture and inventory rules.

## Our Goal

Small retailers should not need a reliable internet connection or complicated software to understand what is happening in their shops.

**Stokari aims to make inventory management practical, reliable, and accessible—even when the internet isn't.**
