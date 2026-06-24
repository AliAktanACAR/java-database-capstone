# Schema Design

## MySQL Database Design

### Table: patients

* id: INT, Primary Key, Auto Increment
* first_name: VARCHAR(100), Not Null
* last_name: VARCHAR(100), Not Null
* email: VARCHAR(255), Unique, Not Null
* phone: VARCHAR(20), Not Null
* date_of_birth: DATE
* created_at: TIMESTAMP

### Table: doctors

* id: INT, Primary Key, Auto Increment
* first_name: VARCHAR(100), Not Null
* last_name: VARCHAR(100), Not Null
* specialization: VARCHAR(100), Not Null
* email: VARCHAR(255), Unique, Not Null
* phone: VARCHAR(20)
* available: BOOLEAN

### Table: appointments

* id: INT, Primary Key, Auto Increment
* doctor_id: INT, Foreign Key → doctors(id)
* patient_id: INT, Foreign Key → patients(id)
* appointment_time: DATETIME, Not Null
* duration_minutes: INT, Default 60
* status: INT (0 = Scheduled, 1 = Completed, 2 = Cancelled)

### Table: admin

* id: INT, Primary Key, Auto Increment
* username: VARCHAR(100), Unique, Not Null
* password_hash: VARCHAR(255), Not Null
* email: VARCHAR(255), Unique

### Table: clinic_locations

* id: INT, Primary Key, Auto Increment
* name: VARCHAR(100), Not Null
* address: VARCHAR(255), Not Null
* phone: VARCHAR(20)

### Notes

* Patient appointment history should be retained.
* Doctors should not have overlapping appointments.
* Deleting a patient should not automatically remove historical appointment records.

---

## MongoDB Collection Design

### Collection: prescriptions

```json
{
  "_id": "ObjectId('64abc123456')",
  "appointmentId": 51,
  "patientId": 12,
  "doctorId": 5,
  "medications": [
    {
      "name": "Paracetamol",
      "dosage": "500mg",
      "frequency": "Every 6 hours"
    }
  ],
  "doctorNotes": "Drink plenty of water and rest.",
  "tags": ["fever", "pain-relief"],
  "refillCount": 2,
  "createdAt": "2026-06-24T10:00:00Z",
  "pharmacy": {
    "name": "City Pharmacy",
    "location": "Downtown"
  }
}
```

### Notes

* MongoDB is used for flexible prescription data.
* Documents reference patients and doctors using IDs.
* The schema can evolve without changing SQL tables.
