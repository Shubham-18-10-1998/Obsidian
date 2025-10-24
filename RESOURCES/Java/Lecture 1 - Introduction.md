
## What is a front-end?
Part of application the user interacts with and what helps the user interact with the application logic. It runs on the client side.

The look and feel is front-end.

- Client-side programming
- User Interface
- Accessibility

HTML - Skeleton
CSS - Beauty
JS - Brain

Note: The logic used in front-end angular typescript is all part of the front-end and comes under front end logic as during **Transpilation** it gets converted from typescript to JS to run on the browser and another key feature of front end is that it runs on client machine (browser in this case).

Transpilation: Conversion of typescript to JS so it can be run on browser.

eg. 
- in restaurant the look and feel, painting on wall furniture etc.
- Car, look and feel is front-end, engine, electronics, fuel mechanisms etc is backend.

## What is back-end?
Part of application that the user cant interact with directly. All logic for the application comes under back-end. Two main segments are DB and Server.
- DB is what holds all the data for the application. 
- Server consist of hosting and the APIs.
- eg. - In restaurant, the waiter is the API who is the medium between customer (front-end) requesting, in the kitchen with the the chef and staff is the Server (who is  preparing the thing and giving) and the fridge which provides the ingredients is DB.
	- The API along with the server and DB together comprise of the backend.

Spring-boot is the framework for server to use Java to make backend.

## How does Internet work?
- We type address, the DNS system resolves the address (eg. - www.google.com) to its equivalent IP address (124.000.100.100 etc)
- Then our request packet is sent via the router to our ISP which then trhough multiple routers reaches the server of the site (google in this case).
- It then responds and the packet travels back and our browser shows the result.

### DNS-
In DNS, the name of the page is then checked for its unique IP address. When the IP address is received, then routed to that IP address.

How does DNS work?

**DNS (Domain Name System)** translates **human-readable domain names** (like `www.google.com`) into **IP addresses** (like `142.250.183.4`) that computers use to communicate.  
It acts as the **internet’s phonebook**.

---

### ⚙️ **Step-by-Step Process**

1. **User enters URL:**  
    You type `www.google.com` into your browser.
    
2. **Local cache check:**  
    Browser or OS checks if it already knows the IP. If not, it asks a **DNS resolver** (usually your ISP or a public DNS like Google `8.8.8.8`).
    
3. **Resolver begins lookup:**  
    If not cached, the resolver queries the DNS hierarchy step by step.
    
    - **Root Server:**  
        Directs the resolver to the correct **TLD server** (e.g., `.com`).
        
    - **TLD Server(Top Level Domain):**  
        Points to the **authoritative server** for the specific domain (e.g., `google.com`).
        
    - **Authoritative Server:**  
        Provides the **actual IP address** for `www.google.com`.
        
4. **IP returned:**  
    The resolver sends the IP back to your browser.
    
5. **Caching:**  
    The result is stored temporarily (TTL – Time To Live) so future lookups are faster.
    
6. **Connection established:**  
    Browser connects directly to the server using the IP and loads the website.
    

---

### 🧩 **DNS Server Types**

|Type|Function|
|---|---|
|**Root Servers**|Know where to find TLD (.com, .org, .in) servers|
|**TLD Servers**|Know which authoritative servers manage each domain|
|**Authoritative Servers**|Store actual DNS records (A, CNAME, MX, etc.)|
|**Resolver (Recursive Server)**|Performs the lookup on behalf of users|

---

### ⚡ **Key Concepts**

- **Anycast:** Root and TLD servers are replicated worldwide; queries go to the nearest instance.
    
- **Caching:** Reduces repeated lookups, improving speed.
    
- **DNS Records:** Hold mappings (A → IP, MX → mail server, CNAME → alias, etc.).
    
- **DNSSEC:** Adds cryptographic security to prevent forged responses.
    

---

### 💡 **Analogy (Restaurant Edition)**

|Internet Part|Analogy|
|---|---|
|Browser|You (the customer)|
|DNS|The phonebook telling you the restaurant’s address|
|IP Address|The restaurant’s street address|
|Web Server|The restaurant serving your order|

---

**In short:**

> DNS is a distributed, hierarchical system that resolves domain names to IP addresses through root → TLD → authoritative servers, with caching and redundancy to make the internet fast and reliable.

---
## Questions and Doubts - 

- Location based routing, how does it work? -> Works through the Border Gateway Protocol which tells how many hops are needed for the Ip address and then it decides to forward to the least cost path.

- Cache Lives ?  -> Browser cache lasts 60 seconds to 5 minutes. OS caches last from 5 minutes to 1 hour sometimes also 24 hours but honour TTL (Time To Live).

- Does each multiple auth server have save IP address or how does it work? ->Yes, they are Any casted. 

- Does the DNS server return the IP address or is the request redirected directly? -> A DNS server does not redirect the request. It returns the IP address to the client. The client then uses that IP address to contact the intended destination, such as a web server.


Learn terminal
GIT all those understanding, Editor V and IntelliJ, Java, Postman get


## Client Server Architecture
The client (via browser or app)sends requests for what it needs and the server (A powerful machine or computer running 24/7) provides it back via HTTP (Hyper Text Transfer Protocol). This is the Client Server model.

### Http Requests-
Method - GET, PUT, POST, DELETE etc,
Endpoint - where you are sending the req to
Header - Metadata such as datatype, auth related data etc.
Body- Data you want to send to server.

### Http Response-
- Http Status Code - Status tellers like 200 OK 500 Internal server error (Tells status of the response being received)
- Headers - Metadata about response like length of response, type, TTL etc.
- Body - Holds what was requested.

### Request Types-
- GET : Default when you hit a webpage. Its used to retrieve things.
- POST : Add/Insert new data.
- PUT : Updating or creating a new resource, replaces the data completely.
- PATCH : Updating an existing resource. Partial Update.

### Status Codes-
- 1XX : Information codes - The server acknowledges and is processing requests.
	- eg. (100 Continue) - means initial part of request received and the server is waiting for the remaining request.
- 2XX : Success Codes - The server successfully received, understood and  processed the request
	- eg. 200 OK means request was successful.
- 3XX : Redirection Codes - The server received the request but there is a redirect to somewhere else or in rare cases that some additional action other than a redirect must be completed.
	- eg. 301 Resource moved permanently means the resource is now move to a new IP address and should be accessed from there.
- 4XX : Client Error Codes - The server couldn't find or reach the page or website. There is an error on sites side.
	- eg. 404 Resources not found
	- eg. 403 Forbidden failed
- 5XX : Server Side Error Codes - The Server encountered some issue. The client made a valid request but the server failed to complete the request.
	- eg. 500 Internal Server Error.




