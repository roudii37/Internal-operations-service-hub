Internal Operations Service Hub – Architecture

## Introduction

The Internal Operations Service Hub is intended to provide the employees with a unified place
to post their requests and track their progress.
The architecture is primarily dictated by the requirement for the employee to be able to submit
a request to the desired department and for the staff to be able to process these requests accordingly.
Hence, the architecture should encompass the following capabilities:
Authentication and authorization:
Request creation
Selecting the appropriate department
Routing of the request
Tracking the request
Updating the status
Adding comments or notes
Access control between employees, staff, managers, and administrators
The service is supposed to be hosted internally and accessible only to the company’s employees.

## Actors
There are four types of actors interacting with the Internal Operations Service Hub.

-An employee is the one creating requests and tracking their progress.
Responsibilities include:
Logging in
Creating a request
Specifying the department
Providing the title and description
Opening a request to view details
Viewing the progress
Reading comments
An employee should only be able to view requests that they created.

-Department staff are responsible for processing the request in the relevant departments.
Each department (IT, Finance, HR) has its staff responsible for resolving the request.
Responsibilities include:
Viewing the list of requests
Opening a request to view details
Updating the status
Viewing and providing comments
Closing or resolving the request
Unless otherwise stated, the staff should only have access to the requests in their department.

-Managers are responsible for overseeing the processing of requests.
Their responsibilities may include:
Viewing requests
Viewing the status of requests to ensure nothing is left pending

Managers are responsible for overseeing the processing of requests in their department.

Responsibilities include:

- Viewing requests belonging to their department
- Monitoring request status
- Identifying requests that remain pending

A Manager's access is limited to the department they manage.

-An administrator is responsible for configuring the system and managing its global settings.
Responsibilities may include:
User management
Department management
Request configuration
Permission settings
Access control management
Other administrative tasks
The administrator is not directly involved in processing employee requests.

## System Boundary

The Internal Operations Service Hub is a system designed and hosted internally.
The following elements fall inside the system boundary:
User authentication
User roles
Request creation
Request routing to departments
Displaying of requests
Status management
Comments
Access control
History of requests
Administrative configuration

The following elements fall outside the system boundary:
Actual IT support services
Actual processing of HR-related requests
Actual processing of Finance-related requests
Customer requests processing
Business processes peculiar to each department
Email system
Advanced analytics
Data mining

## Components

4.1 User Interface

The User Interface component contains all the screens visible to the end-users. 
The interface is dynamic and depends on the user interacting with the system.
For example, the following UI elements are available to the user:

Login screen
Request submission form
My Requests screen
Request Details screen
Departments List
Manager overview
Administration section

4.2 Authentication and Authorization

This component is responsible for identifying the user
and defining what this user is allowed to do in the system.

In other words, this component should ensure that only the authorized
users access the system and that these users only perform the tasks they are allowed to perform.

Authorization must be enforced by the backend and must not rely solely on hiding or disabling functionality in the User Interface.

4.3 Request Management

The Request Management component is the core of the system.

It encompasses the business logic concerning the creation, processing, resolving, and closing of requests. This component is responsible for:
Creating requests
Generating request identifiers
Validating the request data
Storing request data
Retrieving request data
Updating the status
Updating the request data
Adding comments
Closing or resolving requests
Recording significant request status changes in Request History.
4.4 Department Management

The Department Management component is responsible for maintaining the list of departments
and the logic for assigning requests to departments.

4.5 User and Role Management

This component is responsible for maintaining the information about Employees, Department staff, Managers, and Administrators.
It keeps track of who belongs to which department,
who has access to what information, and who can perform which actions.

4.6 Request Storage

The system needs a persistent data store to keep the information about employee requests.
This component is responsible for:
Storing the request
Retrieving the request
Updating the request
Keeping track of the request’s status
Keeping track of comments and notes

The exact structure of the database or databases is beyond the scope of this document,
but the system should be designed in such a way that the request contains the necessary
information to be processed and resolved.
At a minimum, the request should have the following fields:

Unique request identifier
Employee
Department
Title
Description
Creation date
Status
Comments
History

## External Dependencies

The system should have as few external dependencies as possible.

One possible external dependency is the employee directory or authentication service
if the company has one. In other words, the Internal Operations Service Hub
may rely on another service for employee identification and authentication.
Email and notification services are outside the scope and therefore are not required dependencies for the initial release.

