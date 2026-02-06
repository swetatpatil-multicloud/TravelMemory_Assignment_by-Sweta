# Travel Memory

Horizontal scalability for both frontend and backend layers
High availability through health checks and automatic traffic rerouting
.env file to work with the backend after creating a database in mongodb:

```
MONGO_URI='mongodb+srv://Swetatpatil:Rudyredindian2507@Swetapatil.nlqpeax.mongodb.net/?appName=Swetapatil'
PORT=3001
```
Data format to be added: 

```json
{
    "tripName": "Road Trip to Karnataka",
    "startDateOfJourney": "24-12-2025",
    "endDateOfJourney": "02-01-2026",
    "nameOfHotels":"Club Mahindra",
    "placesVisited":"Mysore, Humpi, Otty, Coorg",
    "totalCost": 60000,
    "tripType": "backpacking",
    "experience": "awesome and peaceful experience",
    "image": "https://www.bing.com/images/search?q=virupaksha+temple+hampi&form=HDRSC3&first=1",
    "shortDescription":"Road Trips are the best choice, its one of my best trip.",
    "featured": true
}
```
REACT_APP_BACKEND_URL=http://localhost:3001

### Travel Memory

## Deployment Architecture Diagram – Explanation

The Travel Memory application is deployed using a scalable and highly available cloud architecture on Amazon Web Services (AWS). The application follows a three-tier architecture consisting of the presentation layer (frontend), application layer (backend), and data layer (database). The diagram illustrates how user requests flow securely through each component.

<img width="590" height="884" alt="tv1 drawio(2)" src="https://github.com/user-attachments/assets/7db799cc-5bce-4cdf-9fef-13238a979c58" />



### 1. User (Client Layer)
The user accesses the Travel Memory application through a web browser using a domain name swetamulticloud.xyz or www.swetamulticloud.xyz.
  Protocol: HTTPS
  Port: 443
  Role: Initiates requests to view the application and interact with backend APIs.
All user requests are encrypted using HTTPS to ensure secure communication.

### 2. Cloudflare DNS and Security Layer
Cloudflare acts as the DNS provider and security gateway for the application.
  Responsibilities:
    Resolves domain names (graphtech.live and api.graphtech.live)
    Provides SSL/TLS encryption
    Protects the application from DDoS attacks
    Improves performance through caching and CDN
  Traffic Flow:
    Incoming HTTPS requests from users are forwarded to the AWS Application Load Balancer.
### 3. Application Load Balancer (ALB)
An AWS Application Load Balancer is used to distribute incoming traffic efficiently across multiple EC2 instances.
  Listener Configuration:
    HTTP (Port 80)
    HTTPS (Port 443)
  Routing Rules:
    Requests with path /api/* are routed to the Backend Target Group
    All other requests (/*) are routed to the Frontend Target Group
This routing mechanism enables frontend and backend services to operate independently while sharing a single load balancer.
### 4. Frontend Target Group
The frontend target group contains multiple EC2 instances hosting the React application.
  Configuration:
  Protocol: HTTP
  Port: 80
  Health Check Path: /
The load balancer continuously monitors the health of frontend instances and routes traffic only to healthy targets.
### 5. Frontend EC2 Instances (Presentation Layer)
Multiple EC2 instances are deployed to serve the frontend application.
  Components:
    React (build version)
    Nginx web server
  Responsibilities:
    Serve static frontend content
    Handle client-side routing using React
    Respond to user requests routed by the load balancer
    This setup ensures high availability and scalability of the frontend layer.
### 6. Backend Target Group
The backend target group contains EC2 instances running the Node.js API.
  Configuration:
    Protocol: HTTP
    Port: 80
    Health Check Path: /health
  The health check endpoint ensures that only healthy backend instances receive traffic.
### 7. Backend EC2 Instances (Application Layer)
Multiple EC2 instances are deployed to run the backend services.
  Components:
    Node.js with Express framework
    PM2 process manager
    Nginx reverse proxy
  Internal Communication:
    Nginx listens on port 80 and forwards requests to Node.js running on port 3000
  Responsibilities:
    Handle API requests
    Authenticate users
    Communicate with the database
    Process business logic
    Backend instances are not publicly exposed, enhancing security.
### 8. MongoDB Atlas (Data Layer)
MongoDB Atlas is used as a managed NoSQL database service.
  Configuration:
     Protocol: TCP
     Port: 27017
  Responsibilities:
     Store application data such as user information and travel memories
     Provide secure and scalable data storage
     Only backend EC2 instances are allowed to communicate with MongoDB Atlas, ensuring data security.
### 9. End-to-End Traffic Flow Summary
The user sends an HTTPS request via a web browser.
Cloudflare resolves the domain name and forwards the request securely.
The Application Load Balancer receives the request.
Based on routing rules:
  Frontend requests are sent to frontend EC2 instances.
  API requests are sent to backend EC2 instances.
  Backend services interact with MongoDB Atlas to fetch or store data.
  Responses are sent back to the user through the same secure path.
### 10. Security and Scalability Highlights
HTTPS encryption using Cloudflare SSL
Load balancing across multiple EC2 instances
Backend servers are not publicly accessible
Secure database connectivity

### EC2 Instances:
<img width="940" height="224" alt="image" src="https://github.com/user-attachments/assets/c89a273d-3c6e-4b23-bc0a-eb333a432a98" />


### Security group:
<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/e70e6c6c-ccec-4b2d-a943-d91d6145914e" />


### Load Balancer:
<img width="940" height="399" alt="image" src="https://github.com/user-attachments/assets/7a4d2830-5fcd-470b-a0bf-78fb61dd72c8" />

### Target Group:
<img width="940" height="437" alt="image" src="https://github.com/user-attachments/assets/1fcde033-2316-4a2a-9ec0-bf139d9edbf9" />

### VPC Dashboard:
<img width="940" height="429" alt="image" src="https://github.com/user-attachments/assets/d73bc5a3-08a6-42a7-9956-e4cb6735e85a" />


### Backend Server Running on Port:3001:
<img width="940" height="565" alt="image" src="https://github.com/user-attachments/assets/f80b0d54-4201-413e-b9d7-7c0a36d746ff" />


### npm:
<img width="940" height="276" alt="image" src="https://github.com/user-attachments/assets/7f29f24f-a0ba-42f5-b38c-b9531fd643ef" />

### Reverse Proxy:
<img width="940" height="435" alt="image" src="https://github.com/user-attachments/assets/3bd729e7-a193-464a-9a48-3b47987c672b" />


### Cloudfare:
<img width="940" height="460" alt="image" src="https://github.com/user-attachments/assets/42cf626e-713a-4897-b7d4-75c563cc7193" />

