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

