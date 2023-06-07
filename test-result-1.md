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


# LATEST 

```
{
  "caseNumber": "TST23-00014",
  "client": {
    "npi": "1841363512"
  },
  "dateOfService": "2023-06-01",
  "diagnoses": [
    {
      "description": "",
      "codeSystem": "ICD10",
      "code": "Z12.11",
      "mode": "Pre-Op"
    },
    {
      "description": "",
      "codeSystem": "ICD10",
      "code": "Z12.12",
      "mode": "Post-Op"
    }
  ],
  "disciplineIdentifier": "Pathology",
  "disciplineSpecialtyIdentifier": "Gastrointestinal",
  "isClientBilled": false,
  "leanLab": {
    "mcid": "Gastrointestinal_Specialists_AMC_97d88e"
  },
  "locationOfService": {
    "npi": "1114051463"
  },
  "modalityIdentifier": "Pathology",
  "operation": "create",
  "orderingApplication": "aps",
  "existingPatient": true,
  "existingpatientMRN": "P100819018",
  "patient": {

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
      "firstName": "TESTAnotherFirstNAme",
      "middleName": "M.",
      "lastName": "TESTAntoherLastName",
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
  "physicians": [
    {
      "npi": "1558371450",
      "relationship": "ordering"
    },
    {
      "npi": "1366519423",
      "relationship": "referring"
    }
  ],
  "receivedDate": "2022-10-18T03:11:00.000Z",
  "receivingLab": {
    "mcid": "APS_Lab"
  },
  "requisitionNumber": "LGEC_32541",
  "screening": false,
  "specimens": [
    {
      "deleted": false,
      "grossDescription": "A created gross description... processing.",
      "parentSampleNumber": null,
      "pathology": {
        "additionalDescription": null,
        "anatomicalDistance": null,
        "multiplier": null,
        "pathologyStain": null,
        "ruleOuts": [
          {
            "specimenPathologyRequestMCID": "RuleOut_Other",
            "otherFreeText": "Other rule out free text"
          }
        ],
        "specimenType": {
          "MCID": "Pathology_Snare"
        },
        "tissueOrigin": {
          "MCID": "(GI) Anus"
        },
        "tissueOriginPrefix": {
          "MCID": "Proximal"
        },
        "tissueOriginSuffix": {
          "MCID": "Polyp"
        },
        "tissueType": {
          "MCID": "Double"
        }
      },
      "sampleNumber": "-A",
      "sampleType": {
        "MCID": "Specimen"
      },
      "specimenModality": "Pathology"
    },
    {
      "deleted": false,
      "parentSampleNumber": "-A",
      "pathology": {
        "additionalDescription": null,
        "anatomicalDistance": null,
        "multiplier": null,
        "pathologyStain": null,
        "ruleOuts": [],
        "specimenType": {
          "MCID": "Pathology_Snare"
        },
        "tissueOrigin": {
          "MCID": "(GI) Anus"
        },
        "tissueOriginPrefix": {
          "MCID": "Proximal"
        },
        "tissueOriginSuffix": {
          "MCID": "Polyp"
        },
        "tissueType": {
          "MCID": "Double"
        }
      },
      "sampleNumber": "-A-1",
      "sampleType": {
        "MCID": "Cassette"
      },
      "specimenModality": "Pathology"
    },
    {
      "deleted": false,
      "parentSampleNumber": "-A-1",
      "pathology": {
        "additionalDescription": null,
        "anatomicalDistance": null,
        "multiplier": null,
        "pathologyStain": {
          "MCID": "H&E"
        },
        "ruleOuts": [],
        "specimenType": {
          "MCID": "Pathology_Snare"
        },
        "tissueOrigin": {
          "MCID": "(GI) Anus"
        },
        "tissueOriginPrefix": {
          "MCID": "Proximal"
        },
        "tissueOriginSuffix": {
          "MCID": "Polyp"
        },
        "tissueType": {
          "MCID": "Double"
        }
      },
      "sampleNumber": "-A-1-1",
      "sampleType": {
        "MCID": "Slide"
      },
      "specimenModality": "Pathology"
    },
    {
      "deleted": false,
      "parentSampleNumber": "-A-1",
      "pathology": {
        "additionalDescription": null,
        "anatomicalDistance": null,
        "multiplier": null,
        "pathologyStain": {
          "MCID": "DQ"
        },
        "ruleOuts": [],
        "specimenType": {
          "MCID": "Pathology_Snare"
        },
        "tissueOrigin": {
          "MCID": "(GI) Anus"
        },
        "tissueOriginPrefix": {
          "MCID": "Proximal"
        },
        "tissueOriginSuffix": {
          "MCID": "Polyp"
        },
        "tissueType": {
          "MCID": "Double"
        }
      },
      "sampleNumber": "-A-1-2",
      "sampleType": {
        "MCID": "Slide"
      },
      "specimenModality": "Pathology"
    },
    {
      "deleted": false,
      "parentSampleNumber": "-A-1",
      "pathology": {
        "additionalDescription": null,
        "anatomicalDistance": null,
        "multiplier": null,
        "pathologyStain": {
          "MCID": "BSLL"
        },
        "ruleOuts": [],
        "specimenType": {
          "MCID": "Pathology_Snare"
        },
        "tissueOrigin": {
          "MCID": "(GI) Anus"
        },
        "tissueOriginPrefix": {
          "MCID": "Proximal"
        },
        "tissueOriginSuffix": {
          "MCID": "Polyp"
        },
        "tissueType": {
          "MCID": "Double"
        }
      },
      "sampleNumber": "-A-1-3",
      "sampleType": {
        "MCID": "Slide"
      },
      "specimenModality": "Pathology"
    }
  ],
  "stat": false,
  "subModalityIdentifier": "Gastrointestinal",
  "testCase": false
}
```

