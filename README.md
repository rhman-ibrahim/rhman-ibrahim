# Rhman

Welcome to my development hub. This repository is the central place where I organize, track, and showcase my projects as I work toward building a complete ecosystem of modern applications.

[Wiki](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki) | [Tasks](https://github.com/users/rhman-ibrahim/projects/8)

---

## 1. Who Am I

I am a dedicated full-stack developer, driven by the idea of creating software that is both meaningful and reliable. My background is rooted in ***Django*** and ***React***, where I’ve learned to value clarity, performance, and the craft of building applications that scale. I’ve set a personal challenge to build and complete five cornerstone projects that reflect my skills, discipline, and vision. This journey is not just about writing code; it is about establishing a foundation I can stand on—whether launching products, collaborating with teams, or pursuing opportunities in the tech industry. I believe in steady growth, practical learning, and creating solutions that serve real needs.

[![X](https://skillicons.dev/icons?i=twitter)](https://x.com/Rhman_Al_Warraq)

---

## 2. Tech Stack

### Django & DRF

Django gives me a stable, secure foundation for building applications, while Django REST Framework makes it easy to create flexible APIs that scale. Together, they provide structure, clarity, and reliability for backend development.

### React

React lets me build interactive, modern user interfaces with reusable components. Its speed, flexibility, and community support make it ideal for creating consistent, engaging user experiences that integrate seamlessly with my APIs.

### PostgreSQL

PostgreSQL is my choice for relational data storage due to its robustness, advanced features, and reliability in production. It ensures data integrity and performs well under the demands of complex, data-driven applications.

### Redis

Redis provides fast, in-memory caching and lightweight data structures. It helps reduce load times, manage sessions efficiently, and improve application responsiveness, making user experiences smoother without adding unnecessary complexity.

### Docker

Docker ensures consistency across development and deployment by containerizing applications. It eliminates environment issues, simplifies scaling, and supports efficient collaboration, making my projects portable and reliable in different contexts.

### GitHub

GitHub is my central platform for version control and collaboration. Beyond repositories and issues, I rely on GitHub Actions to automate testing, deployment, and CI/CD pipelines, ensuring consistent quality and faster delivery.

[![OS](https://skillicons.dev/icons?i=linux,bash,ubuntu)](https://skillicons.dev)

[![Base](https://skillicons.dev/icons?i=html,css,js,python)](https://skillicons.dev)

[![API](https://skillicons.dev/icons?i=django,postgres,redis)](https://skillicons.dev)

[![UI](https://skillicons.dev/icons?i=react,redux,vite,nextjs)](https://skillicons.dev)

[![DevOps](https://skillicons.dev/icons?i=docker,github)](https://skillicons.dev)

---

## 3. Projects (Repositories)
> Each project has an API (backend) and a UI (frontend), read the [Wiki](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki).

### 1. Identity (Authentication)

Identity is a modern authentication system built with Django/DRF and React. It secures applications with JWT, while supporting refresh token blacklisting for added safety. Roles and groups provide structured access, and recovery keys ensure account reliability. With clear documentation and an API-first approach, Identity is designed to integrate seamlessly into other projects, serving as the ecosystem’s foundation for trust and security.

- [API](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/Identity)
- [UI](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/Identity-UI)

### 2. HarborFlow

HarborFlow is a logistics and operations management system designed for shipping lines. It streamlines daily workflows, from container tracking to scheduling and operator coordination. By combining domain expertise with practical development, HarborFlow simplifies complex processes while ensuring accuracy and reliability. Built on a scalable Django and React stack, it offers shipping companies a clear, modern tool to manage operations effectively in a demanding industry.

- [API](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/HarborFlow)
- [UI](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/HarborFlow-UI)

### 3. Chat

Chat is a real-time messaging application that integrates directly with Identity to extend the ecosystem. It provides secure communication between users, with instant updates powered by WebSockets. Designed to support both private and group conversations, it emphasizes reliability and performance. With clean UI and robust backend, Chat enhances collaboration and connects seamlessly with other applications, building a unified experience across the entire development ecosystem.

- [API](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/Chat)
- [UI](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/Chat-UI)

### 4. ECom

ECom is a production-ready e-commerce platform that manages products, carts, checkout, and payments with efficiency. Built on Django/DRF for backend reliability and React for user experience, it provides a complete shopping system from inventory to orders. Payment gateways and order tracking create a polished experience for users, while a modular design makes it adaptable for growth, integrations, and real business needs.

- [API](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/ECom)
- [UI](https://github.com/rhman-ibrahim/rhman-ibrahim/wiki/ECom-UI)
  
---

## 4. Project (Tasks)

This project [board](https://github.com/users/rhman-ibrahim/projects/8) tracks the progress of all my repositories in a single place. It helps me stay consistent, break down large goals into manageable steps, and maintain a clear view of what’s ahead. The board is organized into energetic, action-oriented stages, reflecting how tasks move from ideas to completion. Each card represents a specific, testable step in building my ecosystem of applications.

### Columns

1. ***Backlog***: A pool of ideas and unprioritized tasks waiting for future consideration.
2. ***Do***: Tasks that are selected from the backlog and ready to be started next.
3. ***Doing***: Tasks currently in progress and actively being worked on.
4. ***Testing***: Tasks that are finished but undergoing review or validation.
5. ***Done***: Tasks successfully completed and confirmed as finished.
6. ***Archived***: Tasks that are either outdated or stored away for reference.

### Working Rules

> Tasks must be clear, actionable, and testable before moving into “Do.”

1. A task moves to ***Doing*** only when it is actively being worked on.
2. Once complete, tasks enter ***Testing*** to confirm correctness, stability, and integration.
3. After successful testing, tasks move to ***Done*** and may later be ***Archived*** for record-keeping.
4. New tasks are added to the ***Backlog*** first, then promoted when ready.
5. New tasks are added to the ***Backlog*** in batches of 4 at a time; when 4 tasks are completed, the next 4 are planned and added.
6. To stay focused and avoid overload, column limits are enforced: **Backlog (16 tasks)**, **Do (8 tasks)**, **Doing (4 tasks)** and **Testing (2 tasks)**.

### Task Properties

1. ***Project***: identifies which of the five main applications the task belongs to (Identity, HarborFlow, Chat, ECom, Portal).
2. ***End Date***: deadline for completing the task.
3. ***Priority***: urgency of the task: **C** (Critical), **H** (High), **V** (Valuable/Medium) and **N** (Nice-to-have).
4. ***Status***: the current Kanban column (Backlog → Do → Doing → Testing → Done → Archived).
5. ***Size***: effort measured in 40-minute units: **XS** ≤ 1 unit (40 mins), **S** takes 1 to 2 units (40–80 mins), **M** takes 2 to 4 units (80–160 mins) and **L** > 4 units (160+ mins).
6. ***Sub-Issues Progress***: tracks how many smaller sub-tasks within the main issue are completed, shown as a fraction or progress bar (e.g., 2/5 done).
