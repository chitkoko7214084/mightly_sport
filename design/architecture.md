```mermaid

graph TD

    subgraph "Frontend (Vue.js Application)"
        A1[Team Register Form]
        A2[Player Register Form]
        A3[Directory Viewer]
        A4[Rules Page]
        A5[Admin Panel]
    end

    subgraph "Firebase Backend"
        subgraph "Authentication and Authorization"
            B1[Firebase Authentication]
        end
        subgraph "Database"
            B2[Firestore Database]
        end
        subgraph "File Storage"
            B3[Cloud Storage - Headshots and IDs]
        end
        subgraph "Serverless Functions"
            B4[Cloud Functions - Emails and Roster Lock]
        end
    end

    subgraph "External Services"
        C1[SendGrid Email Service]
        C2[Google Sheets Backup and Export]
    end

    %% Data Flows
    A1 -- "Coach submits Team" --> B2
    A2 -- "Player submits Registration" --> B2
    A2 -- "Uploads Headshot and ID" --> B3
    A3 -- "Reads Verified Players" --> B2
    A4 -- "Views Rules" --> A4
    A5 -- "Verify or Reject Players" --> B2
    A5 -- "Trigger Email" --> B4

    %% Backend Logic
    B2 -- "Verified Player Data" --> A3
    B4 -- "Send Micro Emails" --> C1
    B4 -- "Roster Export" --> C2
    B3 -- "File Reference" --> B2
    B1 -- "Auth Check" --> A5
