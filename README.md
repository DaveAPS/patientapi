

We **currently** send this payload in the `POST /v4/lims/cases`:

``` json
"patient": {
    "insurances": [
      // PRIMARY (if used)
      {
        "payer": {"MCID": 1234},
        "insuredRelationshipID": 12,
        "insuredContact": {
          "firstName": "",
          "lastName": "",
          "sex":"M"
        },
        "insuredAddress": {
          "street1": "",
          "countryCode": "US"
        },
        "memberNumber": "SomeNumber",
        "groupNumber": "SomeNumber",
      },
      // SECONDARY (if used)
      {
        "payer": {"MCID": 1234},
        "insuredRelationshipID": 12,
        "insuredContact": {
          "firstName": "",
          "lastName": "",
          "sex":"M"
        },
        "insuredAddress": {
          "street1": "",
          "countryCode": "US"
        },
        "memberNumber": "SomeNumber",
        "groupNumber": "SomeNumber",
      },
      // TERTIARY (if used)
    ],
    "contact": {
      "prefix": "",
      "firstName": "TEST",
      "middleName": "",
      "lastName": "TEST",
      "suffix": "",
      "email": "",
      "sex": "M",
      "dateOfBirth": "1952-01-01",
      "phoneNumber": "",
      "socialSecurityNumber": null
      "workPhone": "",
    },
    "address": {
      "street1": "4115 Tall Trees Ln",
      "street2": "",
      "city": "St Augustine",
      "state": "FL",
      "zip": "32086-5884",
      "countryCode": "US"
    },
    "medicationIDs": [], // we never use this, but the validtion requires it. 
    "referringMedicalRecordNumber": "11731"
  },
}
```

## Option 1 (preferred)

- New endpoint to create patients. `POST /api/v4/lims/patients` using the same payload as above. Returns (at minimum): 

  ``` json
  {
    "ID": 123456,
  }
  ```
- New endpoint to update patients. `PATCH /api/v4/lims/patients/:patientMRN`. 
- Update to `POST /api/v4/lims/cases` client can send either the patient payload above (as is) to update `casePatient`, or send a "MCID" to link a 
  patient to the case:
  
  ``` json
  {
    // ... other case stuff
    "patient": { "MCID": 1032 }
    // ... other case stuff
  }
  ```
  
  No updates are accepted to the patient if the "MCID" is included. This would be a non-breaking change to how the endpoint currently works, since the
  `casePatient` update continues to work as is with it's current payload. 

## Option 2 (may/may not be easier for you)

- Modify the `POST/ api/v4/lims/cases` endpoint wuse the same payload as above. If client includes a patient's ID ("MCID"), it will link  
  the patient to the case and update the patient's info with the inlcuded payload. If the client does *NOT* include "MCID", only the 
  `casePatient` is updated: 

  ```json
  { 
     // ... other case stuff
     patient: {
       "MCID": 1032, // if inlcuded, it updates/adds the patient as a linked patient, if not, the `casePatient` is updated.
       ... normaal patient payload, updates the 'patients' data table
     }, 
  }
  ```
  
  This too would be a non-breaking change to the endpoint, but all of the 'patient' updates would have to be handled server-side.
                                                        
