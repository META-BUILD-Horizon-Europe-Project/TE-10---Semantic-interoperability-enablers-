## **General Information and Purpose**

**TE ID & Name:** TE-10 - Semantic interoperability enablers for energy management, flexibility planning and effective RES assets integration (Interoperability Framework for META-BUILD Services)

**Description and purpose:** TE-10 provides the **semantic interoperability backbone** of META-BUILD, enabling **secure, standardised and scalable data exchange** across pilots, assets and WP4 services. Its purpose is to ensure that heterogeneous systems — including BMS/EMS platforms, IoT devices, heat pumps, PV/PVT systems, batteries, digital twins, optimisation services and maintenance services — exchange information through a **shared semantic layer**, rather than through bespoke point-to-point integrations.

The framework follows a **semantic-light approach**, based on a **minimal canonical NGSI-LD information model**. NGSI-LD is an ETSI standard for context information management that allows entities, relationships and attributes to be exchanged through **JSON-LD APIs**. The model captures the core concepts shared across the Front Runners while remaining intentionally lean, supporting rapid **Proof-of-Concept integration in D4.2** and progressive refinement in **D4.3**.

TE-10 therefore provides a **canonical data model** for key building, zone, asset, measurement, forecast and event concepts; **pilot-specific mappings** from native data formats to canonical entities; **standardised JSON-LD / NGSI-LD interface profiles**; **metadata, lineage and profiling rules**; and **secure access, governance and interoperability mechanisms**. TE-10 acts as the **integration backbone for WP4** and supports the interaction of all relevant digital services, including **TE-12, TE-13, TE-14, TE-15 and TE-16**.

**Lead partner/Contact Information:**

- Lead (TE-10): **European Dynamics (ED)**.
- Contributing partners: **Blueprint, ICCS, IDM, INETUM, INETUMES, CARTIF, EURAC, TECNALIA**.

**Target Front Runners/Pilots:** **All 6 Front Runners**, with early mapping examples and PoC alignment currently focused on **FR1 - Austria** and **FR4 - Greece**.

**Architecture Diagram:**
![Model](methodology.png)

In practical terms, TE-10 sits between **data producers** and **service consumers** and enables both **near-real-time** and **batch context exchange** through a shared semantic layer built around a **Context Broker** and **pilot-specific adapters**. It is structured as a layered interoperability framework composed of:

1. **Data Sources / Producers**
   - Building Management Systems (BMS)
   - Energy Management Systems (EMS)
   - IoT sensors and meters
   - Decarbonisation technologies (HP, PV/PVT, batteries, storage)
   - External sources (weather, tariffs, price signals)
   - WP4 Technology Enablers producing derived data (forecasts, KPIs, maintenance indicators, DT state)

2. **Pilot-Specific Adapters / Connectors**
   - Data translators that convert native pilot formats and proprietary interfaces into the canonical TE-10 representation
   - Protocol handling for REST, MQTT, Modbus, BACnet, OPC-UA, and file-based exchange (CSV/JSON)

3. **Interoperability Core**
   - NGSI-LD Context Broker
   - Canonical entity catalogue
   - Semantic mappings
   - Metadata and schema management
   - Context management
   - Data profiling, lineage and curation

4. **Security and Governance Layer**
   - Authentication
   - Authorisation
   - Attribute-Based Access Control (ABAC)
   - Encryption
   - Pseudonymisation / anonymisation
   - Audit and provenance support

5. **Data Consumers / Services**
   - TE-12 co-designed value-added services
   - TE-13 MPC
   - TE-14 flexibility / DR services
   - TE-15 predictive maintenance
   - TE-16 digital twin
   - Dashboards, KPI services and reporting tools

## **Functional Requirements**

Describe the core capabilities of the TE and the functions it provides.  
Focus on what the TE does, not how it is implemented.

