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


---

## Entity Relationships

- A **User** can belong to multiple **Organizations**
- An **Organization** can have many **Users**
- The relationship between Users and Organizations is managed through **OrganizationMembers**

- An **Organization** can create multiple **Events**
- An **Event** belongs to exactly one **Organization**

- A **User** can sign up for multiple **Events**
- An **Event** can have multiple **Users**
- The relationship between Users and Events is managed through **EventSignups**

---

## Roles & Permissions

### Admin
- Manage organization details
- Add/remove members
- Assign roles
- Create, update, and delete events
- View all event signups and metrics

### Coordinator
- Create and manage events
- View volunteer signups
- Cannot manage organization members

### Volunteer
- View available events
- Sign up for or cancel event participation
- View personal participation history

