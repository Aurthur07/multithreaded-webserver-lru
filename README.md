# Concurrent HTTP Proxy Server with Smart Caching

A high-performance, multi-threaded HTTP proxy server implementation in C, featuring intelligent caching mechanisms and concurrent request handling.

---

## Table of Contents

- [Quick Start](#quick-start)
- [Architecture Overview](#architecture-overview)
- [Key Features](#key-features)
- [Technical Implementation](#technical-implementation)
- [Performance & Optimization](#performance--optimization)
- [Build & Deployment](#build--deployment)
- [Live Demo](#live-demo)
- [Development](#development)

---

## Quick Start

### Prerequisites
- Linux-based operating system
- GCC compiler
- Make utility

### Installation & Setup
```bash
# Clone the repository
git clone <your-repo-url>
cd concurrent-proxy-server

# Build the project
make build

# Launch the proxy server
./http-proxy <desired-port>

# Access via browser
# Navigate to: http://localhost:<port>/https://example.com
```

> **Important:** Disable browser caching for optimal testing experience

---

## Architecture Overview

### System Design Philosophy
Our proxy server follows a **client-server-proxy** architecture pattern, where the proxy acts as an intelligent intermediary handling requests efficiently.

```
[Client Browser] ←→ [Proxy Server] ←→ [Target Web Server]
                        ↓
                   [LRU Cache Layer]
```

### Core Components
- **Request Handler**: Manages incoming HTTP requests
- **Thread Pool Manager**: Distributes workload across multiple threads
- **Cache Engine**: Implements LRU-based caching for faster response times
- **HTTP Parser**: Processes and validates HTTP protocol messages

---

## Key Features

### High Concurrency
- **Semaphore-based Threading**: Efficient thread synchronization without complex joins
- **Non-blocking Operations**: Prevents thread starvation and deadlocks
- **Scalable Architecture**: Handles multiple simultaneous client connections

### Intelligent Caching
- **LRU Algorithm**: Automatically manages cache memory efficiently
- **Response Optimization**: Reduces server load and improves response times
- **Cache Hit Analytics**: Monitor cache performance in real-time

### Enhanced Security
- **Request Filtering**: Potential for implementing access control
- **IP Masking**: Provides client anonymity
- **Request Encryption**: Foundation for secure data transmission

---

## Technical Implementation

### Threading Strategy
Instead of traditional `pthread_join()` and `pthread_exit()` mechanisms, we leverage:
- **Semaphore Synchronization**: `sem_wait()` and `sem_post()` for cleaner thread management
- **Resource Pooling**: Efficient thread lifecycle management
- **Lock-free Operations**: Minimizes contention and improves performance

### Cache Implementation Details
- **Data Structure**: Doubly-linked list for O(1) insertion/deletion
- **Memory Management**: Fixed-size cache elements with intelligent overflow handling  
- **Persistence**: In-memory storage with configurable size limits

### HTTP Protocol Handling
*HTTP parsing implementation adapted from open-source proxy server patterns*

---

## Performance & Optimization

### Current Capabilities
- Multi-client Support: Concurrent request handling  
- Memory Efficient: Optimized cache storage  
- Fast Response Times: Cache-first serving strategy  

### Known Limitations
- Complex Websites: Sites with multiple sub-requests may experience partial caching  
- Large Content: Fixed cache size may not accommodate very large responses  
- Protocol Support: Currently limited to GET requests  

---

## Build & Deployment

### Build Options

**With Caching (Default):**
```bash
make all
./http-proxy 8080
```

**Without Caching:**
```bash
# Rename source file to disable caching
mv proxy_server_with_cache.c proxy_server_without_cache.c
make all
./http-proxy 8080
```

### Configuration
- **Port Selection**: Any available port (recommended: 8080-9000)
- **Cache Size**: Configurable in source code
- **Thread Pool**: Adjustable based on system resources

---

## Live Demo

### Cache Performance Visualization

**First Request (Cache Miss):**
```
[LOG] URL: https://example.com → Cache Miss → Fetching from origin
[RESPONSE] Data served from origin server (120ms)
```

**Subsequent Request (Cache Hit):**
```
[LOG] URL: https://example.com → Cache Hit → Serving from cache
[RESPONSE] Data retrieved from cache (5ms)
```

### Testing Workflow
1. Start the proxy server on your chosen port
2. Configure your browser to use the proxy
3. Navigate to any HTTP/HTTPS website
4. Observe cache hit/miss logs in the terminal
5. Refresh the page to see cache performance improvement

---

## Development

### Future Enhancements
- Multi-processing Support: Leverage process-level parallelism
- Advanced Filtering: Website access control and content filtering
- Extended HTTP Methods: Support for POST, PUT, DELETE operations
- Dynamic Cache Sizing: Adaptive cache management
- SSL/TLS Termination: Enhanced security features
- Load Balancing: Distribute requests across multiple backend servers

### Contributing Guidelines
We welcome contributions! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Implement** your changes with proper documentation
4. **Test** thoroughly on different scenarios
5. **Submit** a pull request with detailed description

### Code Standards
- Follow existing commenting conventions
- Ensure thread-safety in all modifications
- Add appropriate error handling
- Update documentation for new features

---

### Support & Feedback
Found a bug or have suggestions? Feel free to open an issue or submit a pull request. All contributions are appreciated!
