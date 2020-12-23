## Persistent Volume Claims

Created by the developer to request for a persistent volume.

Characteristics:
- Each PVC is attached to only one PV.

PV is chosen based on the below criteria
- Sufficient capacity
- Access mode
- Volume mode
- Storage class.
- Selector

#### Discussion
- What happens if there are more than one PV available for the PVC
    - You can request for a particular PV using the selector match label in the PVC. 
- Can a smaller storage claim get attached to a larger claim. 
- Can a larger storage claim get attached to a smaller claim. 
- Claim till attached to the volume will be in PENDING state. 

#### What happens when a PVC that is bound to a PV is deleted.
Different types:
- Retain (Data is retained)
- Delete (Data and storage is deleted)
- Recycle (Data is deleted and available for other claims)
