## Table: Appointment_Statuses
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| status     | VARCHAR  | 10   | Text   | PK  | Possible appointment statuses |

---

## Table: Appointments
| Column Name        | Data Type | Size | Format | Key | Description |
|-------------------|----------|------|--------|-----|-------------|
| appointmentDate   | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Actual appointment date |
| appointmentID     | VARCHAR  | 6    | Text   | PK  | Unique appointment ID |
| appointmentStatus | VARCHAR  | 10   | Text   | FK  | References Appointment_Statuses |
| concern           | VARCHAR  | 100  | Text   | —   | Reason for visit |
| patientID         | VARCHAR  | 6    | Text   | FK  | References Patients |
| scheduledDate     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Scheduled date |

---

## Table: Billing
| Column Name        | Data Type | Size | Format | Key | Description |
|-------------------|----------|------|--------|-----|-------------|
| amountOutstanding | DECIMAL  | 10,2 | Numeric | —  | Amount owed |
| amountPaid        | DECIMAL  | 10,2 | Numeric | —  | Amount paid |
| billingID         | VARCHAR  | 6    | Text    | PK | Unique billing ID |
| claimID           | VARCHAR  | 6    | Text    | FK | References Insurance_Claims |
| date              | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Billing date |
| encounterID       | VARCHAR  | 6    | Text    | FK | References Medical_Encounters |

---

## Table: Encounter_Statuses
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| status     | VARCHAR  | 10   | Text   | PK  | Possible encounter statuses |

---

## Table: Insurance_Claims
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| claimID    | VARCHAR  | 6    | Text   | PK  | Unique claim ID |
| notes      | VARCHAR  | 300  | Text   | —   | Claim notes |
| providerID | VARCHAR  | 6    | Text   | FK  | References Insurance_Providers |

---

## Table: Insurance_Providers
| Column Name    | Data Type | Size | Format | Key | Description |
|---------------|----------|------|--------|-----|-------------|
| providerID    | VARCHAR  | 6    | Text   | PK  | Unique provider ID |
| providerName  | VARCHAR  | 45   | Text   | —   | Provider name |
| providerNotes | VARCHAR  | 45   | Text   | —   | Additional notes |

---

## Table: Medical_Encounters
| Column Name      | Data Type | Size | Format | Key | Description |
|-----------------|----------|------|--------|-----|-------------|
| appointmentID   | VARCHAR  | 6    | Text   | FK  | Linked appointment |
| date            | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Encounter date |
| encounterID     | VARCHAR  | 6    | Text   | PK  | Unique encounter ID |
| encounterNotes  | VARCHAR  | 1000 | Text   | —   | Notes |
| encounterStatus | VARCHAR  | 10   | Text   | FK  | References Encounter_Statuses |
| physicianID     | VARCHAR  | 6    | Text   | FK  | References Physicians |

---

## Table: Medical_History
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| dateAdded    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Record created |
| dateModified | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Last updated |
| historyID    | INT      | —    | Integer | PK | Unique history ID |
| notes        | VARCHAR  | 1000 | Text    | —  | Medical notes |
| patientID    | VARCHAR  | 6    | Text    | FK | References Patients |

---

## Table: Medications
| Column Name    | Data Type | Size | Format | Key | Description |
|---------------|----------|------|--------|-----|-------------|
| genericName   | VARCHAR  | 45   | Text   | —   | Generic name |
| medicationID  | VARCHAR  | 6    | Text   | PK  | Unique medication ID |
| medicationName| VARCHAR  | 45   | Text   | —   | Brand name |

---

## Table: Patients
| Column Name     | Data Type | Size | Format | Key | Description |
|----------------|----------|------|--------|-----|-------------|
| dateAdded      | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date added |
| patientAddress | VARCHAR  | 70   | Text   | —   | Address |
| patientDOB     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date of birth |
| patientEmail   | VARCHAR  | 45   | Text   | —   | Email |
| patientID      | VARCHAR  | 6    | Text   | PK  | Unique patient ID |
| patientName    | VARCHAR  | 45   | Text   | —   | Full name |
| patientPhone   | VARCHAR  | 15   | Text   | —   | Phone |

---

## Table: Physician_Has_Specialty
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| dateAdded  | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date added |
| physicianID| VARCHAR  | 6    | Text   | FK  | References Physicians |
| specialtyID| INT      | —    | Integer| FK  | References Specialty |

---

## Table: Physicians
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| physicianID  | VARCHAR  | 6    | Text   | PK  | Unique physician ID |
| physicianName| VARCHAR  | 45   | Text   | —   | Name |
| startDate    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Start date |

---

## Table: Prescriptions
| Column Name             | Data Type | Size | Format | Key | Description |
|------------------------|----------|------|--------|-----|-------------|
| datePrescribed         | VARCHAR  | 45   | Text   | —   | Date prescribed |
| dosageAmount           | DECIMAL  | 10,3 | Numeric | —  | Dosage |
| dosageUnits            | VARCHAR  | 20   | Text   | —   | Units |
| encounterPrescribedIn  | VARCHAR  | 6    | Text   | FK  | References Medical_Encounters |
| medicationID           | VARCHAR  | 6    | Text   | FK  | References Medications |
| patientID              | VARCHAR  | 6    | Text   | FK  | References Patients |

---

## Table: Specialty
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| specialtyID  | INT      | —    | Integer| PK  | Unique specialty ID |
| specialtyName| VARCHAR  | 45   | Text   | —   | Specialty name |

