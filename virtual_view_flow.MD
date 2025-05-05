flowchart TD
    subgraph "LDM Virtual View System"
        User[User] --> |Defines| LDM[Logical Data Model]
        User --> |Submits| Query[Query]
        
        LDM --> |Contains| Logic[Business Logic]
        LDM --> |Has| PK[Primary Key]
        
        System[System] --> |Generates| AutoMV[Auto MV]
        System --> |Materializes| UserMV[User Defined MV]
        
        ETL[ETL Process] --> |Feeds| AutoMV
        UserQuery[User Query] --> |Feeds| AutoMV
        
        Logic --> |Binds to| Model[Data Model]
        Logic --> |Creates| Dependency[Natural Dependency]
        
        ODS[ODS Tables] --> |Partial columns| MaterializedData[Materialized Data]
        
        Query --> |Processed by| CBO[Cost-Based Optimizer]
        CBO --> |Rewrites| ExecutionPlan[Execution Plan]
        
        MaterializedData --> |Influences| ExecutionPlan
        ExecutionPlan --> |Uses| DataSource{Data Source Selection}
        
        DataSource --> |May use| OriginalTable[Original Table]
        DataSource --> |May use| MaterializedView[Materialized View]
        DataSource --> |May use| ODSData[ODS Data]
        
        ExecutionPlan --> |Returns| Results[Query Results]
    end