# Network Interview Question

1. ## **http1 vs http2 vs http3?**

   - ### http1:
     - **Text based, Persistent connections, No multiplexing:** _Requires
       multiple TCP connections for parallel requests → slower_
     - **Head-of-line:** _One slow request blocks others in the queue, blocking_
     - **No server push:** _Client must request each resource explicitly_
   - ### http2:
     - **Binary protocol:** _Smaller, faster parsing_
     - **Multiplexing:** _Multiple requests/responses over a single TCP
       connection → no HOL blocking at the HTTP level_
     - **Header compression (HPACK):** _Reduces overhead_
     - **Server push:** _Server can send resources before the client asks for
       them_
     - **Stream prioritization:** _Important resources load first_
   - ### http3:
     - **Replaces TCP with QUIC:** _UDP-based, avoids TCP'c HOL blocking_
     - **Faster connection setup:** _0-RTT handshake for repeat visitors_
     - **Improved security:** _Encryption built into QUIC_
     - **Better mobility support:** _Seamless switching between networks, e.g.,
       Wi-Fi to 5G_
     - **Per-stream flow control:** _No HOL blocking at all_

2. ## **HTTP vs HTTPS?**

   - ### HTTP (Hypertext Transfer Protocol)
     - **Function:** _The foundation of data communication for the World Wide
       Web, used to transmit text, images, and other web resources_
     - **Security:** _Transmits data in plain text, making it vulnerable to
       interception and manipulation by malicious actors_
     - **Vulnerabilities:** _Susceptible to man-in-the-middle attacks, where an
       attacker can intercept and potentially alter the data being exchanged_
   - ### HTTPS (Hypertext Transfer Protocol Secure)
     - **Function:** _An extension of HTTP that adds a layer of security through
       encryption_
     - **Security:** _Uses TLS/SSL encryption to protect data during
       transmission, ensuring confidentiality and integrity_
     - **Benefits:**
       - **Security:** _Encrypts data, preventing eavesdropping and tampering_
       - **Trust:** _Signals to users that the website is trustworthy and takes
         their security seriously_
       - **SEO:** _Search engines like Google favor HTTPS sites, potentially
         boosting rankings_
     - **Implementation:** _Requires an SSL/TLS certificate, which verifies the
       website's identity and enables encryption_

3. ## **CORS?**

   _CORS is a browser security mechanism that controls how web pages from one
   **origin** (domain) can request resources (APIs, data) from another origin_

   - ### How It Works:

     - **Simple Requests (GET, POST)**

       - The browser sends the request directly (e.g., to `api.example.com`).
       - The server responds with CORS headers (like
         `Access-Control-Allow-Origin`).
       - If the origin is allowed, the request succeeds; otherwise, the browser
         blocks it with a **CORS error**.

     - **Preflight Requests (PUT, DELETE, etc.)**
       - For "non-simple" requests, the browser first sends an **OPTIONS**
         request to check permissions.
       - The server responds with allowed methods
         (`Access-Control-Allow-Methods`).
       - If approved, the actual request (PUT/DELETE) is sent.

   - ### Why CORS Exists:
     - Prevents malicious sites from accessing sensitive data on other domains
       without permission.
     - Servers must explicitly allow cross-origin requests via headers.

4. ## **TCP vs UDP**

   | Feature                | TCP (Transmission Control Protocol)                                     | UDP (User Datagram Protocol)                     |
   | ---------------------- | ----------------------------------------------------------------------- | ------------------------------------------------ |
   | **Reliability**        | ✅ **Guaranteed delivery** (retransmits lost packets)                   | ❌ **Best-effort delivery** (no retransmissions) |
   | **Ordering**           | ✅ **In-order delivery** (sequences packets)                            | ❌ **No packet ordering**                        |
   | **Connection**         | ✅ **Connection-oriented** (3-way handshake: `SYN` > `SYN-ACK` > `ACK`) | ❌ **Connectionless** (no handshake)             |
   | **Speed**              | ⚠️ **Slower** (overhead for reliability checks)                         | ⚡ **Faster** (low overhead, minimal latency)    |
   | **Use Cases**          | Web browsing (HTTP/HTTPS), emails, file transfers                       | Video streaming, gaming, VoIP, live broadcasts   |
   | **Congestion Control** | ✅ Adjusts transmission rate to avoid network congestion                | ❌ No congestion control (can flood the network) |

   ### Key Differences:

   - **TCP** is like a **registered mail**—slow but ensures delivery.
   - **UDP** is like a **postcard**—fast but no guarantees.

   ### When to Use?

   - **Choose TCP** for data where **accuracy matters** (e.g., bank
     transactions).
   - **Choose UDP** for **real-time speed** (e.g., Zoom calls, online games).

5. ## **REST vs GraphQL**

   | Feature           | REST (Representational State Transfer)                   | GraphQL                                               |
   | ----------------- | -------------------------------------------------------- | ----------------------------------------------------- |
   | **Endpoints**     | ❗ Multiple fixed endpoints (e.g., `/users`, `/posts`)   | ✅ Single endpoint (`/graphql`)                       |
   | **Data Fetching** | ⚠️ Over-fetching or under-fetching data                  | 🔍 Clients request **exact data needed** (no waste)   |
   | **Requests**      | 🐢 Multiple round trips (e.g., fetch users → then posts) | ⚡ Single request (nested queries)                    |
   | **Flexibility**   | ❗ Rigid (server-defined responses)                      | ✅ Dynamic (client-defined queries)                   |
   | **Use Cases**     | Simple APIs, caching-friendly                            | Complex apps with nested data (e.g., social networks) |

   ### TL;DR:

   - **REST** = Fixed menu 🍽️ (get what the server gives).
   - **GraphQL** = Buffet 🥘 (ask for exactly what you want).

6. ## **Lazy Loading**

   _A performance optimization technique that **delays loading** of non-critical
   resources (images, components, scripts) until they're needed (e.g., when
   visible in viewport)_

   ### 🛠️ How it Works:

   | Traditional Loading             | Lazy Loading                            |
   | ------------------------------- | --------------------------------------- |
   | Loads **all** resources upfront | Loads only **critical** resources first |
   | Slower initial load ⏳          | Faster initial load ⚡                  |
   | Wastes bandwidth 📶             | Saves bandwidth 💾                      |

   ### 💡 Key Benefits:

   - **Faster page load times** (better UX & SEO)
   - **Reduced data usage** (mobile-friendly)
   - **Lower server costs** (fewer initial requests)

7. ## **CDN?**

   _A CDN (Content Delivery Network) is a globally distributed network of
   servers that delivers web content (like images, videos, CSS, and JavaScript)
   to users based on their geographic location, improving speed, performance,
   and reliability_

8. ## **WEB3?**

   - **Decentralized Internet:** _No central authority (blockchain-based)_
   - **User Ownership:** _Control your data/assets via crypto wallets_
   - **Smart Contracts:** _Self-executing code on blockchains (e.g., Ethereum)_

9. ## **Authentication vs Authorization?**
   - **AuthN (Authentication):** _is to know who you really are (JWT, OAUTH,
     etc…)_
   - **AuthZ (Authorization):** _is to know that you’ve an access or not (RBAC)_
