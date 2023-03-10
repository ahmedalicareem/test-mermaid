# test-mermaid

````mermaid
sequenceDiagram
    participant captain as CAPTAIN API GATEWAY
    participant supply as SUPPLY REGISTRY SERVICE
    participant lead as LEAD MANAGEMENT SERVICE
    participant cash as CASH IN SERVICE
    participant e-captain as CAPTAIN-EARNING WORKER
    par ONBOARD LEAD
        activate captain
        activate lead
        captain->>lead: ONBOARD LEAD CAPTAIN
        deactivate captain
        lead->>lead:CREATE CAPTAIN
        activate supply
        lead->>supply: PUBLISH CAPTAIN_LEAD_APPROVED_FOR_CREATION_ON_CORE_VIA_SRS_EVENT
        deactivate lead
        supply->>supply: SAVE DRIVER
        activate cash
        supply->>cash: PUBLISH CAPTAIN_UPDATE EVENT
        activate lead
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES EVENT
        deactivate cash
        supply->>supply: SEND CAPTAIN CREATION SMS
        supply->>supply: SAVE CAPTAIN DOCUMENTS
        activate lead
        supply->>lead: PUBLISH CAPTAIN_CREATION_RESPONSE EVENT
        lead->>supply: PUBLISH CAR_LEAD_APPROVED_FOR_CREATION_ON_CORE EVENT
        supply->>supply: SAVE CAR
        supply->>lead: PUBLISH CAR_CREATION_RESPONSE EVENT
        lead->>supply: PUBLISH PUBLISH LIMO_LEAD_APPROVED_FOR_CREATION_ON_CORE EVENT
        supply->>supply: CREATE AND ASSIGN LIMO COMPANY
        supply->>lead: PUBLISH LIMO_CREATION_RESPONSE EVENT
        deactivate lead
        deactivate supply
    end
    par ADD CAPTAIN
        activate captain
        activate supply
        captain->>supply: ADD CAPTAIN
        supply->>supply: SAVE CAPTAIN
        activate cash
        supply->>cash: PUBLISH CAPTAIN_UPDATE EVENT
        activate lead
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES EVENT
        deactivate cash
        supply->>supply: SAVE DOCUMENTS
        supply->>supply: SAVE CAR
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    par ACTIVATE CAPTAIN
        activate captain
        activate supply
        captain->>supply: ACTIVATE CAPTAIN
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    par CAPTAIN DETAILS
        activate captain
        activate supply
        captain->>supply: GET CAPTAIN DETAILS
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    par EDIT CAPTAIN
        activate captain
        activate supply
        captain->>supply: EDIT CAPTAIN
        activate cash
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES
        deactivate cash
        supply->>supply: UPDATE DRIVER
        supply->>supply: UPDATE DRIVER DETAILS
        supply->>supply: UPDATE DRIVER PHONE
        supply->>supply: VERIFY DOCUMENTS
        supply->>supply: SAVE DOCUMENTS
        supply->captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH CAPTAIN_UPDATE EVENT
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        deactivate supply
    end
    par ADD LIMO COMPANY
        activate captain
        activate supply
        captain->>supply: ADD LIMO COMPANY
        supply->>supply: SAVE ADDRESS
        supply->>supply: SAVE LIMO COMPANY
        supply->>supply: SAVE LIMO COMPANY DETAILS
        supply->>supply: ASSIGN LIMO COMPANY TO SERVICE PROVIDER
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH LIMO_COMPANY_IN_SG EVENT
        deactivate supply
        lead->>lead: UPDATE LIMO COMPANY
        deactivate lead
    end
    par EDIT LIMO COMPANY
        activate captain
        activate supply
        captain->>supply: EDIT LIMO COMPANY
        supply->>supply: UPDATE LIMO COMPANY DETAILS
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH SYNC_LIMO_COMPANY_IN_SG EVENT
        lead->>lead: UPDATE LIMO COMPANY
        deactivate lead
        activate e-captain
        supply->>e-captain: PUBLISH LIMO_COMPANY_EDITED EVENT
        deactivate e-captain
        deactivate supply
    end
    par ADD CAR
        activate captain
        activate supply
        captain->>supply: ADD CAR
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH UPSERT_CAR EVENT
        deactivate lead
        deactivate supply
    end
    par EDIT CAR
        activate captain
        activate supply
        captain->>supply: EDIT CAR
        supply->>supply: ASSIGN DRIVER CAR TYPE
        supply->>supply: ASSIGN DEDICATED DRIVER FOR CAR
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH UPSERT_CAR EVENT
        deactivate lead
        deactivate supply
    end
    par ADD CAR MAKE
        activate captain
        activate supply
        captain->>supply: ADD CAR MAKE
        supply->>supply: SAVE CAR MAKE
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
````


