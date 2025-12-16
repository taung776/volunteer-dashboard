# API Design – Volunteer Organization Dashboard

This document defines the REST API endpoints for the backend service.
All endpoints return JSON and use JWT-based authentication unless otherwise stated.

Base URL (development):
/api

---

## Authentication

### POST /auth/register
Register a new user.

Request:
{
  "email": "user@example.com",
  "password": "password123",
  "fullName": "Jane Doe"
}

Response:
{
  "token": "jwt_token_here"
}

---

### POST /auth/login
Authenticate an existing user.

Request:
{
  "email": "user@example.com",
  "password": "password123"
}

Response:
{
  "token": "jwt_token_here"
}

---

## Organizations

### POST /organizations
Create a new organization.

Access:
- Authenticated user
- Creator becomes Admin of the organization

Request:
{
  "name": "Helping Hands",
  "description": "Community volunteer organization"
}

---

### GET /organizations
Get organization list.

Public (read-only)

---

### GET /organizations/:id
Get organization details.

Public (read-only)

---


### GET /organizations/:id/events
List all events for an organization.

Public (read-only)

---

## Organization Members

### POST /organizations/:id/members
Add a user to an organization.

Access:
- Admin only

Request:
{
  "email": "volunteer@example.com",
  "role": "volunteer"
}

---

### GET /organizations/:id/members
List all members of an organization.

Access:
- Admin
- Coordinator

---

## Events

### POST /organizations/:id/events
Create a new event.

Access:
- Admin
- Coordinator

Request:
{
  "title": "Food Drive",
  "description": "Help distribute food",
  "eventDate": "2025-07-15T10:00:00Z",
  "capacity": 20
}

---

### GET /events
List all events.

Public (read-only)

---

### GET /events/:id
Get an event information.

Public (read-only)

---

### PUT /events/:id
Update an event.

Access:
- Admin
- Coordinator

---

### DELETE /events/:id
Delete an event.

Access:
- Admin only

---

## Event Signups

### POST /events/:id/signup
Sign the authenticated user up for an event.

Access:
- Volunteer

---

### DELETE /events/:id/signup
Cancel signup for an event.

Access:
- Volunteer (self only)

---

## Dashboard

### GET /organizations/:id/dashboard
Retrieve dashboard metrics for an organization.

Access:
- Admin
- Coordinator

Response:
{
  "totalVolunteers": 42,
  "upcomingEvents": 5,
  "totalHoursLogged": 320
}

---

## Authorization Rules Summary

- Users must belong to an organization to access its resources
- Admins have full access within their organization
- Coordinators can manage events but not organization members
- Volunteers can only manage their own event participation
