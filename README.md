# Smart University Data Engineering Platform

## Overview
The **Smart University Data Engineering Platform** is a data-driven university application integrating practical student, faculty, and campus services into one platform. It demonstrates how university data can be collected, processed, stored, and converted into useful services.

## Project Features

### Student Services
1. **Face Recognition Attendance** — Verifies registered students and records attendance with date/time while preventing duplicate marking.
2. **Internal Marks Notification** — Faculty publish internal marks; students view them and receive notifications.
3. **Free Classroom Finder** — Uses timetable and room data to find available classrooms/labs for a selected day and hour.

### Faculty Services
4. **Automated Question Paper Generator** — Processes selected handouts/PPTs, uses a sample paper as the format reference, and generates structured question-paper sets with preview/PDF output.
5. **Instant Classroom/Lab Replacement** — Checks timetable, room availability, capacity, and requirements to assign a suitable replacement room.

### Campus Services
6. **Smart Bus Tracking & Alternative Bus** — Displays route, stop, timing, location/status and ETA information, with alternative suggestions when delays occur. Simulated data is clearly identified when live GPS is unavailable.
7. **Canteen Digital Token & Live Queue** — Generates orders, tokens and receipts and manages `Ordered → Waiting → Processing → Ready → Collected`.

## Data Engineering Approach

The project applies data-engineering concepts to practical university services.

```text
Data Sources
    ↓
Data Ingestion
    ↓
Data Cleaning & Validation
    ↓
Data Transformation / Processing
    ↓
Data Storage
    ↓
Backend APIs
    ↓
University Services
    ↓
User Output
```

### Main Data Sources
- Student records and face reference data
- Marks and academic subjects
- Handouts, PPTs and sample question papers
- Timetables and classroom/lab information
- Bus routes and stops
- Canteen menu and orders

## Technology Architecture

- **Python + Pandas** — structured data generation and ingestion
- **Apache Kafka** — scalable streaming ingestion for real-time events
- **Apache Spark** — scalable large-data processing
- **PostgreSQL + MinIO** — structured and raw/processed data storage
- **FastAPI** — backend APIs and service layer
- **React.js** — frontend interfaces
- **Python + AI Models** — face recognition and document/question-paper processing
- **VS Code** — development
- **Git/GitHub** — version control and collaboration

> Kafka and Spark are included in the scalable data-engineering architecture. The current prototype uses limited/reference datasets; do not claim university-scale Kafka/Spark processing unless those components have actually been deployed.

## User Roles

### Student
Students can use attendance, marks, classroom, bus, and canteen workflows.

### Faculty
Faculty can publish marks, generate question papers, and request classroom/lab replacements.

### Canteen Operator
The operator can view orders, update queue states, and manage ready/collected tokens.

## Reference Data

Reference material is kept separately from transaction data:

```text
data/
└── reference/
    ├── face_data/
    ├── handouts/
    ├── ppts/
    ├── question papers/
    ├── timetables/
    ├── bus routes/
    └── canteen/
```

Reference files should power the relevant features without unnecessarily exposing raw files to users.

## Fresh System State

The application should start as a fresh/unused system. Master/reference data may exist, such as students, subjects, rooms, timetables, bus routes and menu items. Transaction data should be created through actual user actions.

Examples of empty states:
- `No marks have been published yet.`
- `No active canteen orders.`
- `No attendance recorded for this session.`

Avoid fake historical transactions or fabricated dashboard statistics.

## Question Paper Workflow

```text
Select Subject
      ↓
Select Exam
      ↓
Select Handouts/PPTs
      ↓
Select Sample Paper / Format
      ↓
Select Number of Sets
      ↓
Generate
      ↓
Preview / Edit / Regenerate
      ↓
Download PDF
```

Handouts/PPTs are the primary academic sources; sample papers provide the required structure/format.

## Canteen Workflow

```text
Ordered → Waiting → Processing → Ready → Collected
```

The token, receipt, student status, operator queue, and canteen display should reflect the current order state.

## Bus Tracking

The bus module must distinguish between **live data** and **simulated/sample data**. Simulated data must never be presented as real-time GPS.

## Notifications

Email/in-app notifications can be used for attendance, internal marks publication, and configured alerts. Credentials and API keys must be stored in environment variables and never committed to GitHub.

## Environment Variables

Use a `.env` file for secrets, for example:

```text
DATABASE_URL=
EMAIL_HOST=
EMAIL_PORT=
EMAIL_USERNAME=
EMAIL_PASSWORD=
EMAIL_FROM=
AI_API_KEY=
```

Use only the variables required by the implementation and add `.env` to `.gitignore`.

## Testing

Test complete workflows, including:
- Input validation and error handling
- Data processing and database updates
- API responses and UI behaviour
- Notifications and state changes
- Duplicate prevention
- Empty states
- PDF and receipt generation

### Important Tests
**Attendance:** registered students, unknown faces, separate student identities, duplicate prevention.  
**Question Paper:** different materials, required structure, multiple sets, PDF generation.  
**Classroom Finder:** different days/hours and occupied-room exclusion.  
**Room Replacement:** unavailable room and suitable replacement conditions.  
**Canteen:** token creation, all queue states, Ready notification, receipt generation.

## Development Principles

- Keep student, faculty, and campus workflows modular.
- Keep reference data separate from transaction data.
- Validate data before processing.
- Keep database state synchronized with UI state.
- Do not expose sensitive face-reference images unnecessarily.
- Do not hard-code credentials or API keys.
- Use meaningful empty/error states.
- Do not present simulated data as live data.
- Test complete workflows rather than only individual screens.

## Expected Outcome

The project aims to provide an integrated university platform connecting practical student, faculty, and campus services through data-driven processing.

The system produces operational outputs such as attendance records, marks notifications, available/replacement rooms, generated question papers, bus alternatives, and canteen tokens.

## Team

**Batch No.: 6**

- **N Sai Suhaas** — 2420030734
- **A Sudarsan Krishna** — 2420030641
- **A Dhanush** — 2420030639

**Faculty:** Dr. N Sirisha

## Project
**Smart University Data Engineering Platform**
