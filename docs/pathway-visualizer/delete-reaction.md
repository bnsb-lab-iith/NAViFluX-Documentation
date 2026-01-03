---
hide:
  toc: true             # hides the right sidebar
---

The **Delete Reaction feature** enables you to completely remove specific reactions of your choice from the model.

![Delete Reaction](./../images//pathway-visualizer/delete-reaction.png)

!!! tip
    If you wish to undo all deletions, check out [Reset Button](./reset-button.md)

### **How Delete Reaction works**

!!! tip "Recommendation"
    It is highly advised to understand the difference between metabolite and reaction nodes. [Notations Documentation](./../pathway-visualizer/notations.md)

#### Before Deletion

Consider a custom model, where a metabolite is part of two reactions. The aim is to demonstrate the **Delete Reaction** feature. Lets say you want to **delete Reaction - R2**

```mermaid
graph LR
    A ---> R1
    B ---> R1
    R1 ---> C
    R1 ---> D
    C ---> R2 
    R2 ---> E

    %% Define styles
    classDef reaction fill:#4a90e2,stroke:#2c3e50,stroke-width:2px,rx:5px,ry:5px,color:#fff;
    classDef metabolite fill:#27ae60,stroke:#145a32,stroke-width:1.5px,color:#fff,stroke-dasharray:0;

    %% Assign classes
    class R1,R2,R3 reaction;
    class A,B,C,D,E,F,G metabolite;

```
Since **metabolite C** is part of both R1 and R2, deleting the reaction R2 will not delete metabolite C. Instead it only deletes nodes R2 and E.

#### After Deletion

```mermaid
graph LR
    A ---> R1
    B ---> R1
    R1 ---> C
    R1 ---> D
    

    %% Define styles
    classDef reaction fill:#4a90e2,stroke:#2c3e50,stroke-width:2px,rx:5px,ry:5px,color:#fff;
    classDef metabolite fill:#27ae60,stroke:#145a32,stroke-width:1.5px,color:#fff,stroke-dasharray:0;

    %% Assign classes
    class R1 reaction;
    class A,B,C,D metabolite;

```