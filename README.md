# Task Management App

Building a **Task Management App** using Angular and Spring Boot can be a great full-stack project. Below is a detailed breakdown of the requirements for the **Task Management App**:

## 1. Key Features
- **User Authentication**: Users can sign up, log in, and manage their session.
- **Task CRUD Operations**: Users can Create, Read, Update, and Delete tasks.
- **Task Filtering and Sorting**: Users can filter tasks by status (e.g., Completed, In Progress, Pending) and sort tasks by priority, due date, or creation date.
- **Task Labels/Categories**: Tasks can be categorized with labels like Work, Personal, Urgent.
- **Real-Time Updates with WebSocket**: Tasks added or modified by one user are updated in real-time across all active sessions.
- **Task Prioritization**: Users can assign priorities to tasks (e.g., High, Medium, Low).
- **Task Due Date**: Users can set a due date for each task.
- **Task Notifications (Optional)**: Alert users when tasks are near their due date.

## 2. Tech Stack
- **Frontend**: Angular
    - **UI Framework**: Angular Material or Bootstrap
    - **Routing**: Angular Router
    - **State Management**: NgRx or services with `BehaviorSubject`
    - **Real-time Communication**: WebSocket with RxJS
- **Backend**: Spring Boot
    - **Database**: MySQL or PostgreSQL
    - **Security**: Spring Security (JWT for authentication)
    - **Real-time Communication**: WebSocket API
    - **Persistence**: JPA (Hibernate)
    - **API Layer**: RESTful APIs

---

## 3. Detailed Frontend (Angular) Requirements

### 3.1 UI Components
- **Login/Register Page**:
    - Form for login and registration
    - Email/Username and password validation
- **Dashboard** (Task Listing):
    - Display tasks with sorting and filtering options (status, priority, due date)
    - Search bar for quick task search
    - "Add Task" button for creating new tasks
    - Real-time task updates with WebSocket (e.g., new tasks appear without page refresh)
- **Task Form**:
    - Task Name (required)
    - Task Description
    - Task Priority (dropdown: High, Medium, Low)
    - Task Due Date (Date picker)
    - Task Status (dropdown: Completed, In Progress, Pending)
    - Labels/Categories (optional tags for tasks)
- **Task View**:
    - Display task details
    - Buttons for editing or deleting tasks
- **Notification System** (Optional):
    - Popup or badge notification when a task is close to its due date
- **Responsive Design**:
    - Ensure the app is responsive for mobile and desktop views.

### 3.2 Routing and Guards
- **Authentication Guard**: Ensure protected routes like the Dashboard and Task Form are only accessible to authenticated users.
- **Lazy Loading**: Load different modules like `DashboardModule`, `AuthModule` lazily to improve app performance.
- **Route Structure**:
    - `/login` (Login Page)
    - `/register` (Register Page)
    - `/tasks` (Dashboard for task management)
    - `/task/:id` (View/Edit Task)
    - `/add-task` (Form to create a new task)

### 3.3 State Management
- Use **NgRx** for managing the global state of tasks, user session, and real-time updates.
- Alternatively, use Angular services with `BehaviorSubject` to manage the local state.

### 3.4 Real-Time Updates with WebSocket
- Create a WebSocket connection to the Spring Boot backend to receive real-time task updates.
- Use **RxJS** in Angular to handle WebSocket streams for tasks created, updated, or deleted by other users.

---

## 4. Backend (Spring Boot) Requirements

### 4.1 Entity Models
- **User**: For managing users
    - `id`, `email`, `username`, `password`, `roles`
- **Task**: For task management
    - `id`, `name`, `description`, `priority`, `dueDate`, `status`, `labels`, `createdBy` (link to User), `createdAt`, `updatedAt`

### 4.2 Security
- Implement **JWT Authentication** for securing the API endpoints.
- Use **Spring Security** for authentication and authorization.
- Secure REST API endpoints to be accessible only to authenticated users.

### 4.3 Database Schema
- **Tables**:
    - `users`: Store user information (username, email, password, roles).
    - `tasks`: Store task information (task name, description, priority, due date, status, user id).
- Use **JPA/Hibernate** to persist data.

### 4.4 REST API Endpoints
- **AuthController**:
    - `POST /auth/login`: User login, returns JWT token
    - `POST /auth/register`: User registration
- **TaskController**:
    - `GET /api/tasks`: Get a list of all tasks for the authenticated user (supports filtering and sorting via query params)
    - `POST /api/tasks`: Create a new task
    - `GET /api/tasks/{id}`: Get task details by task ID
    - `PUT /api/tasks/{id}`: Update task details
    - `DELETE /api/tasks/{id}`: Delete a task
- **WebSocketController**:
    - `/ws/task-updates`: WebSocket endpoint for task updates in real time (new task, task update, task delete)

### 4.5 Real-Time Updates with WebSocket
- Use Spring WebSocket to broadcast task changes (e.g., new task creation, updates, or deletions).
- Use an event-based system where task changes are automatically broadcast to subscribed users via WebSocket.

### 4.6 Service Layer
- **TaskService**: Handle business logic related to task management (CRUD operations, filtering, sorting).
- **UserService**: Handle user registration, login, and authentication.

---

## 5. Deployment & Best Practices

### 5.1 GitHub Repository Best Practices
- Follow GitHub repo best practices for version control.
- Add a detailed `README.md` with project setup instructions.
- **Commit Messages**: Use meaningful commit messages following the format: `feat: added task creation API`, `fix: fixed task update issue`.
- **Branching Strategy**: Use feature branching (e.g., `feature/task-crud`) and GitFlow for version control.

### 5.2 Deployment:
- **Frontend (Angular)**: Deploy to platforms like Vercel, Netlify, or GitHub Pages.
- **Backend (Spring Boot)**: Deploy to services like Heroku, AWS, or any preferred cloud provider.
- Configure **CI/CD pipeline** for automated deployment using GitHub Actions or Jenkins.

---

## 6. Resources
- **Angular Setup**: [Angular Documentation](https://angular.io/docs)
- **Spring Boot Setup**: [Spring Boot Documentation](https://spring.io/guides/gs/spring-boot/)
- **WebSocket with Spring Boot**: [Spring WebSocket Guide](https://spring.io/guides/gs/messaging-stomp-websocket/)
- **JWT Authentication in Spring Boot**: [JWT with Spring Boot](https://www.baeldung.com/spring-security-oauth-jwt)
- **Real-time WebSocket with Angular**: [Angular WebSocket Guide](https://blog.angular-university.io/angular-websockets-tutorial/)
