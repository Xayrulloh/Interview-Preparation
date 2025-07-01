# Network Interview Question

1. ## **http1 vs http2 vs http3?**  
    - ### http1: 
        - **Text based, Persistent connections, No multiplexing:** *Requires multiple TCP connections for parallel requests → slower*
        - **Head-of-line:** *One slow request blocks others in the queue, blocking*
        - **No server push:** *Client must request each resource explicitly*
    - ### http2:
        - **Binary protocol:** *Smaller, faster parsing*
        - **Multiplexing:** *Multiple requests/responses over a single TCP connection → no HOL blocking at the HTTP level*
        - **Header compression (HPACK):** *Reduces overhead*
        - **Server push:** *Server can send resources before the client asks for them*
        - **Stream prioritization:** *Important resources load first*
    - ### http3:
        - **Replaces TCP with QUIC:** *UDP-based, avoids TCP'c HOL blocking*
        - **Faster connection setup:** *0-RTT handshake for repeat visitors*
        - **Improved security:** *Encryption built into QUIC*
        - **Better mobility support:** *Seamless switching between networks, e.g., Wi-Fi to 5G*
        - **Per-stream flow control:** *No HOL blocking at all*

2. ## **HTTP vs HTTPS?**    
    - ### HTTP (Hypertext Transfer Protocol)
        - **Function:** *The foundation of data communication for the World Wide Web, used to transmit text, images, and other web resources*
        - **Security:** *Transmits data in plain text, making it vulnerable to interception and manipulation by malicious actors*
        - **Vulnerabilities:** *Susceptible to man-in-the-middle attacks, where an attacker can intercept and potentially alter the data being exchanged*
    - ### HTTPS (Hypertext Transfer Protocol Secure)
        - **Function:** *An extension of HTTP that adds a layer of security through encryption*
        - **Security:** *Uses TLS/SSL encryption to protect data during transmission, ensuring confidentiality and integrity*
        - **Benefits:**
            - **Security:** *Encrypts data, preventing eavesdropping and tampering* 
            - **Trust:** *Signals to users that the website is trustworthy and takes their security seriously*
            - **SEO:** *Search engines like Google favor HTTPS sites, potentially boosting rankings*
        - **Implementation:** *Requires an SSL/TLS certificate, which verifies the website's identity and enables encryption*

3. ## **CORS?**    
    *CORS is a browser security mechanism that controls how web pages from one **origin** (domain) can request resources (APIs, data) from another origin* 

    - ### How It Works:  
        - **Simple Requests (GET, POST)**  
            - The browser sends the request directly (e.g., to `api.example.com`).  
            - The server responds with CORS headers (like `Access-Control-Allow-Origin`).  
            - If the origin is allowed, the request succeeds; otherwise, the browser blocks it with a **CORS error**.  

        - **Preflight Requests (PUT, DELETE, etc.)**  
            - For "non-simple" requests, the browser first sends an **OPTIONS** request to check permissions.  
            - The server responds with allowed methods (`Access-Control-Allow-Methods`).  
            - If approved, the actual request (PUT/DELETE) is sent.  

    - ### Why CORS Exists:  
        - Prevents malicious sites from accessing sensitive data on other domains without permission.  
        - Servers must explicitly allow cross-origin requests via headers.  

4. ## **TCP vs UDP**  
    | Feature          | TCP (Transmission Control Protocol)                          | UDP (User Datagram Protocol)                     |
    |------------------|-------------------------------------------------------------|-------------------------------------------------|
    | **Reliability**  | ✅ **Guaranteed delivery** (retransmits lost packets)        | ❌ **Best-effort delivery** (no retransmissions) |
    | **Ordering**     | ✅ **In-order delivery** (sequences packets)                 | ❌ **No packet ordering**                       |
    | **Connection**   | ✅ **Connection-oriented** (3-way handshake: `SYN` > `SYN-ACK` > `ACK`) | ❌ **Connectionless** (no handshake) |
    | **Speed**        | ⚠️ **Slower** (overhead for reliability checks)             | ⚡ **Faster** (low overhead, minimal latency)   |
    | **Use Cases**    | Web browsing (HTTP/HTTPS), emails, file transfers            | Video streaming, gaming, VoIP, live broadcasts  |
    | **Congestion Control** | ✅ Adjusts transmission rate to avoid network congestion  | ❌ No congestion control (can flood the network) |

    ### Key Differences:  
    - **TCP** is like a **registered mail**—slow but ensures delivery.  
    - **UDP** is like a **postcard**—fast but no guarantees.  

    ### When to Use?  
    - **Choose TCP** for data where **accuracy matters** (e.g., bank transactions).  
    - **Choose UDP** for **real-time speed** (e.g., Zoom calls, online games).  

5. ## **REST vs GraphQL**  

    | Feature          | REST (Representational State Transfer)               | GraphQL                              |
    |------------------|-----------------------------------------------------|--------------------------------------|
    | **Endpoints**    | ❗ Multiple fixed endpoints (e.g., `/users`, `/posts`) | ✅ Single endpoint (`/graphql`)      |
    | **Data Fetching**| ⚠️ Over-fetching or under-fetching data              | 🔍 Clients request **exact data needed** (no waste) |
    | **Requests**     | 🐢 Multiple round trips (e.g., fetch users → then posts) | ⚡ Single request (nested queries) |
    | **Flexibility**  | ❗ Rigid (server-defined responses)                  | ✅ Dynamic (client-defined queries)  |
    | **Use Cases**    | Simple APIs, caching-friendly                       | Complex apps with nested data (e.g., social networks) |

    ### TL;DR:  
    - **REST** = Fixed menu 🍽️ (get what the server gives).  
    - **GraphQL** = Buffet 🥘 (ask for exactly what you want).  

6. ## **Lazy Loading**  
    *A performance optimization technique that **delays loading** of non-critical resources (images, components, scripts) until they're needed (e.g., when visible in viewport)*

    ### 🛠️ How it Works:
    | Traditional Loading | Lazy Loading |
    |--------------------|-------------|
    | Loads **all** resources upfront | Loads only **critical** resources first |
    | Slower initial load ⏳ | Faster initial load ⚡ |
    | Wastes bandwidth 📶 | Saves bandwidth 💾 |

    ### 💡 Key Benefits:
    - **Faster page load times** (better UX & SEO)
    - **Reduced data usage** (mobile-friendly)
    - **Lower server costs** (fewer initial requests)

7. ## **CDN?**    
    *A CDN (Content Delivery Network) is a globally distributed network of servers that delivers web content (like images, videos, CSS, and JavaScript) to users based on their geographic location, improving speed, performance, and reliability*

8. ## **WEB3?**
    - **Decentralized Internet:**  *No central authority (blockchain-based)*
    - **User Ownership:** *Control your data/assets via crypto wallets*
    - **Smart Contracts:** *Self-executing code on blockchains (e.g., Ethereum)*

9. ## **Authentication vs Authorization?**
    - **AuthN (Authentication):** *is to know who you really are (JWT, OAUTH, etc…)*
    - **AuthZ (Authorization):** *is to know that you’ve an access or not (RBAC)*