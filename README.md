## Table: Appointment_Statuses
| Column Name | Format  | Size | Key | Description |
|------------|--------|------|-----|-------------|
| status     | VARCHAR| 10   | PK  | Possible appointment statuses |

---

## Table: Appointments
| Column Name        | Format   | Size  | Key | Description |
|-------------------|----------|-------|-----|-------------|
| appointmentID     | INT      | —     | PK  | Unique appointment ID |
| appointmentDate   | DATETIME | —     |     | Actual appointment date |
| scheduledDate     | DATETIME | —     |     | Scheduled date |
| concern           | VARCHAR  | 100   |     | Reason for visit |
| appointmentStatus | VARCHAR  | 10    | FK  | References Appointment_Statuses |
| patientID         | VARCHAR  | 6     | FK  | References Patients |

---

## Table: Billing
| Column Name        | Format   | Size  | Key | Description |
|-------------------|----------|-------|-----|-------------|
| billingID         | INT      | —     | PK  | Unique billing record |
| amountOutstanding | DECIMAL  | 10,2  |     | Amount owed |
| date              | DATETIME | —     |     | Billing date |
| claimID           | INT      | —     | FK  | References Insurance_Claims |
| encounterID       | INT      | —     | FK  | References Medical_Encounters |
| amountPaid        | DECIMAL  | 10,2  |     | Amount paid |

---

