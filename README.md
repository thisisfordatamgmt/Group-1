## Table: Appointment_Statuses
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| status     | VARCHAR  | 10   |    | PK  | Possible appointment statuses |

---

## Table: Appointments
| Column Name        | Data Type | Size | Format | Key | Description |
|-------------------|----------|------|--------|-----|-------------|
| appointmentID     | VARCHAR  | 6    | APXXXX | PK  | Unique appointment ID |
| appointmentDate   | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Actual appointment date |
| scheduledDate     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | —   | Scheduled date |
| concern           | VARCHAR  | 100  |        | —   | Reason for visit |
| appointmentStatus | VARCHAR  | 10   |        | FK  | References Appointment_Statuses |
| patientID         | VARCHAR  | 6    | PAXXXX | FK  | References Patients |

---

## Table: Billing
| Column Name        | Data Type | Size | Format | Key | Description |
|-------------------|----------|------|--------|-----|-------------|
| billingID         | VARCHAR  | 6    | BLXXXX | PK | Unique billing ID |
| amountOutstanding | DECIMAL  | 10,2 | Numeric | —  | Amount owed |
| date              | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Billing date |
| claimID           | VARCHAR  | 6    | CLXXXX | FK | References Insurance_Claims |
| encounterID       | VARCHAR  | 6    | ENXXXX  | FK | References Medical_Encounters |
| amountPaid        | DECIMAL  | 10,2 | Numeric | —  | Amount paid |

---

## Table: Encounter_Statuses
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| status     | VARCHAR  | 10   |        | PK  | Possible encounter statuses |

---

## Table: Insurance_Claims
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| claimID    | VARCHAR  | 6    | CLXXXX | PK  | Unique claim ID |
| notes      | VARCHAR  | 300  |        | —   | Claim notes |
| providerID | VARCHAR  | 6    | PROXXX | FK  | References Insurance_Providers |

---

## Table: Insurance_Providers
| Column Name    | Data Type | Size | Format | Key | Description |
|---------------|----------|------|--------|-----|-------------|
| providerID    | VARCHAR  | 6    | PROXXX | PK  | Unique provider ID |
| providerName  | VARCHAR  | 45   |        | —   | Provider name |
| providerNotes | VARCHAR  | 45   |        | —   | Additional notes |

---

## Table: Medical_Encounters
| Column Name      | Data Type | Size | Format | Key | Description |
|-----------------|----------|------|--------|-----|-------------|
| encounterID     | VARCHAR  | 6    | ENXXXX | PK  | Unique encounter ID |
| encounterNotes  | VARCHAR  | 1000 |        | —   | Notes |
| date            | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Encounter date |
| encounterStatus | VARCHAR  | 10   |         | FK  | References Encounter_Statuses |
| appointmentID   | VARCHAR  | 6    | APXXXX | FK  | Linked appointment |
| physicianID     | VARCHAR  | 6    |       | FK  | References Physicians |

---

## Table: Medical_History
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| historyID    | INT      | —    | Integer | PK | Unique history ID |
| notes        | VARCHAR  | 1000 |         | —  | Medical notes |
| dateAdded    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Record created |
| dateModified | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Last updated |
| patientID    | VARCHAR  | 6    | PAXXXX    | FK | References Patients |

---

## Table: Medications
| Column Name    | Data Type | Size | Format | Key | Description |
|---------------|----------|------|--------|-----|-------------|
| medicationID  | VARCHAR  | 6    | MEDXXX | PK  | Unique medication ID |
| medicationName| VARCHAR  | 45   |        | —   | Brand name |
| genericName   | VARCHAR  | 45   |        | —   | Generic name |

---

## Table: Patients
| Column Name     | Data Type | Size | Format | Key | Description |
|----------------|----------|------|--------|-----|-------------|
| patientID      | VARCHAR  | 6    | PAXXXX | PK  | Unique patient ID |
| patientName    | VARCHAR  | 45   |        | —   | Full name |
| patientPhone   | VARCHAR  | 15   |        | —   | Phone |
| patientDOB     | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date of birth |
| dateAdded      | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date added |
| patientAddress | VARCHAR  | 70   |        | —   | Address |
| patientEmail   | VARCHAR  | 45   |        | —   | Email |

---

## Table: Physician_Has_Specialty
| Column Name | Data Type | Size | Format | Key | Description |
|------------|----------|------|--------|-----|-------------|
| specialtyID| INT      | —    | Integer| FK  | References Specialty |
| physicianID| VARCHAR  | 6    |        | FK  | References Physicians |
| dateAdded  | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date added |

---

## Table: Physicians
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| physicianID  | VARCHAR  | 6    |        | PK  | Unique physician ID |
| physicianName| VARCHAR  | 45   |        | —   | Name |
| startDate    | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Start date |

---

## Table: Prescriptions
| Column Name             | Data Type | Size | Format | Key | Description |
|------------------------|----------|------|--------|-----|-------------|
| patientID              | VARCHAR  | 6    | PAXXXX | FK  | References Patients |
| medicationID           | VARCHAR  | 6    | MEDXXX | FK  | References Medications |
| datePrescribed         | VARCHAR  | 45   |        | —   | Date prescribed |
| encounterPrescribedIn  | VARCHAR  | 6    |        | FK  | References Medical_Encounters |
| dosageAmount           | DECIMAL  | 10,3 | Numeric | —  | Dosage |
| dosageUnits            | VARCHAR  | 20   |         | —   | Units |

---

## Table: Specialty
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| specialtyID  | INT      | —    | Integer| PK  | Unique specialty ID |
| specialtyName| VARCHAR  | 45   | Text   | —   | Name of specialty |

