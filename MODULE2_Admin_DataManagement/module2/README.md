# MODULE 2 — Admin Data Management

## Purpose
Handles all data input, student records, and counsellor assignments.
This is the admin's primary workflow — uploading students and assigning counsellors.

## Files Included

### Backend
| File | Responsibility |
|------|---------------|
| `backend/controllers/studentController.js` | CSV upload, get students, unassigned list |
| `backend/controllers/assignmentController.js` | Assign, bulk assign, list assignments |
| `backend/routes/students.js` | `/api/students/*` route definitions |
| `backend/routes/assignments.js` | `/api/assignments/*` route definitions |

### Frontend
| File | Responsibility |
|------|---------------|
| `frontend/src/pages/UploadStudents.jsx` | CSV file picker + upload result display |
| `frontend/src/pages/AssignStudents.jsx` | Assign students to counsellors (bulk + individual) |
| `frontend/src/pages/ManageCounsellors.jsx` | Add counsellors, view counsellor list |
| `frontend/src/services/api.js` | Axios instance (shared) |

### Data
| File | Description |
|------|-------------|
| `sample_students.csv` | Ready-to-upload sample CSV with 15 students |

## API Endpoints
```
POST /api/students/upload          Upload CSV — bulk insert students
GET  /api/students                 Get all students (admin)
GET  /api/students/unassigned      Students not yet assigned to any counsellor
GET  /api/students/:id             Single student detail
POST /api/assignments              Assign one student to one counsellor
POST /api/assignments/bulk         Assign multiple students at once
GET  /api/assignments/all          All assignments for this institution
GET  /api/assignments/mine         Counsellor sees their own assigned students
```

## CSV Upload Rules
The uploaded CSV must have these exact column headers (first row):
```
Serial Number, Student Name, CGPA, Attendance, Email, Contact Number, Branch
```

Branch values accepted (case-insensitive):
- `CSE` or `Computer Science & Engineering`
- `ECE` or `Electronics & Communication`
- `MECH` or `Mechanical Engineering`
- `CIVIL` or `Civil Engineering`
- `IT` or `Information Technology`
- `AIDS` or `AI & Data Science`

CGPA must be between 0.0 and 10.0
Attendance must be between 0.0 and 100.0

## Key Logic
- CSV parser strips BOM, whitespace, carriage returns automatically
- Branch matched by code OR full name — flexible for any CSV format
- Each row is individually validated — errors reported row-by-row
- Failed rows don't block the rest of the batch from inserting
- Risk level is auto-assigned per student by riskService (Module 3)
