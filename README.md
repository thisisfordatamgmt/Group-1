## Table: Appointments
| Column Name      | Data Type     | Description |
|-----------------|--------------|-------------|
| appointmentID   | INT          | Unique appointment ID |
| appointmentDate | DATETIME     | Actual appointment date |
| scheduledDate   | DATETIME     | Scheduled date |
| concern         | VARCHAR(100) | Reason for visit |
| appointmentStatus | VARCHAR(10)| Status of appointment |
| patientID       | VARCHAR(6)   | References Patients |