- **Canonical Semantic Modelling:** Define and maintain a minimal canonical NGSI-LD information model for META-BUILD and harmonise the representation of buildings, zones, assets, measurements, forecasts, events and derived indicators.
- **Data Ingestion & Transformation:** Ingest near-real-time and historical data from heterogeneous pilot systems, translate native formats into canonical entities using pilot-specific adapters, and support protocol conversion and data normalisation.
- **Semantic Mapping & Context Management:** Map pilot-specific concepts to shared entity types and attributes, maintain explicit links between entities using NGSI-LD relationships, and support contextual queries and subscriptions.
- **Service Interoperability:** Enable data exchange between WP4 services through common schemas and APIs and support planning, monitoring, Digital Twin ingestion, flexibility and maintenance use cases.
- **Metadata, Lineage & Profiling:** Track provenance, source and transformation logic of exchanged data and support metadata such as `unitCode`, `observedAt`, `providedBy`, `computedBy` and `datasetId`.
- **Secure Data Sharing:** Enforce secure communication, access control and privacy-aware exchange policies across services and pilots.

## **Non-Functional Requirements**

- **Performance:**
  - Supports **near-real-time data exchange** for operational services.
  - Supports **batch and historical data onboarding**.
  - Operates with **lightweight semantic overhead** suitable for pilot-scale PoC deployment.
- **Scalability:**
  - Supports **multiple pilots, buildings and services**.
  - Supports extension of the canonical model with **optional properties** and **pilot-specific sub-typing**.
- **Reliability and Availability:**
  - Supports **fault-tolerant ingestion and message handling**.
  - Allows **delayed or replayed ingestion** for historical datasets.
  - Supports **graceful degradation** under partial data availability.
- **Security (authentication, authorisation, data encryption, data privacy):**
  - **Authentication:** Token-based secure access to interoperability services and APIs.
  - **Authorisation:** Attribute-Based Access Control (**ABAC**) and service-level access policies.
  - **Encryption:** **TLS-secured communication** for data exchange.
  - **Privacy:** GDPR-aligned handling of technical and operational building data, with pseudonymisation where user-related data is involved.

## **Service Interfaces**

#### **Interface Types**

- **NGSI-LD REST APIs**
- **REST-based integration endpoints**
- **Event-driven subscriptions / notifications**
- **Adapter-level ingestion interfaces** for pilot systems
- **Optional message-broker based event distribution** for asynchronous service communication

#### **Supported Data Formats**

- **JSON**
- **JSON-LD**
- **NGSI-LD entity payloads**
- **CSV / file-based imports** (through adapters)

#### **Main Interaction Patterns**

- **Publish / upsert context entities**
- **Query current entity state**
- **Query historical time-series or batches**
- **Subscribe to entity changes or event notifications**
- **Exchange forecast, flexibility, DT-ingestion and monitoring payloads**

#### **API Endpoints**

For each exposed endpoint:

