# My Microservice for Team Work Platform

## Overview
This project is a team collaboration platform built on a microservices architecture. It includes services for authentication, task management, chat management, and notifications.

## Architecture

### Microservices

1. **Authentication**
   - **REST API**: 
     - **Sign Up**: 
       - **Endpoint**: `POST /api/auth/signup`
       - **Example**:
         ```json
         {
           "username": "user1",
           "password": "password123",
           "email": "user@example.com"
         }
         ```
     - **Log In**:
       - **Endpoint**: `POST /api/auth/login`

2. **Tasks**
   - **Create Task**:
     - **Endpoint**: `POST /api/task/create`
   - **Edit Task**:
     - **Endpoint**: `PUT /api/task/{task.id}`
   - **Delete Task**:
     - **Endpoint**: `DELETE /api/task/{task.id}`
   - **Split Tasks**:
     - **Endpoint**: `POST /api/task/split`
   - **Delegate Task**:
     - **Endpoint**: `POST /api/task/delegate`

3. **Chats Manager**
   - **View Chats**:
     - **Endpoint**: `GET /api/chats/load`
   - **Create Chats**:
     - **Endpoint**: `POST /api/chats/create`
   - **Delete Chats**:
     - **Endpoint**: `DELETE /api/chats/{chat.id}`
   - **Add Users**:
     - **Endpoint**: `POST /api/chats/{chat.id}/add_user`
   - **Remove Users**:
     - **Endpoint**: `POST /api/chats/{chat.id}/remove_user`

4. **Messenger (MQTT)**
   - Subscribe to the topic `chat/{chatId}` to receive messages.
   - Messages can contain text, files, and images.
   - **Send Message**
   - **Send Files**
   - **Send Images**
   - **Edit Text**
   - **Delete Message**

5. **Notifications (Kafka)**
   - **Send Notifications**
   - **Example**:
     ```json
     {
       "notificationType": "taskAssigned",
       "userId": "user123",
       "message": "You have been assigned a new task.",
       "taskId": "task456",
       "timestamp": "2024-11-03T12:00:00Z"
     }
     ```

### Communication
- **REST API**: For synchronous microservices communication.
- **Kafka**: For asynchronous microservices communication.
- **MQTT**: For low latency messaging.

### Data Storage
- **PostgreSQL**: Used for storing task information and user data.

## Security
- **OAuth2 + OpenID Connect**: A reliable authentication system.
- **ABAC (Attribute-Based Access Control)**: For managing access control.
- **JWT**: Used for signing tokens.
- Split all microservices into different subnets to limit access through a firewall.
- Regularly check for updates on libraries and frameworks.

## Deployment
- **Docker & Kubernetes**: Used for scaling the application.

## Testing
- **JUnit**: For isolated unit testing.
- **Spring Boot Test**: For integration testing.

## Monitoring
- **ELK Stack**: (Elasticsearch, Logstash, Kibana) for logging.
- **Prometheus & Grafana**: For metrics collection and visualization.
- **Alertmanager**: For setting up alerts.

## Data Structure
- **Task**: Contains the following fields:
  - Name of task
  - Description
  - Deadline
  - Executor
  - Comments
- **User**: Contains the following fields:
  - First name
  - Last name
  - ID
  - Email
  - Password
  - Profile picture
  - Access token (with appropriate rights)
- **Chats**: Contains the following fields:
  - Name
  - Members
  - Logo
  - Last message
- **Message**: Contains the following fields:
  - Sender
  - Message content (text and/or file)
  - Send time
  - Edited flag (if edited)
  - Read status
- **Notifications**: Contains the following fields:
  - Name/type
  - Message content
  - Time

## Documentation
Further documentation will be provided as the project evolves. Please refer to the specific microservice documentation for detailed usage instructions and examples.