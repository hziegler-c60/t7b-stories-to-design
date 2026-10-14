# T7B Design — Card 2: View an Incident

**Group members and roles:**
- Diagrammer: Jordan
- Contract Writer: Andre
- Story Checker: Hannah
- Presenter: Myia

## User story
As an IT Branch Operations Support Lead, I want to open an incident and see its details and current status so that I can decide who should handle it

## Story breakdown
- **Inputs:** Click into incidents
- **Process:** runs acess check, Populates incident details and current status
- **Outputs (success):** Returns proper incident data
- **Outputs (failure):** Returns error no acees grsnted message
- **Interface:** `GET /incidents/{id}`

## Workflow diagram

```mermaid
flowchart LR
    U[User selects incident]
    S[Incident detail screen]
    A["GET /incidents/{id}"]
    D[(Incident database)]
    Q{Incident found?}
    OK[Display incident details]
    ERR["403: Forbidden"]
 
    U --> S
    S --> A
    A --> D
    D --> Q
    Q -->|Yes| OK
    Q -->|No| ERR
    ERR --> S

 ## Component diagram

```mermaid
flowchart LR
    U["Medline Staff"]
    FE["React Frontend - Incident View"]
    API["Backend API - GET /incidents/{id}"]
    DB[("Incident Database")]
 
    U -->|"Select incident"| FE
    FE -->|"GET /incidents/{id}"| API
    API -->|"Find matching incident"| DB
    DB -->|"Record or no match"| API
    API -->|"200 OK:Incident JSON / 404: Not found"| FE
    FE -->|"Display result"| U    

## Contract
See `schema.json`.

## Traceability
| Story phrase | Where it shows up in the design |
| --- | --- |
| "Display Incident Details" | Used to click into the incident details  |
| "Incident Details" | Success Path: redirect |
| "403: Forbidden" | 403 error, used denied access |

## What we changed after feedback
- ___ because ___
