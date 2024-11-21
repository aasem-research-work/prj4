# Detailed Design Document

## Project Title
Development of Web and Mobile App for Legal Practice Management

## Overview
This document provides a detailed design for the development of a web and mobile application to assist lawyers in managing their practice. It includes UML and ER diagrams, as well as detailed specifications for the user interface. The aim is to clarify the developers' understanding and their parts so they can write code effectively.

## Table of Contents
1. System Architecture
2. UML Diagrams
   - Use Case Diagram
   - Class Diagram
   - Sequence Diagrams
3. ER Diagram
4. User Interface Specifications
   - Web Application
   - Mobile Application
5. Component Design
6. Approval and Next Steps

## System Architecture
### Frontend
- **Web Application**: React.js
- **Mobile Application**: React Native

### Backend
- **Server**: Node.js with Express.js framework
- **Database**: SQLite database (only for release 1)

### Security
- **Encryption**: SSL/TLS for data in transit, AES-256 for data at rest
- **Authentication**: OAuth 2.0, JWT (JSON Web Tokens) for session management

## UML Diagrams
### Use Case Diagram
```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffcc00', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#ffcc00'}}}%%
graph TD
    A[Lawyer] -->|Manages| B[Client Management]
    A -->|Handles| C[Case Management]
    A -->|Tracks| D[Financial Management]
    A -->|Schedules| E[Time Management]
    B -->|Stores| F[Client Details]
    B -->|Tracks| G[Client Interactions]
    C -->|Records| H[Case Details]
    C -->|Schedules| I[Court Dates]
    C -->|Organizes| J[Documents]
    D -->|Records| K[Payments]
    D -->|Generates| L[Invoices]
    D -->|Monitors| M[Outstanding Balances]
    E -->|Tracks| N[Billable Hours]
    E -->|Schedules| O[Appointments]
    E -->|Sets| P[Reminders]
```

### Class Diagram
```mermaid
classDiagram
    class Client {
        +int client_id
        +string name
        +string contact_info
        +string case_history
    }

    class Case {
        +int case_id
        +int client_id
        +string status
        +string details
        +string key_dates
    }

    class Appointment {
        +int appointment_id
        +int case_id
        +string date
        +string description
    }

    class Payment {
        +int payment_id
        +int client_id
        +float amount
        +string date
        +string status
    }

    class Timesheet {
        +int timesheet_id
        +int user_id
        +float hours
        +string date
        +string description
    }

    Client "1" --> "0..*" Case : has
    Case "1" --> "0..*" Appointment : includes
    Client "1" --> "0..*" Payment : makes
    Case "1" --> "0..*" Payment : involves
    Timesheet "1" --> "0..*" Client : records
```

### Sequence Diagrams
#### Client Management
```mermaid
sequenceDiagram
    participant Lawyer
    participant ClientSystem as Client Management System
    participant Database

    Lawyer->>ClientSystem: Add new client details
    ClientSystem->>Database: Insert client details
    Database-->>ClientSystem: Confirmation
    ClientSystem-->>Lawyer: Client added successfully

    Lawyer->>ClientSystem: Update client details
    ClientSystem->>Database: Update client record
    Database-->>ClientSystem: Confirmation
    ClientSystem-->>Lawyer: Client details updated

    Lawyer->>ClientSystem: View client details
    ClientSystem->>Database: Fetch client details
    Database-->>ClientSystem: Client details
    ClientSystem-->>Lawyer: Display client details
```

#### Case Management
```mermaid
sequenceDiagram
    participant Lawyer
    participant CaseSystem as Case Management System
    participant Database

    Lawyer->>CaseSystem: Add new case details
    CaseSystem->>Database: Insert case details
    Database-->>CaseSystem: Confirmation
    CaseSystem-->>Lawyer: Case added successfully

    Lawyer->>CaseSystem: Update case details
    CaseSystem->>Database: Update case record
    Database-->>CaseSystem: Confirmation
    CaseSystem-->>Lawyer: Case details updated

    Lawyer->>CaseSystem: View case details
    CaseSystem->>Database: Fetch case details
    Database-->>CaseSystem: Case details
    CaseSystem-->>Lawyer: Display case details
```

## ER Diagram
```mermaid
erDiagram
    CLIENTS {
        int client_id PK
        string name
        string contact_info
        string case_history
    }
    CASES {
        int case_id PK
        int client_id FK
        string status
        string details
        string key_dates
    }
    APPOINTMENTS {
        int appointment_id PK
        int case_id FK
        string date
        string description
    }
    PAYMENTS {
        int payment_id PK
        int client_id FK
        float amount
        string date
        string status
    }
    TIMESHEETS {
        int timesheet_id PK
        int user_id
        float hours
        string date
        string description
    }

    CLIENTS ||--o{ CASES : "has"
    CASES ||--o{ APPOINTMENTS : "includes"
    CLIENTS ||--o{ PAYMENTS : "makes"
    CASES ||--o{ PAYMENTS : "involves"
    TIMESHEETS ||--o{ CLIENTS : "records"
```

## User Interface Specifications
### Web Application
#### Dashboard
- **Description**: Overview of key metrics and recent activities.
- **Components**: Charts, recent activities list, notifications.

#### Client Management
- **Description**: Interface to add, edit, and view client details.
- **Components**: Client list, client detail form, search bar.

#### Case Management
- **Description**: Interface to manage case details and documents.
- **Components**: Case list, case detail form, document upload.

#### Financial Management
- **Description**: Interface to track payments and generate invoices.
- **Components**: Payment list, invoice generation form, payment status.

#### Time Management
- **Description**: Interface to track billable hours and manage appointments.
- **Components**: Timesheet, appointment scheduler, reminders.

### Mobile Application
#### Dashboard
- **Description**: Overview of key metrics and recent activities.
- **Components**: Charts, recent activities list, notifications.

#### Client Management
- **Description**: Mobile-friendly interface to manage client details.
- **Components**: Client list, client detail form, search bar.

#### Case Management
- **Description**: Mobile-friendly interface to manage case details.
- **Components**: Case list, case detail form, document upload.

#### Financial Management
- **Description**: Mobile-friendly interface to track payments.
- **Components**: Payment list, invoice generation form, payment status.

#### Time Management
- **Description**: Mobile-friendly interface to track billable hours.
- **Components**: Timesheet, appointment scheduler, reminders.

## Component Design
### Frontend Components
- **Header**: Navigation bar with links to different sections.
- **Footer**: Footer with contact information and links.
- **Sidebar**: Sidebar for quick navigation.
- **Forms**: Reusable form components for client, case, and payment details.

### Backend Components
- **API Endpoints**: RESTful API endpoints for client, case, appointment, and payment management.
- **Database Models**: Models for Clients, Cases, Appointments, Payments, and Timesheets.
- **Authentication**: OAuth 2.0 and JWT for secure authentication and authorization.

## Next Steps
- Kickoff current sprent development
- Update the document with next version for future sprent

---

**Prepared by:**
[Development Team Lead's Name]  
[Development Team's Contact Information]

**Date:**
[Current Date]