## Main Flow

The main flow of the Internal Operations Service Hub starts with the employee creating a request.

1. Authentication

An employee authenticates themselves to the Internal Operations Service Hub.

2. Request Creation

The employee opens a form to create a request and selects the department. The employee provides the following information:

Request title

Request description

Other required information

3. Validation

The information provided by the employee is validated by the Request Management component. If the request is valid,
the system proceeds to step 4; otherwise, the employee is notified of the required changes.

4. Request Registration

A request is created and assigned a unique request identifier. The status is set to Open.

5. Department Routing

The request is routed to the selected department. For example, if an employee selects IT,
the request becomes visible to the IT staff. Once the request is assigned to the relevant staff, it can be processed.

6. Staff Processing

The staff opens the request and updates the status from Open to In Progress.
The staff can also add comments or notes.

7. Employee Tracking

The employee opens the My Requests page to view the status of their request.
In doing so, the employee can see that their request has moved from Open to In Progress.

8. Resolving

Once the staff has resolved the issue, they can update the status to Resolved -> Closed and add a comment.

9. Final Employee View

The employee views the updated status and can see that the request has been resolved.

## Information Flow

The main information flow for both Employees and Department Staff is:

User
- User Interface
- Backend Authentication / Authorization
- Request Management
- Request Storage

Employees use this flow to create and retrieve their Requests.

Department Staff use the same flow to retrieve department Requests,
update their status, and add Comments.

All authorization checks are performed before protected Request data is returned or modified.

## Trust and Authorization Boundaries

The Internal Operations Service Hub typically stores and processes sensitive or confidential information;
hence, these trust and authorization boundaries are of particular importance.


-Employee Trust/Authorization Boundary
An employee should be able to:
Create a request
View their requests
See comments for their requests


-Department Trust/Authorization Boundary

A department staff should only be able to see and process the requests for their department.
For example, IT staff should only be able to process IT-related requests.

-Manager Trust/Authorization Boundary

Managers have an extended set of viewing permissions to be able to oversee the progress of requests.

-Administrator Trust/Authorization Boundary

Administrators have extended permissions to configure the system.
These permissions should be clearly segregated from the rest of the system’s permissions.

## Failure Scenarios

The system should gracefully handle the following failure scenarios.

-Invalid Request

If a user tries to submit an invalid request (e. g., missing required fields), the system should reject the request and inform the user of all the required changes.

-Unauthorized Access

If a user tries to access unauthorized information, the system should deny access.

-Invalid Department

If a user tries to submit a request to an invalid department, the system should reject the request and inform the user.

-Request Update Failure

If a department staff tries to update a request but the system fails to save these updates,
the request should remain unchanged. The user should be informed that the system failed to update the request.

-Temporary System Failure

As the Internal Operations Service Hub is supposed to be constantly available to the employees,
the system should handle temporary failures gracefully. In the case of a subsystem failure,
the system should fail gracefully and inform the employees instead of failing catastrophically and losing data.

## Architectural Decisions

-Decision 1: Centralized request management
All internal service requests will be managed in one central place.
Impact:
This decision simplifies the system and makes it easier to use. It also prevents employees from contacting different services via different means.
Reason:
The product specification requires the system to standardize how internal service requests are managed.

-Decision 2: Department-scoped role-based access control
Department Staff and Managers receive access according to both their roleand their associated department.
Impact:
Each user type will have different features available to them.
Reason:
Each user type has significantly different responsibilities and should only have access to the features pertaining to their duties.

-Decision 3: Department-based routing
Every request in the system will be associated with a department.
Impact:
Department staff will have a unified way to view and process the requests assigned to them.
Reason:
The system needs to ensure that the requests are appropriately assigned to the staff capable of resolving them.

-Decision 4: Persistent status
The system will maintain the status of each request. The status can be:
Open
In Progress
Waiting on information
Resolved
Closed
Impact:
The status will be visible to users authorized to access that request.
Reason:
The product specification requires that the employee is always aware of the status of their request. Hence, the system must always store the latest status.

-Decision 5: Authorization enforced by the system
The system will enforce authorization policies. In other words,
the system will restrict the users from performing unauthorized actions
even if these users have the technical capability to perform them.
Impact:
The system will be more secure.
Reason:
The product specification requires that the users only have access to the information they are supposed to have.


![Internal Operations Service Hub Archetecture](internalservice.drawio.png)