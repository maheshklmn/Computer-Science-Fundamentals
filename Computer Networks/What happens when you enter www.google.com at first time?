## ❓ The Question

**What happens when you type `www.google.com` in your browser for the first time?** \

This question requires you to explain the full sequence of events, assuming no prior data (like DNS records or website assets) is cached.

---

## ✅ The Answer: 8-Step Workflow

When you enter the URL and press Enter, your computer and the network execute the following steps: 

### 1. DNS Resolution

* Your browser first checks its cache and the local operating system's hosts file for the **IP address** of `www.google.com`.
* If not found, it sends a **DNS query** to a configured DNS server.
* The DNS system (involving recursive, root, TLD, and authoritative nameservers) resolves the domain name to its corresponding **IP address** (e.g., a specific server IP).

### 2. TCP Connection

* Using the resolved IP address, the browser initiates a **TCP connection** to the Google web server (typically on port 80 for HTTP or 443 for HTTPS).
* This is established using the **TCP 3-way handshake** for reliable communication: **SYN** $\rightarrow$ **SYN-ACK** $\rightarrow$ **ACK**.

### 3. TLS/SSL Handshake

* Since `www.google.com` is an HTTPS site, a **TLS/SSL handshake** immediately follows to establish a secure, encrypted tunnel.
* This process verifies the server's identity (via its digital certificate) and securely exchanges keys for future encrypted data transfer.

### 4. HTTP Request

* The browser is now ready to ask for the page. It sends an **HTTP GET request** to the server, asking for the contents of the Google homepage.

### 5. Server Processing

* The Google server receives the request. It processes the client's query, which may involve:
    * Running application logic.
    * Querying databases for dynamic content.
    * Generating the necessary HTML, CSS, and JavaScript.

### 6. HTTP Response

* The server packages the generated content into an **HTTP response** (including a status code like `200 OK`) and sends it back to the browser.

### 7. Rendering of the Page

* The browser receives the response and begins the process of rendering the page:
    * It parses the **HTML**.
    * It retrieves and applies **CSS** for styling.
    * It executes **JavaScript** for interactivity.
    * The complete page is displayed to the user.

### 8. Caching

* To ensure faster loading on future visits, the browser caches certain assets (images, stylesheets, scripts, and the DNS information itself) based on caching rules defined in the server's response headers.
