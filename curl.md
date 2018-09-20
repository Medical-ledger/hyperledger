### Register Hospital

 * hospital Id
 * name

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.Hospital", 
   "hospitalID": "h1", 
   "name": "h1"
 }' 'http://localhost:3000/api/org.medical.ledger.Hospital'

```

### Register Admins for hospitals
 
 * admin Id
 * hospital name

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.Admin", 
   "adminID": "a1",
   "hospital": "resource:org.medical.ledger.Hospital#h1" 
 }' 'http://localhost:3000/api/org.medical.ledger.Admin'

```
### Register doctor to hospital

 * doctor Id
 * firstName
 * lastName
 * salary
 * admin name

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.RegisterDoctor", 
   "doctor": {
     "$class": "org.medical.ledger.Doctor", 
     "doctorID": "d1", 
     "name": { 
       "$class": "org.medical.ledger.Name", 
       "firstName": "d1", 
       "lastName": "d1" 
     },
     "salary": "100"
   },
   "admin": "resource:org.medical.ledger.Admin#a1"
 }' 'http://localhost:3000/api/org.medical.ledger.RegisterDoctor'

```
### Register Patient

 * patient Id
 * firstName 
 * lastName 
 * email 
 * phone
 * city (optional)
 * country (optional)
 * street (optional)
 * dayofBirth (optional)
 * gender (MALE, FEMALE , OTHER) (optional)
	
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.Patient", 
   "patientID": "p1",
   "name": {
     "$class": "org.medical.ledger.Name",
     "firstName": "f1",
     "lastName": "l1" 
   },
   "contactDetails": { 
     "$class": "org.medical.ledger.ContactDetails", 
     "email": "e1",
     "phone": "p1", 
     "address": { 
       "$class": "org.medical.ledger.Address", 
       "city": "c1",
       "country": "c1", 
       "street": "s1" 
     }
   }, 
   "dayOfBirth": "2018-09-20T14:27:42.966Z", 
   "gender": "MALE",
   "age": 60
   
 }' 'http://localhost:3000/api/org.medical.ledger.Patient'


```
### Request Appointment as a Patient
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.RequestAppointment",
   "description": "having cold fever plz book my appoinment", 
   "patient": "resource:org.medical.ledger.Patient#p1", 
   "hospital": "resource:org.medical.ledger.Hospital#h1"
 }' 'http://localhost:3000/api/org.medical.ledger.RequestAppointment'

```

### Approve Patient Appointment as Hospital Admin
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.ApproveAppointment", 
   "appointment": { 
     "$class": "org.medical.ledger.Appointment", 
     "appointmentId": "aa1", 
     "time": "2018-09-20T14:37:56.607Z", 
     "patient": "resource:org.medical.ledger.Patient#p1" 
   }, 
   "doctor": "resource:org.medical.ledger.Doctor#d1", 
   "admin": "resource:org.medical.ledger.Admin#a1"
 }' 'http://localhost:3000/api/org.medical.ledger.ApproveAppointment'

```


### Reject Patient Appointment as Hospital Admin
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ 
   "$class": "org.medical.ledger.RejectAppointment",
   "appointment": "resource:org.medical.ledger.Appointment#a1", 
   "admin": "resource:org.medical.ledger.Admin#a1"
 }' 'http://localhost:3000/api/org.medical.ledger.RejectAppointment'

```

### Process Patient Appointment as Appointed Doctor
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
   "$class": "org.medical.ledger.ProcessAppointment", 
   "treatment": { 
     "$class": "org.medical.ledger.Treatment", 
     "diagnosis": { 
       "$class": "org.medical.ledger.Diagnosis", 
       "diseases": [ 
         { 
         	"name": "cancer" 
       	},
       	{ 
         	"name": "cold" 
         } 
       ] 
     }, 
     "medication": [ 
       { 
         "name": "medicine1", 
         "quantity": "100 mg", 
         "description": "with milk" 
       }, 
       { 
         "name": "medicine2", 
         "quantity": "10 mg", 
         "description": "without milk" 
       } 
     ], 
     "description": "get back to us in 5 days" 
   }, 
   "appointment": "resource:org.medical.ledger.Appointment#aa1", 
   "doctor": "resource:org.medical.ledger.Doctor#d1" 
 }' 'http://localhost:3000/api/org.medical.ledger.ProcessAppointment'

```

