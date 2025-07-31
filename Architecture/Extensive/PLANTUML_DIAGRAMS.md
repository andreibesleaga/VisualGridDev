# VisualGridDev v5.0 - PlantUML Diagrams

This document contains PlantUML source for all required architecture diagrams: C4 (all levels), arc42, system, context, state, sequence, runtime, security, and deployment. Each diagram is referenced in the main documentation and can be rendered for visual clarity.

---

## 1. C4 Context Diagram

```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(dev, "Developer")
Person(admin, "Admin")
System_Boundary(visualgriddev, "VisualGridDev Platform") {
  System(ide, "Visual IDE", "Web/VS Code")
  System(runtime, "Flow Runtime", "Node/Edge/Cloud")
  System(ai, "AI/ML Orchestrator", "LLM, ML, RAG")
  System(mesh, "Mesh Network", "libp2p, MQTT, etc.")
  System(monitor, "Monitoring Dashboard", "Real-time UI")
}
Rel(dev, ide, "Uses")
Rel(admin, monitor, "Monitors")
Rel(ide, runtime, "Deploys Flows")
Rel(runtime, mesh, "Joins Mesh")
Rel(runtime, ai, "Invokes AI/ML")
Rel(runtime, monitor, "Reports Health")
@enduml
```

---

## 2. C4 Container Diagram

```plantuml
@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

System_Boundary(visualgriddev, "VisualGridDev Platform") {
  Container(ide, "Visual IDE", "React/TS", "Visual programming, live collaboration")
  Container(api, "API Gateway", "Node.js/Express", "REST/gRPC/GraphQL")
  Container(runtime, "Flow Runtime", "Node.js/Python", "Executes agent flows")
  Container(mesh, "Mesh Agent", "libp2p, MQTT", "Self-healing, mesh comms")
  Container(ai, "AI/ML Engine", "Python/LLM", "Inference, RAG, learning")
  Container(monitor, "Monitoring Dashboard", "React/TS", "Real-time health/status")
  Container(db, "Database", "Postgres/Redis", "State, config, logs")
}
Rel(ide, api, "API calls")
Rel(api, runtime, "Deploys/Manages Flows")
Rel(runtime, mesh, "Mesh comms")
Rel(runtime, ai, "AI/ML calls")
Rel(runtime, monitor, "Health/Status")
Rel(api, db, "Reads/Writes")
Rel(monitor, db, "Reads Metrics")
@enduml
```

---

## 3. arc42 System Overview

```plantuml
@startuml
actor Developer
actor Admin
rectangle "VisualGridDev Platform" {
  rectangle "Visual IDE" as IDE
  rectangle "API Gateway" as API
  rectangle "Flow Runtime" as RT
  rectangle "Mesh Agent" as Mesh
  rectangle "AI/ML Engine" as AI
  rectangle "Monitoring Dashboard" as Mon
  rectangle "Database" as DB
}
Developer --> IDE : Uses
Admin --> Mon : Monitors
IDE --> API : API Calls
API --> RT : Deploys Flows
RT --> Mesh : Mesh Comms
RT --> AI : AI/ML Calls
RT --> Mon : Health/Status
API --> DB : State/Config
Mon --> DB : Metrics
@enduml
```

---

## 4. Security Architecture Diagram

```plantuml
@startuml
actor User
actor Admin
rectangle "VisualGridDev Platform" {
  rectangle "Self-Healing Agent" as Agent
  rectangle "Extension Manager" as Ext
  rectangle "Security Policy Engine" as Sec
  rectangle "Monitoring Dashboard" as Mon
}
User --> Agent : Uses
Admin --> Mon : Monitors
Agent --> Ext : Loads/Validates Plugins
Agent --> Sec : Enforces Policies
Agent --> Mon : Reports Health/Security
@enduml
```

---

## 5. State Diagram: Flow Deployment & Healing

```plantuml
@startuml
[*] --> Designing
Designing --> Deploying : Deploy Flow
Deploying --> Running : Success
Deploying --> Error : Failure
Running --> Monitoring : Health Check
Monitoring --> Healing : Failure Detected
Healing --> Running : Remediated
Healing --> Error : Unrecoverable
Error --> [*]
@enduml
```

---

## 6. Sequence Diagram: Live Collaboration

```plantuml
@startuml
actor User1
actor User2
participant IDE as "Visual IDE"
participant Server as "Collab Server"
User1 -> IDE : Edit Flow
IDE -> Server : Sync Change
Server -> IDE : Broadcast Change
User2 -> IDE : Receives Update
@enduml
```

---

## 7. Deployment Diagram

```plantuml
@startuml
node "Cloud" {
  component "Kubernetes Cluster" {
    component "AGCP Core"
    component "API Gateway"
    component "Monitoring Dashboard"
  }
}
node "Edge Node" {
  component "Self-Healing Agent"
  component "Flow Runtime"
}
node "User Device" {
  component "Visual IDE"
}
@enduml
```

---

## 8. Runtime Diagram: Self-Healing & Monitoring

```plantuml
@startuml
actor Admin
participant "Visual IDE" as IDE
participant "Self-Healing Agent" as Agent
participant "Monitoring Dashboard" as Mon
Admin -> IDE : View Dashboard
IDE -> Mon : Request Status
Mon -> Agent : Poll Health
Agent -> Mon : Health/Incident Report
Mon -> IDE : Update Dashboard
@enduml
```

---

# End of PlantUML Diagrams