- Request Parameters
- Request Example
- Response Parameters
- Response Example
- Error Handling

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 1</strong></p></th><th><p><strong>Upsert / Update Context Entity</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/ngsi-ld/v1/entities/{entityId}/attrs</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>PATCH / POST</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Creates or updates attributes of an NGSI-LD entity in the interoperability layer. Used by pilot adapters and service producers to publish harmonised context data.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Content-Type: application/ld+json</li><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>entityId (path, required): Target NGSI-LD entity identifier</li><li>body (object, required): One or more NGSI-LD attributes expressed as Properties or Relationships</li><li>@context (array/string, optional): JSON-LD context definition</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"temperature": {<br>"type": "Property",<br>"value": 21.7,<br>"unitCode": "CEL",<br>"observedAt": "2026-01-12T13:40:00Z"<br>}<br>}</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>status (string): Operation status</li><li>entityId (string): Updated entity identifier</li><li>updated_attributes (array&lt;string&gt;): Names of updated attributes</li><li>timestamp (string): ISO 8601 timestamp of processing</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"status":"updated",<br>"entityId":"urn:ngsi-ld:ThermalZone:fr4-zone-01",<br>"updated_attributes":["temperature"],<br>"timestamp":"2026-01-12T13:40:01Z"<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":"ValidationError","message":"Invalid NGSI-LD payload"}</li><li>401 Unauthorized: {"error":"Unauthorized","message":"Invalid token"}</li><li>404 Not Found: {"error":"NotFound","message":"Entity does not exist"}</li><li>415 Unsupported Media Type: {"error":"UnsupportedMediaType","message":"Expected application/ld+json"}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 2</strong></p></th><th><p><strong>Retrieve Entity by ID</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/ngsi-ld/v1/entities/{entityId}</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns the latest available state of an entity, including its properties and relationships.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li><li>Accept: application/ld+json</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>entityId (path, required): NGSI-LD entity identifier</li><li>attrs (query, optional): Comma-separated list of requested attributes</li></ul></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>id (string): Entity identifier</li><li>type (string): Entity type</li><li>properties (object): Latest available properties</li><li>relationships (object): Linked entities and references</li><li>@context (array/string): Applied JSON-LD context</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"id":"urn:ngsi-ld:HeatPump:fr4-hp-01",<br>"type":"HeatPump",<br>"status":{"type":"Property","value":"on"},<br>"refBuilding":{"type":"Relationship","object":"urn:ngsi-ld:Building:fr4-bld-01"}<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>404 Not Found: {"error":"NotFound","message":"Entity not found"}</li><li>401 Unauthorized: {"error":"Unauthorized","message":"Invalid token"}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 3</strong></p></th><th><p><strong>Query Entities by Type / Filter</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/ngsi-ld/v1/entities</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns entities filtered by type, relationship or attribute constraints.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li><li>Accept: application/ld+json</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>type (string, optional): Entity type filter</li><li>q (string, optional): Attribute-based query filter</li><li>attrs (string, optional): Requested attributes</li><li>limit (int, optional): Maximum number of returned entities</li><li>offset (int, optional): Pagination offset</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>Example GET /ngsi-ld/v1/entities?type=ThermalZone&amp;q=refBuilding==urn:ngsi-ld:Building:fr4-bld-01</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>entities (array): Matching entity objects</li><li>count (int): Number of returned entities</li><li>limit (int): Applied page size</li><li>offset (int): Applied offset</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"entities":[<br>{"id":"urn:ngsi-ld:ThermalZone:fr4-zone-01","type":"ThermalZone"},<br>{"id":"urn:ngsi-ld:ThermalZone:fr4-zone-02","type":"ThermalZone"}<br>],<br>"count":2,<br>"limit":20,<br>"offset":0<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":"InvalidQuery","message":"Malformed query expression"}</li><li>401 Unauthorized: {"error":"Unauthorized","message":"Invalid token"}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 4</strong></p></th><th><p><strong>Subscribe to Context Changes</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/ngsi-ld/v1/subscriptions</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>POST</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Creates a subscription for receiving notifications when selected entity attributes change.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Content-Type: application/ld+json</li><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>type (string, required): Target entity type</li><li>watchedAttributes (array&lt;string&gt;, optional): Attributes to observe</li><li>notification (object, required): Endpoint and payload settings for notifications</li><li>q (string, optional): Query filter</li><li>expiresAt (string, optional): Subscription expiry time</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"type":"Subscription",<br>"entities":[{"type":"ThermalZone"}],<br>"watchedAttributes":["temperature"],<br>"notification":{"endpoint":{"uri":"https://service.example.com/notify","accept":"application/json"}}<br>}</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>subscription_id (string)</li><li>status (string)</li><li>message (string)</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"subscription_id":"urn:ngsi-ld:Subscription:te16-zone-temp",<br>"status":"created",<br>"message":"Subscription registered successfully."<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":"ValidationError","message":"Notification endpoint missing"}</li><li>401 Unauthorized: {"error":"Unauthorized","message":"Invalid token"}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 5</strong></p></th><th><p><strong>Publish Event / Forecast Entity</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/ngsi-ld/v1/entities</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>POST</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Publishes a new context entity such as an EnergyForecast, PriceSignal, DemandResponseEvent or KPI report entity. This endpoint is useful for exchanging forecasted or derived information between TEs.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Content-Type: application/ld+json</li><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>body (object, required): Full NGSI-LD entity payload</li><li>@context (array/string, optional): JSON-LD context definition</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"id":"urn:ngsi-ld:EnergyForecast:fr4-2026-01-13",<br>"type":"EnergyForecast",<br>"forecastFor":{"type":"Relationship","object":"urn:ngsi-ld:Building:fr4-bld-01"},<br>"targetDay":{"type":"Property","value":"2026-01-13"},<br>"predictedLoad":{"type":"Property","value":[12.1,11.8,10.9]}<br>}</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>entityId (string)</li><li>status (string)</li><li>timestamp (string)</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"entityId":"urn:ngsi-ld:EnergyForecast:fr4-2026-01-13",<br>"status":"created",<br>"timestamp":"2026-01-12T18:00:00Z"<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":"ValidationError","message":"Invalid entity payload"}</li><li>401 Unauthorized: {"error":"Unauthorized","message":"Invalid token"}</li><li>409 Conflict: {"error":"AlreadyExists","message":"Entity already exists"}</li></ul></td></tr></tbody></table></div>

