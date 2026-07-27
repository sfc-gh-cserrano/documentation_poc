---
icon: material/database
title: Docebo Learn Data
---
# :material-database: Docebo Learn Data
> ERD & Data Dictionary

> **Source**: Docebo Learn Data Export — February 2026  


## Database Statistics

| Metric | Count |
|--------|-------|
| Tables | 443 |
| Columns | 5,808 |
| Foreign Key Relationships | 291 |
| Domains | 50 |

## High-Level Domain Architecture

```mermaid
graph LR
    subgraph Identity["Identity & Access"]
        CORE[Core Platform<br/>62 tables]
        USER[User / Branches<br/>5 tables]
        RBAC[RBAC & Power Users<br/>6 tables]
    end

    subgraph LearningContent["Learning & Content"]
        LEARN[Learning<br/>107 tables]
        CONTENT[Content & Marketplace<br/>29 tables]
        COACH[Coach & Share<br/>37 tables]
    end

    subgraph Delivery["Training Delivery"]
        ILT[ILT & Webinars<br/>27 tables]
        CERT[Certifications & Transcripts<br/>12 tables]
        SKILLS[Skills & Gamification<br/>51 tables]
    end

    subgraph Enrollment["Enrollment & Analytics"]
        ENROLL[Enrollments & KPIs<br/>11 tables]
        DM[Data Mart<br/>12 tables]
        AUDIENCES[Audiences & Subscriptions<br/>25 tables]
    end

    subgraph Commerce["Commerce"]
        ECOM[E-Commerce & Payments<br/>22 tables]
    end

    subgraph Config["Platform Configuration"]
        PLATFORM[Pages, Policies, Mobile<br/>35 tables]
    end

    CORE -->|"idst (user PK)"| LEARN
    CORE -->|"idst"| COACH
    CORE -->|"idst"| ILT
    CORE -->|"idst"| SKILLS
    CORE -->|"idst"| ENROLL
    CORE -->|"idst"| CERT
    CORE -->|"idst"| ECOM
    CORE -->|"idst"| AUDIENCES
    LEARN -->|"course_id"| ILT
    LEARN -->|"course_id"| ENROLL
    LEARN -->|"course_id"| CERT
    LEARN -->|"lo_id"| COACH
    DM -.->|"analytical views"| LEARN
    DM -.->|"analytical views"| CERT
    DM -.->|"analytical views"| ILT
```

## Domain Index

| # | Domain Document | Domains Covered | Tables | Description |
|---|----------------|-----------------|--------|-------------|
| 1 | [Core Platform](core-platform.md) | Core Platform, User, Branches, Login, RBAC, Power Users, Manager Types | 72 | Users, groups, roles, org structure, notifications, settings |
| 2 | [Learning](learning.md) | Learning, LO Content, Equivalent Courses | 110 | Courses, learning paths, learning objects, tracking |
| 3 | [Enrollments](enrollments.md) | Archived Enrollments, Enrollment KPIs, Course KPIs, Group KPIs, LMS Sessions | 11 | Enrollment lifecycle, snapshots, and KPI metrics |
| 4 | [Certifications](certifications.md) | Certifications, Transcripts | 12 | Certification programs and external transcript records |
| 5 | [ILT Sessions](ilt-sessions.md) | ILT Sessions, Webinars, Attendance | 27 | Instructor-led training, virtual classrooms, attendance |
| 6 | [Coach & Share](coach-and-share.md) | Coach & Share | 37 | Social/informal learning: Q&A, channels, content sharing |
| 7 | [Skills](skills.md) | Skills, On-the-Job, Gamification | 51 | Competency mapping, observation checklists, badges/contests |
| 8 | [Content](content.md) | Content Curation, Content Marketing, Content Partners, Marketplace, LevelJump, OpenSesame | 29 | Third-party content, curation, campaigns, integrations |
| 9 | [Audiences](audiences.md) | Audiences, Communications, Subscriptions, Subscription Codes | 25 | User segmentation, messaging, subscription plans |
| 10 | [E-Commerce](ecommerce.md) | E-Commerce, Payments | 22 | Course purchases, coupons, wallets, payment gateways |
| 11 | [Data Mart](data-mart.md) | Data Mart | 12 | Pre-built analytical/reporting views (DM_* tables) |
| 12 | [Platform Config](platform-config.md) | Cookie Policy, T&C Policies, Terms & Conditions, Pages, Menu, Mobile App, Launchers, Player, Presets, Proctoring, PENS, Blacklist, Docebo | 35 | UI configuration, policies, mobile, proctoring |

## Central Entity: CORE_USER

The `CORE_USER` table (PK: `idst`) is the hub of the entire data model. Nearly all domains reference it via an `iduser` foreign key. When building analytics queries, joins to `CORE_USER` provide:

- User identity and profile fields
- Branch/group membership (via `CORE_GROUP_MEMBERS`)
- Role assignments (via `CORE_ROLE_MEMBERS`)
- Manager relationships (via `CORE_ORG_CHART_TREE`)

## Key Join Patterns

| From Domain | FK Column | To Table | To Column |
|-------------|-----------|----------|-----------|
| Learning | `iduser` | CORE_USER | `idst` |
| Coach & Share | `iduser` | CORE_USER | `idst` |
| ILT Sessions | `id_user` | CORE_USER | `idst` |
| Certifications | `id_user` | CORE_USER | `idst` |
| Skills | `iduser` | CORE_USER | `idst` |
| E-Commerce | `id_user` | CORE_USER | `idst` |
| Gamification | `id_user` | CORE_USER | `idst` |
| On-the-Job | `iduser` | CORE_USER | `idst` |
| Subscriptions | `iduser` | CORE_USER | `idst` |

---

*This documentation set was generated from the interactive ERD HTML artifact (February 2026).*
