# Data Model – Volunteer Organization Dashboard

This document defines the core database entities for the backend system.
The goal is to support multiple volunteer organizations with role-based access
and event participation tracking.

---

## Users
Represents all users of the system.

| Field | Type | Notes |
|------|----|------|
| id | UUID | Primary key |
| email | string | Unique |
| password_hash | string | Hashed password |
| full_name | string |  |
| created_at | timestamp |  |

---

## Organizations
Represents volunteer organizations using the platform.

| Field | Type | Notes |
|------|----|------|
| id | UUID | Primary key |
| name | string |  |
| description | text |  |
| created_at | timestamp |  |

---

## OrganizationMembers
Join table linking users to organizations with roles.

| Field | Type | Notes |
|------|----|------|
| id | UUID | Primary key |
| user_id | UUID | FK → Users |
| organization_id | UUID | FK → Organizations |
| role | enum | admin, coordinator, volunteer |
| joined_at | timestamp |  |

---

## Events
Represents volunteer events created by organizations.

| Field | Type | Notes |
|------|----|------|
| id | UUID | Primary key |
| organization_id | UUID | FK → Organizations |
| title | string |  |
| description | text |  |
| event_date | timestamp |  |
| capacity | integer | Max volunteers |
| created_by | UUID | FK → Users |
| created_at | timestamp |  |

---

## EventSignups
Tracks volunteer participation in events.

| Field | Type | Notes |
|------|----|------|
| id | UUID | Primary key |
| event_id | UUID | FK → Events |
| user_id | UUID | FK → Users |
| status | enum | signed_up, canceled |
| hours_logged | decimal | Nullable |
| signed_up_at | timestamp |  |