````mermaid
sequenceDiagram
    participant captain as CAPTAIN API GATEWAY
    participant supply as SUPPLY REGISTRY SERVICE
    participant lead as LEAD MANAGEMENT SERVICE
    participant cash as CASH IN SERVICE
    participant ecaptain as CAPTAIN-EARNING WORKER
    rect rgba(236, 236, 255,1)
    Note right of captain: ONBOARD LEAD
        activate captain
        activate lead
        captain->>lead: ONBOARD LEAD CAPTAIN
        deactivate captain
        lead->>lead:CREATE CAPTAIN
        activate supply
        lead->>supply: PUBLISH CAPTAIN_LEAD_APPROVED_FOR_CREATION_ON_CORE_VIA_SRS_EVENT
        deactivate lead
        supply->>supply: SAVE DRIVER
        activate cash
        supply->>cash: PUBLISH CAPTAIN_UPDATE EVENT
        activate lead
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES EVENT
        deactivate cash
        supply->>supply: SEND CAPTAIN CREATION SMS
        supply->>supply: SAVE CAPTAIN DOCUMENTS
        activate lead
        supply->>lead: PUBLISH CAPTAIN_CREATION_RESPONSE EVENT
        lead->>supply: PUBLISH CAR_LEAD_APPROVED_FOR_CREATION_ON_CORE EVENT
        supply->>supply: SAVE CAR
        supply->>lead: PUBLISH CAR_CREATION_RESPONSE EVENT
        lead->>supply: PUBLISH PUBLISH LIMO_LEAD_APPROVED_FOR_CREATION_ON_CORE EVENT
        supply->>supply: CREATE AND ASSIGN LIMO COMPANY
        supply->>lead: PUBLISH LIMO_CREATION_RESPONSE EVENT
        deactivate lead
        deactivate supply
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: ADD CAPTAIN
        activate captain
        activate supply
        captain->>supply: ADD CAPTAIN
        supply->>supply: SAVE CAPTAIN
        activate cash
        supply->>cash: PUBLISH CAPTAIN_UPDATE EVENT
        activate lead
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES EVENT
        deactivate cash
        supply->>supply: SAVE DOCUMENTS
        supply->>supply: SAVE CAR
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: ACTIVATE CAPTAIN
        activate captain
        activate supply
        captain->>supply: ACTIVATE CAPTAIN
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: CAPTAIN DETAILS
        activate captain
        activate supply
        captain->>supply: GET CAPTAIN DETAILS
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: EDIT CAPTAIN
        activate captain
        activate supply
        captain->>supply: EDIT CAPTAIN
        activate cash
        supply->>cash: PUBLISH CAPTAIN_INFO_ATTRIBUTES
        deactivate cash
        supply->>supply: UPDATE DRIVER
        supply->>supply: UPDATE DRIVER DETAILS
        supply->>supply: UPDATE DRIVER PHONE
        supply->>supply: VERIFY DOCUMENTS
        supply->>supply: SAVE DOCUMENTS
        supply->captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH CAPTAIN_UPDATE EVENT
        supply->>lead: PUBLISH CAPTAIN_PROFILE_UPDATE EVENT
        deactivate lead
        deactivate supply
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: ADD LIMO COMPANY
        activate captain
        activate supply
        captain->>supply: ADD LIMO COMPANY
        supply->>supply: SAVE ADDRESS
        supply->>supply: SAVE LIMO COMPANY
        supply->>supply: SAVE LIMO COMPANY DETAILS
        supply->>supply: ASSIGN LIMO COMPANY TO SERVICE PROVIDER
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH LIMO_COMPANY_IN_SG EVENT
        deactivate supply
        lead->>lead: UPDATE LIMO COMPANY
        deactivate lead
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: EDIT LIMO COMPANY
        activate captain
        activate supply
        captain->>supply: EDIT LIMO COMPANY
        supply->>supply: UPDATE LIMO COMPANY DETAILS
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH SYNC_LIMO_COMPANY_IN_SG EVENT
        lead->>lead: UPDATE LIMO COMPANY
        deactivate lead
        activate ecaptain
        supply->>ecaptain: PUBLISH LIMO_COMPANY_EDITED EVENT
        deactivate ecaptain
        deactivate supply
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: ADD CAR
        activate captain
        activate supply
        captain->>supply: ADD CAR
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH UPSERT_CAR EVENT
        deactivate lead
        deactivate supply
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: EDIT CAR
        activate captain
        activate supply
        captain->>supply: EDIT CAR
        supply->>supply: ASSIGN DRIVER CAR TYPE
        supply->>supply: ASSIGN DEDICATED DRIVER FOR CAR
        supply->>captain: SUCCESS
        deactivate captain
        activate lead
        supply->>lead: PUBLISH UPSERT_CAR EVENT
        deactivate lead
        deactivate supply
    end
    rect rgba(236, 236, 255,1)
    Note right of captain: ADD CAR MAKE
        activate captain
        activate supply
        captain->>supply: ADD CAR MAKE
        supply->>supply: SAVE CAR MAKE
        supply->>captain: SUCCESS
        deactivate supply
        deactivate captain
    end
````
