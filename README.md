# MIST 4610 Team 1

## Team Name

Sp26_71552_Group 1

## Team Members

- Grace Buckley 
- Jerry Chen
- Sanjana Karanth
- Sam Lashley
- Sai Shankar Sadhu
- Anaya Stinson

# Scenario Description


# Data Model

## Explanation:

Our model is based on the structure of a hypothetical medical clinic or healthcare practice. The central entity in the model is the Patients entity, which stores all relevant demographic and contact information for individuals receiving care at the clinic.

From the Patients entity, there are several important branches. First, the Medical_History table stores ongoing clinical notes for each patient. Because a single patient can have many medical history records over time, there is a one-to-many relationship between Patients and Medical_History.
Patients also book appointments at the clinic, which is represented by the one-to-many relationship between Patients and Appointments. The Appointments table tracks both the scheduled and actual appointment dates, the patient's stated concern, and the appointment's current status. The appointmentStatus field references the Appointment_Statuses table, which serves as a lookup entity containing the set of valid statuses an appointment can hold (e.g., "Scheduled," "Completed," "No-Show").

Each appointment leads to a Medical_Encounters record, and the model assumes that each medical encounter has only one appointment. This one-to-one relationship links the Appointments and Medical_Encounters tables. The Medical_Encounters entity captures the clinical details of the visit, including encounter notes, the date, and the encounter's status. Similar to appointments, the encounterStatus field references the Encounter_Statuses lookup table, which contains valid encounter statuses.

Each medical encounter is conducted by a physician, establishing a many-to-one relationship between Medical_Encounters and Physicians. The Physicians table stores the physician's name and start date. Because physicians can hold multiple specialties, and a specialty can belong to many physicians, the Physician_Has_Specialty associative entity resolves this many-to-many relationship between Physicians and Specialty. The Specialty table simply contains the specialty name (e.g., "Cardiology," "Pediatrics").

During a medical encounter, a physician may prescribe medications to a patient. The Prescriptions table sits at the intersection of three entities and contains three foreign keys. First, there is a one-to-many relationship between Patients and Prescriptions, as a single patient can receive many prescriptions over time. Second, there is a one-to-many relationship between Medications and Prescriptions, since the same medication can appear on many different prescriptions. Third, there is a one-to-many relationship between Medical_Encounters and Prescriptions through the encounterPrescribedIn field, because a single encounter can result in multiple prescriptions being written. In addition to these three foreign keys, the Prescriptions table records the date prescribed, the dosage amount, and the dosage units. The Medications table that feeds into Prescriptions stores both the brand name and generic name for each medication.

On the billing and insurance side of the model, each medical encounter can generate a billing record, represented by the one-to-many relationship between Medical_Encounters and Billing. The Billing table tracks the amount outstanding, amount paid, the billing date, and links to an insurance claim. The claimID field in Billing references the Insurance_Claims table, which stores notes about each claim and connects to the Insurance_Providers entity. Insurance_Providers contains the provider's name and any additional notes. This chain of relationships from Medical_Encounters through Billing to Insurance_Claims to Insurance_Providers models the full revenue cycle from the point of care to insurance reimbursement.


---
<img width="1200" height="850" alt="Group Project Diagram" src="https://github.com/user-attachments/assets/33eaf972-5ffb-483b-a924-b808a5e39403" />

# Data Dictionary

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

## Matrix

<img width="924" height="614" alt="Screenshot 2026-04-02 at 8 45 15 AM" src="https://github.com/user-attachments/assets/7330e486-86c8-4517-a00e-c18646e94715" />

## Query 1

### Description: 
Query to retrieve a patient's contact info given their ID number. 

<img width="1511" height="536" alt="Screenshot 2026-04-02 at 8 26 26 AM" src="https://github.com/user-attachments/assets/ccc7eff3-40a9-4f8f-bd5c-dfd34b5bbbd9" />

### Justification: 
The following query retrieves the contact information for patients in our database, which is necessary for sending confirmation messages regarding appointments and other details we, as a clinic, would like to send to our patients outside their appointment time. This query is very valuable to a manager because every clinic must maintain a proper record of all of the contact information of their clients, in fact it is a rule because without proper contact information, patients are not given updates about their appointment times or dates which could cause them to miss their appointment and therefore leave them dissatisfied by having to pay a late fee. When a manager runs this query, no null values should be present; if there are, it signals the clinic to enter data in that row or instance immediately to ensure proper communication.

