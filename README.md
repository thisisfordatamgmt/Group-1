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
| physicianID     | VARCHAR  | 6    | PHXXXX      | FK  | References Physicians |

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
| physicianID| VARCHAR  | 6    | PHXXXX       | FK  | References Physicians |
| dateAdded  | DATETIME | —    | YYYY-MM-DD HH:MM:SS | — | Date added |

---

## Table: Physicians
| Column Name   | Data Type | Size | Format | Key | Description |
|--------------|----------|------|--------|-----|-------------|
| physicianID  | VARCHAR  | 6    | PHXXXX | PK  | Unique physician ID |
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


# Queries

## Query 1

### Explanation:

<img width="1511" height="536" alt="Screenshot 2026-04-02 at 8 26 26 AM" src="https://github.com/user-attachments/assets/ccc7eff3-40a9-4f8f-bd5c-dfd34b5bbbd9" />

### Justification: 

## Query 2

### Explanation:

<img width="1511" height="536" alt="Screenshot 2026-04-02 at 8 27 00 AM" src="https://github.com/user-attachments/assets/d7463d3b-007c-4493-8a69-974b816531ce" />

### Justification:

## Query 3

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 28 06 AM" src="https://github.com/user-attachments/assets/1e007e40-09d7-4c39-bf4a-db82254efab0" />

### Justification:

## Query 4

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 28 40 AM" src="https://github.com/user-attachments/assets/fd352bf7-c2cb-484d-9f30-809f6c25a35f" />

### Justification:

## Query 5

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 06 AM" src="https://github.com/user-attachments/assets/618632c5-d629-4130-a3ac-cf17dc166ad3" />

### Justification:

## Query 6

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 37 AM" src="https://github.com/user-attachments/assets/3f59bf6b-6952-4edc-ac6e-014b1a835916" />

### Justification

## Query 7

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 55 AM" src="https://github.com/user-attachments/assets/3a787fcc-4b85-4c8d-803c-a53ce33bfc76" />

### Justification:

## Query 8

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 30 18 AM" src="https://github.com/user-attachments/assets/d5b2df4e-d9af-4749-be03-13ebc1013940" />

### Justification:

## Query 9

### Explanation:

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 31 17 AM" src="https://github.com/user-attachments/assets/a256ff96-4001-4d0c-a663-5a0154918f73" />

### Justification

## Query 10

### Explanation:

<img width="1511" height="574" alt="Screenshot 2026-04-02 at 8 33 16 AM" src="https://github.com/user-attachments/assets/c63764fc-ce98-48dc-add4-613d79c25127" />

### Justification:


