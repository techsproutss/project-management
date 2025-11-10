## 📘 Project Overview

You are required to develop a **Project Management System** using **Laravel** (version 10 or later) and **Blade (Bootstrap for UI)**.  
The system should support **multiple user roles**, **authorization**, **API creation**, **service-layer abstraction**, and a clean **frontend dashboard**.

---

## 🧱 Functional Requirements

### 1. Authentication & User Roles
- Implement authentication using any approach (Laravel Breeze, Fortify, or custom).
- There should be **three types of users**:
  - **Admin:** Can manage all users and projects.
  - **Manager:** Can manage only their own projects and assign tasks.
  - **Employee:** Can view and update only their assigned tasks.

### 2. Role-Based Authorization
- Use **middleware** and/or **policies** to control access:
  - Admin → full access
  - Manager → access to their assigned projects and related tasks
  - Employee → access to only their tasks
- Redirect users to dashboards based on their role after login.

---

## 🗄️ Database Design

Create the following entities and relationships:

| Table | Fields | Relationships |
|--------|---------|---------------|
| **users** | id, name, email, password, role | hasMany(Projects as manager), hasMany(Tasks as assigned user) |
| **projects** | id, name, description, manager_id (FK→users.id) | belongsTo(User as manager), hasMany(Tasks) |
| **tasks** | id, project_id (FK→projects.id), assigned_to (FK→users.id), title, description, status, due_date | belongsTo(Project), belongsTo(User as assigned employee) |

**Notes:**
- Use **foreign key constraints**.
- Seed database with at least one Admin, Manager, and Employee account.

---

## ⚙️ Backend Logic

### 1. CRUD Operations
- **Projects:**  
  - Only Admin or Manager can create, update, or delete projects.
- **Tasks:**  
  - Only Managers can create or assign tasks under their projects.  
  - Employees can update only their task status.

### 2. Service Layer
Implement a **Service class** for each core entity:
- `ProjectService` — handles all project logic.
- `TaskService` — handles assignment and task updates.

> Controllers should call Service classes; avoid heavy business logic in controllers.

### 3. Authorization Policies
- Use Laravel **Policy classes** for fine-grained access control.
- Implement authorization checks in controllers using `$this->authorize()` or Gates.

---

## 🌐 RESTful API Requirements

Implement the following API endpoints under `/api/v1/`:

| Endpoint | Method | Access | Description |
|-----------|--------|---------|-------------|
| `/projects` | GET | Admin, Manager | List all projects |
| `/projects` | POST | Manager, Admin | Create new project |
| `/projects/{id}` | GET | Manager, Admin | Show project details with tasks |
| `/tasks` | POST | Manager | Create a new task |
| `/tasks/{id}` | PUT | Manager, Employee | Update task details or status |
| `/tasks/{id}` | DELETE | Manager, Admin | Delete a task |

### Requirements:
- Use **Form Request** classes for validation.
- Use **Laravel API Resources** for JSON formatting.
- Handle exceptions gracefully with proper status codes.

---

## 🎨 Frontend (Blade + Bootstrap)

### Requirements:
- Use **Laravel Blade** templating with **Bootstrap 5** styling.
- Create a common layout (`layouts/app.blade.php`) with navigation.
- Role-based dashboards:
  - **Admin Dashboard:** Overview of all users, projects, and tasks.
  - **Manager Dashboard:** List of projects they manage + option to assign tasks.
  - **Employee Dashboard:** List of tasks assigned to them + status update option.
- Highlight overdue tasks in red.
- Optional: Use modal forms for creating/editing tasks.

---

## 🧰 Middleware & Dynamic Routes

- Create **role-based middleware** for:
  - `/admin/*` → Admin only  
  - `/manager/*` → Manager only  
  - `/employee/*` → Employee only  
- Use **Route Model Binding** for dynamic routes:
  - Example: `/projects/{project}/tasks/{task}`

---

## 🧪 Bonus / Advanced Features (Optional)

If you have extra time, implement any of the following:
- Task **search/filtering** by status, due date, or assigned user.
- **Soft Deletes** for tasks and projects.
- **Notifications** (email or database) when a new task is assigned.
- **Activity Logs** (e.g., task status updates).

---

## 📦 Deliverables

1. A fully functional Laravel project built from scratch.
2. A working database schema with migrations and seeders.
3. Clean and modular code (Service layer, Policies, Middleware, etc.).
4. RESTful APIs working with Postman.
5. Responsive Blade front-end using Bootstrap 5.
6. README file describing:
   - Setup instructions  
   - Test credentials (Admin, Manager, Employee)  
   - API endpoints list  

---

## 🧮 Evaluation Criteria

| Category | Marks | Key Skills |
|-----------|--------|------------|
| Authentication & Roles | 15 | Auth, redirection, seeding |
| Authorization & Middleware | 15 | Role-based policies, access control |
| Database Design | 10 | Relationships, migrations |
| Services & Logic Layer | 15 | Code architecture, reusability |
| RESTful APIs | 20 | Resource, validation, error handling |
| Blade Frontend | 15 | UI, conditional views, layouting |
| Code Quality | 10 | PSR-12, naming, readability |
| Bonus Features | 10 | Creativity & completeness |
| **Total** | **110** | — |

---

## 🚀 Submission Instructions

1. **Clone** this repository to your local machine.  
2. Build your project **from scratch** using the latest Laravel version.  
3. Commit your progress frequently (we’ll check commit history).  
4. Once done:
   - Push your code to a **public GitHub repo**.  
   - Share the repository link.  

> ⚠️ Do not upload the `vendor` folder or `.env` file.  
> Use `.env.example` with dummy credentials.

---

## 🧠 Key Evaluation Focus
- Code readability and architecture  
- Proper use of Laravel features (Middleware, Policies, Services, Resources)  
- Database design and data integrity  
- Frontend usability  
- Problem-solving approach and logical separation  

---

**Good luck!**  
Design it like a real-world application — modular, maintainable, and clean.
