# API Design – Volunteer Organization Dashboard

This document defines the REST API endpoints for the backend service.
All endpoints return JSON and use JWT-based authentication unless otherwise stated.

Base URL (development):
/api

---

## Authentication

### POST /auth/register
Register a new user.

**Request**
```json
{
  "email": "user@example.com",
  "password": "password123",
  "fullName": "Jane Doe"
}

**Response**
```json
{
  "token": "jwt_token_here"
}

### POST /auth/register
Authenticate an existing user.

**Request**
```json
{
  "email": "user@example.com",
  "password": "password123"
}

**Response**
```json
{
  "token": "jwt_token_here"
}

## Organization

### POST /organizations
Create a new organizations.

Access: Authenticated user
Role: User becomes Admin of organization

**Request**
```json
{
  "name": "Helping Hands",
  "description": "Community volunteer organization"
}

### GET /organizations/:id
Get organization details.

Access: Organization members details.

### POST /organizations/:id/members
Add a user to an organization.

Access: Admin only

**Request**
```json
{
  "email": "volunteer@example.com",
  "role": "volunteer"
}

### GET /organizations/:id/members
List all members of an organization.

Access: Admin, Coordinator

## Events

### POST /organizations/:id/events
Create a new event.

Access: Admin, Coordinator

**Request**
```json
{
  "title": "Food Drive",
  "description": "Help distribute food",
  "eventDate": "2025-07-15T10:00:00Z",
  "capacity": 20
}

### GET /organizations/:id/events
List all events for an organization.

Access: Organization members

### PUT /organizations/:id
Update an event.

Access: Admin, Coordinator

### DELETE /events/:id
Delete an event.

Access: Admin

### POST /events/:id/signup
Sign the authenticated user up for an event.

Access: Volunteer

### DELETE /events/:id/signup
Cancel signup for an event.

Access: Volunteer (self only)

## Dashboard

### GET /organizations/:id/dashboard

Retrieve dashboard metrics for an organization.

Access: Admin, Coordinator

**Response**
```json
{
  "totalVolunteers": 42,
  "upcomingEvents": 5,
  "totalHoursLogged": 320
}















