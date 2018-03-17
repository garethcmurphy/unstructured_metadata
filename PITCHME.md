
### Managing Unstructured Metadata at ESS

Gareth Murphy, European Spallation Source

Helmholtz-Zentrum Berlin
2018-03-19

---

### What is metadata?

- a set of data that describes and gives information about other data.
- Can classify into separate types
- administrative
- structural
- descriptive

---

### SCIENTIFIC METADATA

- more extensive 
- less predictable 
- "unknown unknowns"
- units need to be included 

---

### Existing tools

- performance and flexibility issues 
- SQL database technology aging
- nosql offers more opportunities for unstructured data 


---
### Metadata at ESS


- Scientific data is complex
- Not always predictable what is important
- Keep all data and make it easy to search for important features?
- Most scientific data is unFAIR
- Findable, Accessible, Interoperable, Reproducible


---

### Currently metadata can be stored

- In filename (run1_vanadium) - not scalable
- In Excel files - not accessible
- Not at all

---

### Using a data catalogue

- One source of information
- All data can be found through this
- Manages permissions, publication
- User reads a publication, can get data from catalogue

---

### SciCat


- Manage the meta data of raw and derived data which is taken at
experiment facilities
- Meta data
- administrative : data management lifecycle, ownership, filecatalog
- scientific: describing the sample, beamline and experiment
parameters relevant for the users data analysis
---

### SciCat
- Enables management of the lifecycle of the data from creation ,
data analysis and eventual deletion
- Data can be linked to proposals and samples
- Data can be linked to publications (DOI, PID)
- Data can be migrated to and from longterm storage on tape

---

### SciCat
- Reproducibility- Helps keeping track of data provenance (i.e. the steps leading to
the final results)
- Allows checking scientific integrity (checksum of data)
- Finadbility - Allows find data based on the meta data (your own data and
other peoples public data)
- In the long term:help to automate standardized analysis workflow
---


### SciCat - collection of microservices
- Web frontend (catanie - [angular](http://angular.io) based)
- API service backend (catamel- Automatically generated using IBM's [loopback.io](http://loopback.io)
- Database [MongoDB](https://www.mongodb.com/)
- Message/job queuing system (currently RabbitMQ -> migrating to [Kafka](http://kafka.apache.org))
- Flow-based editor [Node-RED](https://nodered.org/)

---

### SciCat architecture

![scicat](assets/SciCat.png)

---

### Kubernetes Deployment

- Can test kubernetes deployment using minikube, wihout installing a full cluster
- Try it yourself!
- Working minikube config at http://www.github.com/ScicatProject/localdeploy
- RBAC disabled by default - can re-enable


---

### Kubernetes architecture

![kube](assets/kube_arch.png)


---

## Kubernetes

- Applications are deployed to "pods", which are made available using services, which are accessed using ingress
- For each of the 5+ services we need to configure:
    1. Deployments
    2. Services
    3. Pods (can be groups of containers, we typically use single containers)
    4. Ingress
- for each of 5 microservices, 4 configurations = 20 config files




### MongoDB

- NoSQL storage of metadata, login, jobs
- Database requires persistent storage
- Currently we store on k8s nodes, not a longterm solution



---

### Catanie

- Angular website
- Javascript generated static html
- Data served by catamel
- Viewable on PC, phone etc

---

### Catanie
![catanie](assets/catanie2.png)


---

### Node-RED

- Translate metadata from Kafka stream XML to catamel format (JSON)
- Can be used to add in extra data cleaning  or processing


---

### Node-RED

![nodered](assets/nodered.png)

---

### Catamel

- Metadata server
- Loopback generated API
- Models defined in JSON
- Also provides connectivity to authentication server(s)


---

### Catamel

![catamel](assets/catamel.png)

---

### Dashboard Overview

![kube1](assets/overview.png)
---

### Pods Overview

![kube2](assets/pods.png)
---

###  Pod CPU & Memory

![kube3](assets/kuberabbit.png)


---

### Deployment of scicat

- still outstanding:
- persistent storage
- file viewer
- data download

---

## Conclusion

- SciCat on Kubernetes will be able to provide metadata services for ESS users needs
