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


<img width="940" height="1131" alt="image" src="https://github.com/user-attachments/assets/a879c517-14c0-43c6-9be8-73a74283f0c9" />

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
<img width="940" height="224" alt="image" src="https://github.com/user-attachments/assets/6827e589-1305-4029-ae02-992299ec1348" />

### Security group:
<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/a9ed904e-951d-4d5c-9c46-13d30be8dd9a" />

### Load Balancer:
<img width="940" height="399" alt="image" src="https://github.com/user-attachments/assets/c4e7ede8-819e-4c7f-a6cd-79a5a2a71870" />

### Target Group:
<img width="940" height="437" alt="image" src="https://github.com/user-attachments/assets/79e2d79d-e829-40ba-a62c-621dec65cb86" />

### VPC Dashboard:
<img width="940" height="429" alt="image" src="https://github.com/user-attachments/assets/fbddf623-2981-4724-a88f-576267ddb8ae" />

### Backend Server Running on Port:3001:
<img width="940" height="565" alt="image" src="https://github.com/user-attachments/assets/6f31728e-f8a3-4a97-8d0c-38687264588c" />

### npm:
<img width="940" height="276" alt="image" src="https://github.com/user-attachments/assets/5eb4f998-82d5-4cc0-bccc-455cfbe37126" />

### Reverse Proxy:
<img width="940" height="435" alt="image" src="https://github.com/user-attachments/assets/c841a62c-99f3-49e0-8538-9b6499f62aff" />

### Cloudfare:
<img width="940" height="460" alt="image" src="https://github.com/user-attachments/assets/ad85aef4-779f-483d-8696-ad49920b2fac" />
