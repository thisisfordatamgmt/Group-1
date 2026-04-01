## Table: Appointment_Statuses
| Column Name | Data Type    | Description |
|------------|-------------|-------------|
| status     | VARCHAR(10) | Possible appointment statuses |

--- 

## Table: Appointments
| Column Name      | Data Type     | Description |
|-----------------|--------------|-------------|
| appointmentID   | INT          | Unique appointment ID |
| appointmentDate | DATETIME     | Actual appointment date |
| scheduledDate   | DATETIME     | Scheduled date |
| concern         | VARCHAR(100) | Reason for visit |
| appointmentStatus | VARCHAR(10)| Status of appointment |
| patientID       | VARCHAR(6)   | References Patients |

--- 

## Table: Billing
| Column Name        | Data Type      | Description |
|-------------------|---------------|-------------|
| billingID         | INT           | Unique billing record |
| amountOutstanding | DECIMAL(10,2) | Amount owed |
| date              | DATETIME      | Billing date |
| claimID           | INT           | Linked insurance claim |
| encounterID       | INT           | Linked encounter |
| amountPaid        | DECIMAL(10,2) | Amount paid |

---

