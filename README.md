# Rhman

- Self-taught developer with a business background, focused on building systems around **automation, optimization, and customization**. I approach software as a tool to simplify operations and give full control over how things work.

- I build **websites, APIs, UIs and full-stack web applications**, with a focus on clarity, reliability, and long-term usability.

---

## Tools

- For websites, I use **Astro** and **Next.js** to deliver fast, structured, and SEO-friendly experiences.  

- For systems, I rely on **Django** for a stable, structured backend that supports clean and maintainable architecture and **React (JavaScript)** for building flexible and interactive user interfaces. This combination helps me move from idea to production in a predictable and scalable way.


### Web 256 The Ecosystem

I maintain a personal UI layer for layouts and forms, used consistently across all projects. It is built with **React, Redux, and GSAP**, and evolves continuously alongside new work. This ensures a consistent visual structure and interaction behavior across different applications.

Currently, these packages are hosted in private repositories and will be released publicly after the first release of [Auth+RBAC](#auth--rbac).

```sh
npm install @web256utilities/layout@latest
npm install @web256utilities/form@latest
```

> *Web256Utilities* is my private organization for managing shared utilities. Each category of projects is also separated into its own organization. To use the packages above, an access token must be configured in the .npmrc file.

|#|Organization|Description|
|--|--|--|
|1|[Web256Utilities](https://github.com/Web256Utilities)|Reusable code, helpers, mixins, and modules for frontend and backend, enabling consistent patterns and maintainable architecture.|
|2|[Web256Bridge](https://github.com/Web256Bridge)|Backend APIs and services built primarily with Python using Django, DRF, and Flask. Focused on reliable systems, integrations, and scalable application logic.|
|3|[Web256Portal](https://github.com/Web256Portal)|Frontend interfaces built with JavaScript & the React ecosystem. Focused on building UIs for existing APIs or delivering standalone single tier solutions.|
|4|[Web256Studio](https://github.com/Web256Studio)|Websites and web experiences built with modern frameworks. Focused on Next.js and Astro depending on the project's structure, performance needs, & goals.|
---

## Auth + RBAC

A foundational system for authentication and role-based access control, designed as an internal operations layer for teams, startups, and organizations. It remains simple at the surface while supporting structured and flexible authorization rules underneath.

- Stateless authentication using JWT  
- Access and refresh token lifecycle with blacklisting support  
- Role-based access control (RBAC) for defining permitted actions  
- Group-based organization of users without hierarchical complexity  
- Dynamically managed permissions per system needs  
- Secure recovery mechanism through generated keys  
- Full audit logging for system-level actions  
- Supports throttling

---

## Working On

### Clouding

Attending official training on Google Cloud Platform (GCP) and AWS (Amazon Web Services) to support automated deployments and improve understanding of infrastructure cost modeling.

### Discussions Layer

Extending the system with a lightweight discussions feature to support collaboration and context-based communication within *Auth + RBAC*.

- Unified abstraction layer to switch transport modes without modifying core logic
- Polling adapter for simple and reliable update flows
- WebSocket adapter for real-time interaction where required

---

## Next

Building a **RAG (Retrieval-Augmented Generation) system** to enable querying across structured and unstructured data sources, making internal knowledge accessible through natural interaction.
