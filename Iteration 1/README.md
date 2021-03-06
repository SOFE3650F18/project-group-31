| Category                        | Details                                                      |
| ------------------------------- | ------------------------------------------------------------ |
| Design Purpose                  | This is a greenfield system from a mature domain. The purpose is to produce a sufficiently detailed design to support construction of the system. |
| Primary functional requirements | From the use cases in Deliverable 1, the primary ones are as follows:<br>**UC1:** Because it supports the core business.<br/>**UC2:** Because it supports the core business.<br/>**UC3:** Because it supports the core business.<br/>**UC6:** Because it supports the core business.<br/>**UC9:** Because it supports the core business.<br/>**UC11:** Because it supports the core business.<br/>**UC12:** Because it supports the core business.<br/>**UC17:** Because of technical issues associated with the CMS. |
| Quality Attribute Scenarios     | The scenarios were mentioned in the first deliverable, and will be prioritized as below:</br><table><tr><th>Scenario ID</th><th>Importance to Customer</th><th>Difficulty of Implemention</th></tr><tr><td>QA 1</td><td>High</td><td>High</td></tr><tr><td>QA 2</td><td>High</td><td>Low</td></tr><tr><td>QA 3</td><td>High</td><td>Medium</td></tr><tr><td>QA 4</td><td>High</td><td>Low</td></tr><tr><td>QA 5</td><td>Low</td><td>Low</td></tr><tr><td>QA 6</td><td>High</td><td>High</td></tr><tr><td>QA 7</td><td>Medium</td><td>High</td></tr><tr><td>QA 8</td><td>Medium</td><td>High</td></tr></table> |
| Constraints                     | All the constraints which are shown in Deliverable 1 are included as drivers. |
| Architectural Concerns          | All of the architectural concerns as shown in Deliverable 1 are included as drivers. They form the basis for the iteration goals. |

# Iteration 1
### Step 2: Establish a goal 
The goal of this iteration is to achieve architectural concern CNR-1 of establishing overall system architecture.

### Step 3: Choose 1 or more elements of the system to refine
We will be refining the backend of the CMS system. 

### Step 4: Choose one or more design concepts that satisfy the selected drivers
| Design Decisions                                             | Rationale                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Three-tier-deployment pattern                                | Since the users are required to use a web browser to use the system CON-1 and database is required to store and update data CON-5, three-tier-deployment is suitable.<br><br>Discarded Alternatives: <br><table><tr><th>Alternative</th><th>Reason for Discarding</th></tr><tr><td>Layered Pattern</td><td>A layered architectural pattern is best suitable for separating components of a system and each layer provides support to next layer. This design fails to address any of our constraints. </td></tr></table> |
| The system tier (server-side) will communicate with the database tier using  PostgreSQL | PostgreSQL offers an easy backup solution, as well as many security features including concurrent user encryption and sanitized inputs which can prevent unauthorized access. This design decision helps satisfy QA1, QA-8, CON4, CON-2, CON-3, and CON-5. |
| The system layer (server-side) will communicate with the client tier via a REST API reference design | This offers extensibility, security and can easily transmit authentication tokens. Additionally, this helps satisfy CON-1 by enabling the client tier to access data, while not forcing the use of a Standard Web Application (wherein only static pages are generated, like with PHP). <br><br>Discarded Alternatives:<br><table><tr><th>Alternative</th><th>Rationale for Discarding</th></tr><tr><td>PHP</td><td>The use of PHP would force us to adopt the Web Application Reference Architecture for the front-end, which would mean we cannot satisfy QA-2 and QA-3.</td></tr></table> |
| The system layer will be written using Node.js | This offers easy extensibility, good integration with JSON-based REST and CRUD API’s (a result of a previous decision process), and the asynchronicity helps satisfy the need for many concurrent users (CON-3). Lastly, because node runs on Google’s V12 JavaScript engine, access to system clocks are found within the server, removing the need for a clock component.<br><br>Discarded Alternatives:<br><table><tr><th>Alternative</th><th>Rationale for Discarding</th></tr><tr><td>.Net</td><td>.Net was discarded due to its inability to natively handle JSON objects (json handlers are a component and therefore require packaged libraries to handle such objects. </td></tr><tr><td>Java</td><td>Java offers useful features, but implementing non-blocking IO (supporting multiple users) is more expensive. </td></tr></table>

### Step 5: Instantiate architectural elements, allocate responsibilities and define interfaces

| Design Decision (Element + Responsibility)                   | Rationale                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| The system tier (server-layer) will utilize Express.js middleware for handling asynchronous I/O, and to create a REST API interface. | Express middleware offers various functionalities which are required to create a connection to PostgreSQL database CON-5. |
| The system tier will use promise/await structure instead of callbacks. | The usage of asynchronous function allows us to support over 5000 simultaneous connection and thus addressing CON-3. |
| The system tier will utilize Node-Postgres as the handler for PostgreSQL database connection. | The handler is used to create a connection from the server to the Postgres database server CON-5. |

### Step 6: Sketch views and record design decisions

![](img1.png)

### Step 7: Perform analysis of current design and review iteration goal and design objectives

![](img2.png)