## Query 2

### Description:
This query provides on average how long it takes from the date of the medical encounter for the patient to be billed for the services provided.


<img width="1511" height="536" alt="Screenshot 2026-04-02 at 8 27 00 AM" src="https://github.com/user-attachments/assets/d7463d3b-007c-4493-8a69-974b816531ce" />

### Justification:
This query provides information about the average number of days from a medical encounter to when the patient is billed for the services provided. This is a vital metric for telehealth clinics as minimizing the amount of time between when physicians render services and patients are billed lessens the time it takes to collect on accounts. Maintaining a reasonable average here is crucial to profitability as any delays could result in high revenue losses.

## Query 3

### Description:
Query provides the encounter ID, encounter date, patient name, status of the encounter, and the name of the physician

<img width="1512" height="611" alt="Screenshot 2026-04-02 at 11 29 43 AM" src="https://github.com/user-attachments/assets/c21abb98-c2ca-43b4-8721-6f6c7ae08de4" />

### Justification:
The following query retrieves the encounter's ID, encounter's date, patient’s name, the status of their encounter and the name of the physician that treated them. From a managerial standpoint, the clinic’s manager is in charge of managing the physicians and staff and making sure everything runs smoothly, so the manager should be aware of any encounter that is not yet closed, and they should also know the physician that is assigned that encounter, so they can follow up with the physician and make sure that they are in the process of closing that encounter. This query does a great job by giving the manager a general run down of the physician’s activity and workload regarding their patient’s appointments in the clinic.

## Query 4

### Description:
Get all insurance Providers that we accept

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 28 40 AM" src="https://github.com/user-attachments/assets/fd352bf7-c2cb-484d-9f30-809f6c25a35f" />

### Justification:
This following query retrieves all of the insurance providers that we as a clinic will accept and do business with. This is highly important information because the clinic needs to have reference of all of the various types of providers that are accepted so that if someone has an inquiry on whether or not the clinic accepts a certain provider, the manager or staff can look from the list of providers and check. This information is also helpful in a sense that management can look to expand its list of insurance providers to be more accommodating to all sorts of patients and attract new patients to the clinic if management finds that very little variety of insurance providers exist in the database.

## Query 5

### Description:
Identify customers who have an outstanding balance in billing and the respective amounts

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 06 AM" src="https://github.com/user-attachments/assets/618632c5-d629-4130-a3ac-cf17dc166ad3" />

### Justification:
This query will return back the patient’s name and ID along with their contact information and their outstanding balances. This is a highly important query that is very useful in the financial aspect of the clinic because the clinic needs to be aware of its accounts receivables, and make sure they are up to date regarding their financial information. The clinic needs to be able to contact certain patients who have still not paid yet, and the clinic needs to do that quickly so that the patient and the clinic can be up-to-date on the situation and the clinic would have done its part by informing the patient before they would be subject to any unnecessary additional fees or collections that come with penalties for not paying the balance on time. 

## Query 6

### Description:
Query lists out all of the physicians with their total amount billed and their average billing

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 37 AM" src="https://github.com/user-attachments/assets/3f59bf6b-6952-4edc-ac6e-014b1a835916" />

### Justification
This query will return the physician name, the total amount that they have billed a patient as well as the average amount they typically bill a customer. At this clinic, management wants to ensure impartiality and always being fair to our patients. Our goal is to not overcharge our clients for the services we provide and risk getting bad reviews, so it’s important that management has access to this information returned in this query to keep a check on the physician’s actions regarding the amounts that they are billing their patients. If there is a large discrepancy between the average billing amount and the specific billed amount, then that  may suggest that management has to conduct further investigation to maintain regulation and balance in the clinic. This practice will lead to increased customer satisfaction rates and a more attentive and regulated workplace environment.

## Query 7