#### **UI Mockups (if applicable)**

- **Context explorer view:** List of canonical entities by type (Building, ThermalZone, HeatPump, Battery, PVSystem, Forecast, Event) with current state, relationships and metadata.
- **Interoperability monitoring view:** Ingestion health, mapping status, latest updates, lineage metadata, active subscriptions and service-consumer activity.
- **Semantic mapping dashboard:** Native-to-canonical attribute mappings per pilot, schema version, completeness checks and validation flags.

## **Data Model**

- **Entities and relationships:**
  - **Building**(building_id) 1-N **ThermalZone**(zone_id)
  - **Building**(building_id) 1-N **Asset**(asset_id, type = HeatPump / Battery / PVSystem / SmartMeter / Sensor)
  - **Asset**(asset_id) 1-N **Measurement**(ts, observed properties)
  - **Asset**(asset_id) 1-N **Event**(event_id, type, severity, ts)
  - **Building / Asset / Service** 1-N **EnergyForecast**(forecast_id, target_day, values)
  - **Building / Asset / Service** 1-N **PriceSignal / DemandResponseEvent**(signal_id, validity, payload)
  - **Service Output** entities linked back to source entities using metadata and explicit NGSI-LD relationships

- **Common Property / Metadata Rules:**
  - Quantitative values use **`unitCode`**
  - Time-varying values use **`observedAt`**
  - Source values may use **`providedBy`**
  - Derived values may use **`computedBy`**
  - Dataset-level traceability may use **`datasetId`**
  - Relationships are modelled explicitly (e.g. **`refBuilding`**, **`refZone`**, **`servedBy`**, **`isPartOf`**)

- **Database / Context schema (logical):**
  - buildings: {building_id, name, location, metadata}
  - thermal_zones: {zone_id, building_id, name, geometry, metadata}
  - assets: {asset_id, building_id, zone_id, type, model, capacity, metadata}
  - measurements: {entity_id, ts, attribute, value, unitCode, observedAt, providedBy}
  - forecasts: {forecast_id, target_entity, target_day, values, computedBy, datasetId}
  - events: {event_id, entity_id, type, severity, ts, source}
  - subscriptions: {subscription_id, entity_filter, watched_attributes, endpoint, created_at}
  - lineage_registry: {dataset_id, source_ref, mapping_version, schema_version, timestamps}

## **Data Requirements**

