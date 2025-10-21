%% ===========================================
%% ProIT System Use Case Diagram (GitHub Safe)
%% ===========================================

flowchart LR
    %% === Define Actors ===
    Client((Client))
    Developer((Developer))
    DevOps((DevOps Engineer))
    Trainer((Trainer))
    Consultant((Consultant))
    Admin((Admin))

    %% === System Boundary ===
    subgraph ProIT_System [ProIT System]
        UC1([Request Project])
        UC2([Make Payment])
        UC3([Develop Software])
        UC4([Deploy Application])
        UC5([Provide Training])
        UC6([Consult Client])
        UC7([Generate Report])
        UC8([Manage User Accounts])
        UC9([Provide Support])
    end

    %% === Actor Interactions ===
    Client --- UC1
    Client --- UC2
    Client --- UC9

    Developer --- UC3
    DevOps --- UC4
    Trainer --- UC5
    Consultant --- UC6
    Admin --- UC7
    Admin --- UC8

    %% === Include Relationships ===
    UC1 -.-> UC2:::include
    UC3 -.-> UC4:::include

    %% === Extend Relationships ===
    UC1 -.-> UC9:::extend
    UC6 -.-> UC1:::extend

    %% === Styles for include/extend ===
    classDef include stroke-dasharray: 5 5,stroke:#008000,color:#008000;
    classDef extend stroke-dasharray: 5 5,stroke:#0000ff,color:#0000ff;
