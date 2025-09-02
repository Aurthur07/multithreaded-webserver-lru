Multithreaded Proxy Web Server with LRU Cache
📌 Overview

This project is a multithreaded HTTP proxy web server implemented in C, featuring an integrated Least Recently Used (LRU) caching mechanism. The server efficiently handles multiple client requests concurrently while reducing response time by caching frequently accessed content.

✨ Features

🚀 Multithreading with Pthreads – handles multiple clients in parallel.

📂 LRU Cache – speeds up responses by reusing cached results.

🧩 Custom HTTP Parser – implemented in proxy_parse.c/.h.

⚡ Scalable Design – modular and extensible architecture.

📂 Project Structure
.
├── Makefile                # Build instructions
├── proxy                   # Compiled executable
├── proxy_parse.c           # HTTP request parser implementation
├── proxy_parse.h           # HTTP parser header
├── proxy_server_with_cache.c  # Main server with multithreading & cache
└── .vscode/                # VS Code settings

⚙️ Build & Run
# Clone the repo
git clone https://github.com/your-username/multithreaded-webserver-lru.git
cd multithreaded-webserver-lru

# Build
make

# Run the proxy server
./proxy <port_number>


Example:

./proxy 8080

📜 Future Enhancements

HTTPS support

Configurable cache size

Logging & monitoring

🤝 Contribution

Contributions, issues, and feature requests are welcome!

👉 Do you want me to also include a Usage Example (client → server → remote server flow) diagram in the README? It would make it much more attractive for recruiters on GitHub.
