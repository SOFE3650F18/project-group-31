# Iteration 3
### Step 2: Establish a goal 
The goal of this iteration to realize architectural concern CNR-3, of establishing a secure database logic and implementing security features.

- QA-1(Security)
- QA-5 (Performance)
- QA-6 (Security)
- QA-8 (Scalability)
- QA-9 (Maintainability)
- CON-2
- CON-3
- CON-4
- CON-5
- CNR-3

### Step 3: Choose 1 or more elements of the system to decompose
We will be refining the database tier and the security components of the CMS System (back-end).

### Step 4: Choose one or more design concepts that satisfy the selected drivers

| Design Decisions                                             | Rationale                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| To prevent direct access to the database, we will be using a **3-tier architecture**, thereby separating the user from the database with an API layer that supports JWT Authentication | In previous iterations, this decision supported usability. It also enhances security by making it easy to prevent users from using malicious queries to directly address the database, thereby addressing QA-1, QA-6 and QA-5. This is because the login system is able to ensure only authorized persons have access to certain parts of the web application. This also sufficiently completes CON-5. This also provides the benefits of a **Distributed Deployment System** (Cervantes) |
| The **Database Tier** of the application will use **PostgreSQL** and users, backup tables and simultaneous access will be enabled | By enabling backup, we can address UC17, QA-9, and CON-4. Additionally, by enabling simultaneous access, we can allow more than 5000 users to be supported at once, thereby CON-3 is addressed. Additionally, because a relational-data model was required, this also addresses CON-5. |
| A distributed **Load-balanced cluster** is utilized to access the database simultaneously, and database clusters are used in RAID 10 to ensure quick, secure data and removes many data limitations | This design decision fully addressed CON-2 and CON-3, as it can now sufficiently handle large amounts of users. Additionally, large amounts of data can now be stored, as storage space is not sacrificed for redundancy in a design involving a distributed array of storage solutions. This decision also fully enables QA-8, as new clusters can be added to ensure more data. Lastly, QA-9 is also fully addressed here, as data backups can be taken. |
| Security tactics (Cervantes) are implemented to detect Denial of service attacks and intrusion, as well as identify actors. | This design decision fully addresses QA-4, by preventing downtime from attacks. |