### Description:
Query provides the percent of medications prescribed out of all prescriptions for physicians who have prescribed anything in a medical encounter

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 29 55 AM" src="https://github.com/user-attachments/assets/3a787fcc-4b85-4c8d-803c-a53ce33bfc76" />

### Justification:
This query will return the percentage of medications prescribed out of all prescriptions for physicians who have prescribed anything in a medical encounter. The results are grouped by each physician, so management is aware of what percentage of the total prescriptions relates to a certain physician. Recently, many debates and concerns are being raised about healthcare in the U.S. Many believe that U.S physicians are overprescribing their patients with medications that they may not actually need. Studies have shown that 20-25% of medications prescribed have been deemed unnecessary. The clinic wants to avoid any legal or moral issue, so it’s important that management is aware of what is going on at the clinic, and this way they are able to keep a look out for any physician who might be contributing to the majority of total prescriptions issued from the clinic. Management will then have to oversee that physician’s work and actions to ensure checks and regulations in the clinic.

## Query 8

### Description:
Query provides all physicians and the distinct number of patients they have seen.

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 30 18 AM" src="https://github.com/user-attachments/assets/d5b2df4e-d9af-4749-be03-13ebc1013940" />

### Justification:
This query will return back the physician name, and the number of different patients they have seen.
This query is useful when identifying patients’ preference over a specific physician. A physician might have had to deal with many encounters, but they were all between a few patients. This would likely lead management to misinterpret the information shown and conclude that a specific physician deals with multiple patients, when in fact they don’t. The DISTINCT clause makes sure that only unique instances of the patient’s ID are selected, so management can realize how many different customers each physician treats. This information can be found valuable to management when deciding bonuses and promotions for the clinic’s physicians. The physician that is most preferred by many different patients and treats the most people are reasonably going to be given a bonus or promotion. This will help encourage all the physicians to be on their best behavior when handling issues with the patients, and this in turn will help the clinic’s reviews and name.

## Query 9

### Description:
Find all the bills that have not yet had an insurance claim created for it. This query will retrieve information about all of the bills that have not yet had an insurance claim created for them yet. The query will also format the date of the medical encounter in a better way (Month/Day/Year) and also rename the amountOutstanding and amountPaid columns for better readability.

<img width="1511" height="570" alt="Screenshot 2026-04-02 at 8 31 17 AM" src="https://github.com/user-attachments/assets/a256ff96-4001-4d0c-a663-5a0154918f73" />

### Justification
The information retrieved by this query can be found useful from a managerial perspective because almost all bills should eventually have an insurance claim associated with them and if there is not the associated encounter cannot be closed until a claim is filed. Unfiled bills can cause issues with the clinic’s patients and their insurance providers later on because in order for an insurance provider to cover a medical encounter of their customer, an insurance claim must be attached to each bill. If the clinic can streamline and regulate this process by checking up on the status of the bills that do not yet have an insurance claim and attend to them promptly, the clinic can build a better relationship with its patients and maintain customer satisfaction. 

## Query 10

### Description:
This case when a statement query will sort out and label the different types of patients with different situations regarding their amounts outstanding. If a patient has an amount outstanding of less than or equal to $1,000, he/she is classified as having “Little Amount Due,” if the amount is less than or equal to $5,000, “Moderate Amount Due”, if the amount is less than or equal to $10,000 then “High Amount Due.” Patients with anything greater than $10,000 are classified as “Needs attention.”

<img width="1511" height="574" alt="Screenshot 2026-04-02 at 8 33 16 AM" src="https://github.com/user-attachments/assets/c63764fc-ce98-48dc-add4-613d79c25127" />

### Justification:
The classification of accounts is highly valuable information to management because they will be able to better classify their patients by segmenting them based on the aforementioned classifications. This information specifically will make things easier for management by giving them specific areas to keep an eye out for. For example, management would want to keep patients classified as anything other than “Little Amount Due” on their radar because those are the patients that are most alarming in reference to their outstanding bills. Management would seek to reduce those cases as much as possible to make sure they are up to date in their accounts receivables. Furthermore, in future analysis of the data, one could assign probabilities to each designation in order to provide an estimate of bad debt expense at the end of the term.

# Database Information:
Name of the database: `ns_Sp26_71552_Group1`

Additional information: Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL TP_Q1();
