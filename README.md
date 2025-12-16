## volunteer-dashboard

## Project Overview
This project is a backend REST API for a volunteer organization dashboard.  
It allows nonprofit organizations to manage volunteers, events, and participation while providing role-based access control for different user types.

The frontend UI is being designed by a graphic designer collaborator, while this repository focuses on backend architecture, APIs, and business logic.

## Target Users
- Volunteer organizations / nonprofits
- Organization administrators
- Event coordinators
- Volunteers

## Tech Stack
- Node.js
- Express.js
- PostgreSQL
- JWT Authentication
- bcrypt (password hashing)

## Roles & Permissions
- **Admin**
  - Manage organization details
  - Manage members and roles
  - Create and manage events
- **Coordinator**
  - Create and manage events
  - View volunteer signups
- **Volunteer**
  - View events
  - Sign up for or cancel participation

## Planned Features

### MVP
- User authentication (register/login)
- Role-based access control
- Organization creation and membership
- Event creation and management
- Volunteer signup and tracking
- Basic dashboard metrics

### Stretch Goals
- Volunteer hour tracking
- Event capacity limits and waitlists
- Search and filtering
- CSV export for reports
- Notifications (email or in-app)

## Project Status
Planning & system design phase
