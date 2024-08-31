# News Dissemination System

## Objectives

This code implements a news dissemination system using various communication techniques and the TCP/IP protocol stack, particularly UDP, TCP, and IP multicast.

## Application Features

### Architecture

The news application consists of several components:

- **Server:**
  - Authenticates and accepts client connections.
  - Manages topics and client subscriptions.
  - Sends multicast addresses to clients for news topics.
  - Communicates with clients over TCP and the administration console over UDP.

- **Administration Console:**
  - Communicates with the server via UDP.
  - Manages users and configures the application.

- **Client:**
  - Communicates with the server via TCP.
  - Subscribes to news topics and receives news via multicast.
  - May send news if permitted.

Clients must authenticate with the server using a username and password registered by the administrator. Clients are either subscribers or publishers, based on their permissions.

### Server Functionality

- **Manage News Topics:**
  - Inform clients of available topics and manage client subscriptions.
  - Authenticate clients and manage permissions (subscribers or publishers).
  - Provide multicast addresses for subscribed topics.

- **User Management:**
  - Manage users with login, password, and permissions, stored in a file.
  - Admin can use a command-line interface (CLI) over UDP to:
    - Add or delete users.
    - List users.
    - Exit the console.
    - Shut down the server.
  - Admin authentication is required to access the CLI.

- **Client Access:**
  - Validate client access with username and password.
  - Provide information about topics the client is associated with.
  - Handle topic subscription requests and provide multicast addresses.

- **Concurrency:**
  - Support simultaneous connections from multiple clients.

**Server Command Syntax:**

```bash
news_server {NEWS_PORT} {CONFIG_PORT} {config_file}
```
## Client Functionality

### Subscriber Client:
- Authenticate with username and password.
- List topics and subscribe to them.
- Receive news via multicast.
- Remove client from all groups upon exit.

### Publisher Client:
- In addition to subscriber functions, can create topics and send news to the multicast group.

## Client Command Syntax

```bash
news_client {server_address} {NEWS_PORT}
```

## Communication Protocols

- **TCP:** Used for communications between clients and the server.
- **UDP:** Used for communications between the server and the administration console.
- **Multicast:** Used for distributing news to subscribed clients.

## Administration Console Commands

- Add user: `ADD_USER {username} {password} {admin/client/journalist}`
- Delete user: `DEL {username}`
- List users: `LIST`
- Exit console: `QUIT`
- Shut down server: `QUIT_SERVER`

