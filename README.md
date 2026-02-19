1.attendance.js
Will manage attendance-related operations such as:
Recording attendance
Fetching student attendance
Attendance reports
2.marks.js
Will handle marks and academic data including:
Uploading marks
Retrieving marks
Performance analysis
Database Connection
3.db.js 
This file manages the database connection for the backend.
Purpose:
Establish connection to database
Reusable across modules
Centralized DB configuration
Why placed here?
The Admin module is data-heavy, and most database operations
(mainly uploads, updates, and retrievals) depend on a stable DB connection.
Keeping DB logic centralized improves:
Code maintainability
Reusability
Debugging
Scalability
