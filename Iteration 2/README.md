### Step 2: Establish a goal 

The goal of this iteration is to achieve architectural concern CNR-2. This will involve designing the front-end of the system. Related artifacts are chosen as the drivers,even though all Quality Attributes, Use Cases and Concerns should be taken into consideration.Namely, the following are going to be focused on:

- QA-2 (Usability)
- QA-3 (Performance)
- QA-6 (Security)
- QA-7 (Interoperability)
- CNR-2
- CON-1
- CON-2

### Step 3: Choose 1 or more elements of the system to decompose

This is a specific development effort for the client-side module of the deployable application. As such, the element to refine is the Client-Side Application (or the front-end). Refinement is performed through decomposition.


### Step 4: Choose one or more design concepts that satisfy the selected drivers

| Design Decisions and Location                                | Rationale                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Logically Structure Client part of system using the Rich Internet Applications Reference Architecture | The Rich Internet Application (RIA) supports the development of dynamic or static client-side web pages that can be rendered in a browser. As such, constraint CON-1 is satisfied. Additionally, through the use of web sessions  QA-6 is satisfied. QA-2 and QA-3 are satisfied through the use of dynamic menus. Lastly, QA-6 can be satisfied, as JavaScript can be used to generate and export google/apple calendar importable files.<br/>Discarded Alternatives:<table><tr><th>Alternative</th><th>Reason for Discarding</th></tr><tr><td>Rich Client Applications</td><td>Rich Client Applications (RCAs) are similar to RIAs, but they fail to satisfy CON-1, as they are run as OS platform applications </td></tr><br/><tr><td>Web Applications</td><td>Rendering things server side fail to meet QA-2 and QA-3 requirements, as static web pages may require multiple navigations to get new data.</td></tr><tr><td>Mobile Applications</td><td>A mobile application would fail to meet QA-2 and QA-3, as the size constraints would ultimately result in hidden menus and modals. Additionally, mobile and handheld devices were not considered for accessing the system (as most project submissions and long-tasks require more powerful devices, anyway)</td></tr></table> |
| Structure the logic of the client-side application to use an MVC pattern | For an RIA, implementing the MVC framework would generally involve using DOM manipulation and event listeners as controllers, a JavaScript program as a model (which uses AJAX and HTTP requests), and the view would be the rendered html document. This further satisfies QA-2, as it would reduce the requirement to navigate to different pages to access data, as data can be dynamically loaded into view from model once attained asynchronously via AJAX requests. |
| Build the user-interface of the client application using Angular | One of two standard framework for front-end rich browser based applications, angular enables the use of Token Authentication (to satisfy QA-6, i.e. Security )  <br/>Alternatives were considered, and were discarded for the below reasons<table><tr><th>Alternative</th><th>Rationale for Discarding</th></tr><tr><td>React</td><td>React does not have the application structure enforcement that Angular does, nor does it comply to the level of security that Angular provides. It fails QA-6, and therefore is discarded.</td></tr><tr><td>Plain JavaScript</td><td>Security gaps would be far more difficult to analyze for an entirely custom application, while little benefit would be provided. Discarded for high development costs.</td></tr></table> |


### Step 5: Instantiate architectural elements, allocate responsibilities and define interfaces

*The services referenced below are actually Angular services. In architectural terms, they resemble components, and not services. 

| Design Decision                                              | Rationale                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| A single JavaScript-based HTTP Service* is used for all communication to the server. Additionally, a single Service* is also used to hold all of the relevant data. | Since the data is refreshed all together, and all data is 2-way bound between the view and the model, having intermediary services (which are components). This helps to maintain security and performance, helping satisfy QA-2, QA-3, and QA-6. |
| No data is stored locally, except for session variables and authorization tokens. This is handled by the **AngularStorage** module | Because the web application is relatively quick, and for security purposes, data that requested and received via the HTTP service is never stored on the user’s machine. However, security tokens for logging in are. This helps to satisfy QA-6 and QA-1 |
| A single page is rendered, and what can be accessed is additionally restricted by a *Service module that handles authorization and encryption called the **authService** component | This will help ensure that QA-1 is satisfied, by restricting access to pages that the user does not have access to. Even if the server-side application does not serve any information to unauthorized users, the structure of the frontend may still provide hints towards possible security flaws. |
| The DomManipulation module interfaces with the independent modules for each user to change the browser render | This will ensure that QA-2 and QA-3 are realized. Alternative is to hardcode these behaviors, but they are less secure and are far more expensive to implement. |
| The Student, Lecturer and Administration modules are implemented with views and logic manipulators for each user respectively. They are responsible interfacing with the DomManipulation module that renders the html, and will implement some basic business logic. | This addresses all of the use cases with the exception of UC17 and UC18, which are largely implemented in the previous iteration. |


### Step 6: Sketch views and record design decisions

Elements within the front-end package are decided upon below. While they conform to Angular 6 component or service definitions, components that are packaged as part of angular are also included if they are relevant to the selected drivers.

While the Business (Server) Layer is not part of the MVC structure of the front-end, it is included to provide insight on the interfaces that are required by the httpService component.

![https://github.com/SOFE3650F18/project-group-31/blob/master/Iteration%202/Iteration2Diagram.png?raw=true](https://github.com/SOFE3650F18/project-group-31/blob/master/Iteration%202/Iteration2Diagram.png?raw=true)
