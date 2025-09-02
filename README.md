Multi Threaded Proxy Server with LRU Cache

This project is implemented in C and extends a basic proxy server by adding multi-threading and an LRU (Least Recently Used) caching mechanism for improved performance and concurrency. The HTTP request parsing logic is adapted from Proxy Server
.

Index

Project Theory

How to Run

Demo

Contributing

Project Theory

[Back to top]

Introduction

A proxy server acts as an intermediary between a client and the destination server. This project enhances the proxy with multi-threading (to serve multiple clients concurrently) and an LRU cache (to reduce repeated network calls and improve speed).

Working Flow of the Proxy Server

Client sends a request to the proxy.

Proxy checks the cache (using LRU policy).

If data is present (cache hit), it is returned immediately.

If not (cache miss), the proxy fetches the data from the remote server, stores it in the cache, and returns it to the client.

How Multi-threading is Implemented

Used POSIX threads (pthread_create) for handling multiple clients concurrently.

Synchronization is handled using semaphores for locking shared resources.

Semaphores are preferred over condition variables in this case since sem_wait() and sem_post() do not require specific thread IDs, making them simpler and more efficient.

Motivation / Need of the Project

To understand:

The flow of HTTP requests and responses.

Handling concurrent connections.

Implementing cache management in networking.

Benefits of proxy servers:

Reduce server load and improve response time.

Restrict or filter website access.

Hide client IP from servers.

Enable request encryption for security.

OS Components Used

Threads – for concurrent client handling.

Semaphores – for synchronization.

Locks – to prevent race conditions.

Cache – implemented with LRU eviction policy.

Limitations

Large responses may not fit in cache due to fixed cache size.

If a URL spawns multiple client responses, only partial content may be cached.

Future Extensions

Implement multiprocessing for even faster request handling.

Add access control to block/allow certain websites.

Extend to handle POST requests.

Enhance caching strategy to support larger websites and persistent storage.

How to Run
$ git clone https://github.com/<your-username>/<your-repo-name>.git
$ cd <your-repo-name>
$ make all
$ ./proxy <port>


Open in browser:

http://localhost:<port>/https://www.cs.princeton.edu/


Notes:

Works only on Linux.

Disable your browser’s own cache to observe proxy caching.

To run the proxy without cache, rename proxy_server_with_cache.c to proxy_server_without_cache.c in the Makefile.

Demo

On first request to a website → Cache Miss (data fetched from server).

On subsequent requests → Cache Hit (data served from proxy cache).

Contributing

[Back to top]

Contributions are welcome! Check out Future Extensions
 for ideas, fork the repo, and submit a pull request.
