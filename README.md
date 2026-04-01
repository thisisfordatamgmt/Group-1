## Table: Appointment_Statuses
| Column Name | Data Type   | Size | Format        | Key  | Description |
|------------|------------|------|--------------|------|-------------|
| status     | VARCHAR    | 10   | Text         | PK   | Possible appointment statuses |

---

## Table: Appointments
| Column Name        | Data Type | Size | Format        | Key | Description |
|-------------------|----------|------|--------------|-----|-------------|
| appointmentDate   | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Actual appointment date |
| appointmentID     | INT      | —    | Integer      | PK  | Unique appointment ID |
| appointmentStatus | VARCHAR  | 10   | Text         | FK  | References Appointment_Statuses |
| concern           | VARCHAR  | 100  | Text         | —   | Reason for visit |
| patientID         | VARCHAR  | 6    | Text         | FK  | References Patients |
| scheduledDate     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Scheduled date |

---

## Table: Billing
| Column Name        | Data Type      | Size | Format        | Key | Description |
|-------------------|---------------|------|--------------|-----|-------------|
| amountOutstanding | DECIMAL       | 10,2 | Numeric      | —   | Amount owed |
| amountPaid        | DECIMAL       | 10,2 | Numeric      | —   | Amount paid |
| billingID         | INT           | —    | Integer      | PK  | Unique billing record |
| claimID           | INT           | —    | Integer      | FK  | References Insurance_Claims |
| date              | DATETIME      | —    | YYYY-MM-DD HH:MM:SS | —   | Billing date |
| encounterID       | INT           | —    | Integer      | FK  | References Medical_Encounters |

---

## Table: Encounter_Statuses
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| status     | VARCHAR  | 10   | Text   | PK  | Possible encounter statuses |

---

## Table: Insurance_Claims
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| claimID    | INT      | —    | Integer | PK | Unique claim ID |
| notes      | VARCHAR  | 300  | Text    | —  | Claim notes |
| providerID | INT      | —    | Integer | FK | References Insurance_Providers |

---

## Table: Insurance_Providers
| Column Name     | Data Type | Size | Format | Key | Description |
|----------------|----------|------|--------|-----|-------------|
| providerContact| VARCHAR  | 45   | Text   | —   | Contact info |
| providerID     | INT      | —    | Integer| PK  | Unique provider ID |
| providerNotes  | VARCHAR  | 45   | Text   | —   | Additional notes |

---

## Table: Medical_Encounters
| Column Name      | Data Type | Size | Format | Key | Description |
|-----------------|----------|------|--------|-----|-------------|
| appointmentID   | INT      | —    | Integer | FK | Linked appointment |
| date            | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Encounter date |
| encounterID     | INT      | —    | Integer | PK | Unique encounter ID |
| encounterNotes  | VARCHAR  | 1000 | Text    | —  | Notes for encounter |
| encounterStatus | VARCHAR  | 10   | Text    | FK | References Encounter_Statuses |
| physicianID     | VARCHAR  | 6    | Text    | FK | References Physicians |

---

## Table: Medical_History
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| dateAdded    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date record created |
| dateModified | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Last update date |
| historyID    | INT      | —    | Integer | PK | Unique history record |
| notes        | VARCHAR  | 1000 | Text    | —  | Medical notes |
| patientID    | VARCHAR  | 6    | Text    | FK | References Patients |

---

## Table: Medications
| Column Name    | Data Type | Size | Format | Key | Description |
|---------------|----------|------|--------|-----|-------------|
| genericName   | VARCHAR  | 45   | Text   | —   | Generic name |
| medicationID  | INT      | —    | Integer| PK  | Unique medication ID |
| medicationName| VARCHAR  | 45   | Text   | —   | Brand name |

---

## Table: Patients
| Column Name     | Data Type | Size | Format | Key | Description |
|----------------|----------|------|--------|-----|-------------|
| dateAdded      | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date patient added |
| patientAddress | VARCHAR  | 70   | Text   | —   | Patient address |
| patientDOB     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date of birth |
| patientEmail   | VARCHAR  | 45   | Text   | —   | Email |
| patientID      | VARCHAR  | 6    | Text   | PK  | Unique patient ID |
| patientName    | VARCHAR  | 45   | Text   | —   | Full name |
| patientPhone   | VARCHAR  | 15   | Text   | —   | Phone number |

---

## Table: Physician_Has_Specialty
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| dateAdded  | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date relationship added |
| physicianID| VARCHAR  | 6    | Text   | FK  | References Physicians |
| specialtyID| INT      | —    | Integer| FK  | References Specialty |

---

## Table: Physicians
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| physicianID  | VARCHAR  | 6    | Text   | PK  | Unique physician ID |
| physicianName| VARCHAR  | 45   | Text   | —   | Physician name |
| startDate    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Employment start |

---

## Table: Prescriptions
| Column Name          | Data Type     | Size  | Format | Key | Description |
|---------------------|--------------|-------|--------|-----|-------------|
| dosageAmount        | DECIMAL      | 10,3  | Numeric | —  | Dosage amount |
| dosageUnits         | VARCHAR      | 20    | Text    | —  | Units |
| encounterPrescribed | INT          | —     | Integer | FK | Encounter ID |
| medicationID        | INT          | —     | Integer | FK | References Medications |
| patientID           | VARCHAR      | 6     | Text    | FK | References Patients |
| datePrescribed      | VARCHAR      | 45    | Text    | —  | Date prescribed |

---

## Table: Specialty
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| specialtyID  | INT      | —    | Integer| PK  | Unique specialty ID |
| specialtyName| VARCHAR  | 45   | Text   | —   | Name of specialty |