| Data Category | Data Description | Source Type | Temporal Granularity | Spatial Scope | Historical Depth | Access Mode |
| --- | --- | --- | --- | --- | --- | --- |
| Asset Metadata | Static information describing building assets, systems and devices (type, model, capacity, identifiers, location, ownership context) | Asset registry / BIM / BMS / partner inputs | On change | Building / Zone / Asset | Full history | Read-only |
| Sensor Measurements | Real-time and historical measurements from sensors and meters (temperature, humidity, power, flow, voltage, CO₂, etc.) | Sensors / BMS / EMS / meters | Preferred: 1-15 min; worst case: 1 h | Zone / Asset / Building | 3-12 months where available | Read-only |
| Equipment Telemetry | Operational data from controllable assets (HP states, battery status, PV production, alarms, modes) | OEM APIs / EMS / BMS / device gateways | Preferred: 1-15 min; worst case: 1 h | Asset / Building | 3-12 months where available | Read-only |
| Events and Alerts | Faults, alarms, warnings, service events | BMS / EMS / TE services / event broker | Event-based | Asset / Building / Service | As available | Read-only |
| Weather Data | Outdoor temperature, humidity, solar irradiance, wind and related variables | External weather service / local weather station | Preferred: 15 min; worst case: 1 h | Site / Region | 12 months plus forecast horizon | Read-only |
| Tariff / Market Signals | Electricity prices, tariff periods, flexibility signals, DR-related values | Market API / supplier API / DR service | Preferred: 15 min; worst case: 1 h | Building / Supplier / Region | 12 months where available | Read-only |
| Forecast Data | Demand forecasts, flexibility forecasts, PV forecasts, weather forecasts | TE services / forecasting tools / external APIs | Preferred: 15 min; worst case: 1 h | Asset / Building / Site | Forecast horizon + historical archive where available | Read-only |
| User Preferences / Service Parameters | Comfort settings, operating preferences, optional policy/configuration values | Dashboard / application / service configuration | On change | User / Building / Zone | Not required | Read-write |
| Control / Service Outputs | Set-points, schedules, mode changes, command requests, service recommendations | Control platform / HEMS / optimisation services | Event-based | Asset / Zone / Building | Not applicable | Read-write |
| KPI / Analytics Outputs | Derived indicators such as savings, health indicators, compliance values, flexibility indicators | TE services / analytics engines | Event-based / periodic | Asset / Building / Service | As generated | Read-only |
| Metadata / Provenance | Lineage, schema version, timestamps, source references, mapping information, quality flags | TE-10 interoperability core | On ingestion / on update | Dataset / Asset / Service | Full history | Read-only |

## **Integration and Dependencies**

- **External dependencies:** Pilot-side system APIs and interfaces; external weather, tariff and market signal providers where relevant.
- **System dependencies:** Pilot-specific adapters/connectors; NGSI-LD Context Broker; metadata and schema management components.
- **Third-party integrations:** BMS, EMS, IoT gateways, OEM APIs, BIM/asset registries, file-based partner datasets, optional message brokers.
- **Edge/Cloud integration:** TE-10 can bridge edge and cloud systems through adapters, REST APIs, event subscriptions and optional asynchronous messaging.
- **Data space integration:** TE-10 provides the shared semantic layer through which TE-11, TE-12, TE-13, TE-14, TE-15 and TE-16 can consistently exchange and reuse data.

**Dependencies:**

- Pilot-side data availability and interface access
- Pilot-specific adapter implementation
- Availability of source metadata from WP3 / WP5
- Coordination with service providers consuming TE-10 outputs

**Replication logic:**

A new pilot or replication site can adopt TE-10 by:

- Mapping local devices / APIs to the canonical entities and attributes
- Implementing a simple **NGSI-LD client / adapter**
- Consuming standardised queries and subscriptions from the broker

## **Security and Privacy**

- **Data Sensitivity:** Mainly technical and operational building data, including telemetry, events, forecasts, service outputs and metadata/provenance records.
- **Access Control:** Authentication and authorisation policies with **ABAC** for fine-grained interoperability access.
- **Encryption:** **TLS-secured communication** for data exchange between producers, interoperability core and consumers.
- **Privacy:** Pseudonymisation where user-related data is involved, data minimisation and GDPR-compliant handling of operational and service-level data.
- **Audit Logs:** Audit logging and provenance support preserve traceability of exchanged information, mappings, schema versions and update history across services.

## **Current Status**

This section summarises the current maturity of TE-10 as an interoperability framework at the **D4.2 stage**, focusing on the transition from conceptual design to a **PoC-oriented semantic interoperability baseline**.

**Progress achieved:**

- Definition of a **minimal canonical NGSI-LD model**
- Definition of **semantic-light design principles**
- Initial **mapping examples for FR1 and FR4**
- Definition of three priority interface profiles:
  - **DR Forecast**
  - **Digital Twin Context Ingestion**
  - **Heat Pump / Flexibility Monitoring**
- Definition of **lightweight metadata and governance rules**
- Early **replication-readiness considerations**

**Validation status:**

- PoC-oriented and **partially validated** through architectural design, semantic mapping exercises and early integration planning.
- Intended to support **early cross-TE integration in D4.2**.
- Further implementation, pilot refinement and validation expected in **D4.3**.

**Current limitations:**

- Not all pilots have **complete or stable data access** yet.
- Some mappings remain to be **confirmed during pilot implementation**.
- **Context broker deployment** and **adapter realisation** are still evolving.
