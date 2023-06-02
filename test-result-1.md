# Try to create a new case (TST23-00010)

## Attempt 1

### Request body
Send in normal payload (didn't send patient object at all): 
```
  {
    existingPatient: true,
    existingPatientMRN: "P100819018"
  }
```
### Response
```
"patient is rquired when creating a new case".
```

## Attempt 2

### Request body
```
{ 
  "patient": {
     existingPatient: true,
     existingPatientMRN: "P100819018"
  },
}
```

### Response
Got validation errors: 
```
[
    {
        "property": "patient",
        "children": [
            {
                "property": "contact",
                "children": [],
                "constraints": {
                    "isDefined": "contact should not be null or undefined"
                }
            },
            {
                "property": "address",
                "children": [],
                "constraints": {
                    "isDefined": "address should not be null or undefined"
                }
            },
            {
                "property": "medicationIDs",
                "children": [],
                "constraints": {
                    "isDefined": "medicationIDs should not be null or undefined"
                }
            },
            {
                "property": "insurances",
                "children": [],
                "constraints": {
                    "isDefined": "insurances should not be null or undefined"
                }
            }
        ]
    }
]
```

## Attempt 3

### Request body
Send patient with the info: 

```
"patient": {
    "existingPatient": true,
    "existingPatientMRN": "P100819018",
    "insurances": [
      {
        "payer": {
          "MCID": "Payer110"
        },
        "insuredRelationshipID": 1,
        "insuredContact": {
          "prefix": null,
          "firstName": "insuredfirstname",
          "middleName": null,
          "lastName": "insuredlastname",
          "suffix": null,
          "dateOfBirth": null,
          "sex": "M",
          "homePhone": null,
          "workPhone": null
        },
        "insuredAddress": {
          "street1": "",
          "countryCode": "US"
        },
        "memberNumber": "xxxxxxxxxxx",
        "groupNumber": "yyyy"
      }
    ],
    "contact": {
      "prefix": "Mr",
      "firstName": "TESTfirstName",
      "middleName": "M.",
      "lastName": "TESTLastName",
      "gender": "F",
      "suffix": "Jr",
      "sex": "F",
      "dateOfBirth": "1971-01-01",
      "phoneNumber": "318-824-9992",
      "socialSecurityNumber": "111221234"
    },
    "address": {
      "street1": "105 Bertrand drive",
      "street2": "Test street 2",
      "city": "Lafayette",
      "state": "LA",
      "zip": "70506-5414",
      "countryCode": "US"
    },
    "medicationIDs": []
  },
```

### Result
*Case was created!*

But... when pulling the case from the API... patient is empty and the changes seem to be applied 
the `casePatient`. 

``` 
"patient": {
     "medicalRecordNumber": null,
     "clinicalMedicalRecordNumber": null,
     "referringLabMedicalRecordNumber": null
},
"casePatient: {
  // has all the changes
```

