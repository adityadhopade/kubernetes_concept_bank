# KUBECTL APPLY

- Kubectl Apply considers the 3 files while appplying it 

- ``1. Local File(yaml)``
- ``2. Last Applied Configuration``
- ``3. Live Object Configuration`` 

- When we hit apply it converts the definition.yaml file into the JSON Format which is stored under the Last Applied Configurations.
- IF we make a change in the ``local yaml file`` eg> change in the image name & if there is a difference between ``Live Object Configuration`` for the same field then it is bound to make the changes while applying "kubernetes apply"

## What is the need of the Last Applied Configuration then ?
- Last Applied Configurations it is used to verify what fields have been removed from the local file.

- eg> If a field is removed from the local file an we can see that field in the "Last Applied Configuration" it means that there is a change and the field has been removed so it also needs to be removed from the Live Object Configurations

## Where is the last applied Configuration JSON Stored? 
- It is inside the Live Object Configuration under Annotations