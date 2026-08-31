

## 1. Introduction

The purpose of this data model is to define the main information that the Internal Operations Service Hub needs to store, how this information is connected, and the rules that must be maintained.

The main entities are Users, Departments, Requests, Comments, Roles, and Request History.

---

## 2. Main Entities

### User

A User represents an employee who can access the system.

Important fields:

- id
- employee_id
- name
- email
- active status

A user can have one or more roles in the system.

The possible roles are:

- Employee
- Department Staff
- Manager
- Administrator

---

### Department

A Department represents an internal company service such as IT, HR, or Finance.

Important fields:

- id
- name
- code
- active status

One department can receive many requests.

Each request belongs to one department.

---

### Request entity

A Request represents a support or service request created by an employee.

Important fields:

- id
- request_number
- requester_id
- department_id
- title
- description
- status
- created_at
- updated_at
- resolved_at
- closed_at

Every request belongs to one employee and one department.

The request number must be unique.

A newly created request starts with the status Open.

---

### Comment

A Comment represents a comment or note added to a request.

Important fields:

- id
- request_id
- author_id
- comment
- created_at

One request can have many comments.

Each comment belongs to one request and has one author.

Comments are visible to the requester and authorized department users.
Private staff-only notes are not included.

---

### Request History

Request History records important changes made to a request.

Important fields:

- id
- request_id
- changed_by
- previous_status
- new_status
- created_at
- event-type
This allows the system to keep track of the progress of a request.

---

### User Role Assignment

A User Role Assignment associates a User with a role and,
when required, a Department.

Important fields:

- id
- user_id
- role
- department_id
- created_at

The supported roles are:

- Employee
- Department Staff
- Manager
- Administrator

The department_id is required for Department Staff and Manager assignments.

Employee and Administrator assignments do not require a department.

---

## 3. Relationships

The main relationships are:

- One User can create many Requests.
- One Request belongs to one User.
- One Department can have many Requests.
- One Request belongs to one Department.
- One Request can have many Comments.
- One Comment belongs to one Request.
- One User can create many Comments.
- One Request can have many Request History records.
- One User can have one or more roles.



## 4. Request Lifecycle

The request can have the following statuses:

- Open
- In Progress
- Waiting for Information
- Resolved
- Closed

The normal lifecycle is:

Open  
↓  
In Progress  
↓  
Waiting for Information  
↓  
In Progress  
↓  
Resolved  
↓  
Closed

A new request always starts as Open.

Department Staff can change the status while processing the request.

A Closed request cannot be reopened in the Firstversion.

---

## 5. Business and Authorization Rules

The following rules must always be maintained:

- Every Request must have one requester.
- Every Request must belong to one department.
- Every Request must have a valid status.
- New Requests start with the Open status.
- Employees can create Requests.
- Employees can view their own Requests.
- Employees cannot update the processing status of their Requests.
- Department Staff can access and process Requests belonging to their department.
- Managers can view Requests belonging to their department.
- Administrators manage users, departments, roles, and system configuration.
- Unauthorized users must not be able to access Requests they are not permitted to view.
- Closed Requests cannot be reopened in Firstversion.

---

## 6. Storage model

The following information must be stored permanently:

- Users
- User Roles
- Departments
- Requests
- Current Request Status
- Comments
- Request History



The Internal Operations Service Hub will use a relational data model.

A relational database is appropriate because the system contains structured entities with clear relationships between Users Departments, Role Assignments, Requests,Comments, and Request History.

A relational model also provides strong consistency for important operations such as Request creation, status changes, and authorization relationships.

Examples include:

- My Requests
- Number of Open Requests
- Department Request Queue
- Requests grouped by status
- Manager Overview
- Number of comments on a Request

These values can be produced using database queries.

A relational database is appropriate because the system has clear relationships between Users, Departments, Requests, Comments, and Roles.

---

## 7. Important Access Patterns

### Employee

The system needs to support queries for:

- Viewing all Requests created by the employee.
- Filtering the employee's Requests by status.
- Opening one Request and viewing its details and comments.

### Department Staff

The system needs to support queries for:

- Viewing Requests belonging to their department.
- Filtering department Requests by status.
- Opening a Request.
- Updating the Request status.
- Adding comments.

### Manager

The system needs to support queries for:

- Viewing Requests belonging to their department.
- Viewing Requests grouped by status.
- Identifying Requests that are still pending.

### Administrator

The system needs to support queries for:

- Viewing and managing Users.
- Viewing and managing Departments.
- Managing User Roles and permissions.

---

## 8. Indexes

Indexes should only be added where they support important system queries.

Useful indexes include:

- Request requester_id and status.
- Request department_id and status.
- Comment request_id.
- Request History request_id.
- Request request_number.

These indexes support the most common Employee and Department Staff operations.

---

## Consistency Rules

Important operations should preserve data consistency.

When a Request is created, the Request record and its initial History entry
should either both be stored successfully or both fail.

When the status of a Request changes, the current Request status
and the corresponding Request History entry should be updated together.

This prevents the current Request state and its History from becoming inconsistent.


---

## Unknowns

The following data-model questions remain open for future clarification:

- Can a User hold department-scoped roles in multiple Departments?
- Can an existing Request be transferred from one Department to another?
- Will private staff-only notes require a separate model or visibility rule?
- Can a Manager oversee multiple Departments?
- What format should be used for the human-readable Request number?
- How long should closed Requests and Request History be retained?
- Should inactive Users and Departments ever be permanently deleted?

## 9. Firstversion Decisions

For the first version of the Internal Operations Service Hub:

- A Request belongs to only one Department.
- Attachments are not included.
- Email and system notifications are not included.
- Closed Requests cannot be reopened.
- Managers can view Requests from their own Department.
- External customers are not supported.
- Employees cannot change the processing status of Requests.

