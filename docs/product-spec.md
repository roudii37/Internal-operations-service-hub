                                Internal Operations Service Hub

## Problem
In many companies, employees can contact different services in various ways.
Therefore, the correspondence can be difficult to track.
The proposed solution will introduce a unified platform for requesting the 
services covered by the Internal Operations Service Hub.
It will allow the employees to follow the progress of the request and the
service desks to organize the work and manage the tasks effectively.

## Facts
The Internal Operations Service Hub will be used by the company’s employees to 
request the help of various services. Therefore, the software will be available
in the intranet and cover the popular departments, such as IT, HR, Finance, and others.
The employees will be able to fill out a request form and provide the necessary
information to track the request. The service desk personnel will manage the task
and update the status accordingly. The main aim of the system is to standardize
the process of requesting and managing the services within the firm.

## Users and Stakeholders

The users of the Internal Operations Service Hub will be divided into four groups:
employees, department staff, managers, and the system administrator.
The employees will use the system to submit support requests,
choose the appropriate department, and track the progress of their requests.
They will be able to sort the list of their requests according to their status
and open the necessary requests to review the details.
The staff of the chosen departments will be able to view, update,
and manage the employee’s request. They will be able to sort the list
of requests according to their status and open the necessary requests to review the details.
The managers will use the system to oversee the progress of the tasks
and ensure that nothing is left unattended.
The system administrator will manage the software’s settings,
including the user management, department setup, request configuration, and access control.

## Functional Requirements
The Internal Operations Service Hub will enable its users to perform the following tasks:
Employees will be able to create a new support request, choosing the necessary department.
Moreover, the users will enter a short description of the problem and submit the request.
They will also be able to view their past requests, open the necessary request to check the status,
and ensure that the task is resolved or closed.
The staff will be able to view the list of the requests in their department.
They will be able to open each request and examine the details and the necessary information
provided by the employee.
Department staff will update the status of the request and add their comments or notes,if necessary.
They will close or resolve the request if the problem is solved.
Each request will have a particular status, which will indicate its progress.
The status will also include the request ID, the name of the employee who created the request,
the date when the request was created, the selected department, the request title, and the comments,
if any.

## Non-Functional Requirements
The system will be easy to navigate and understand,even for those who are not familiar
with the technical aspects of the software.
The Internal Operations Service Hub will be available to the employees 24/7,
as it will be in the company’s intranet.
The data will be protected, and only the authorized personnel
will have access to the relevant information.
The information will be well-structured and presented in a comprehensible manner.
The system will function efficiently without additional automation and complexity.

## Assumptions
The following assumptions will be considered while developing the system.
First, all the employees will have their accounts,
which will be used to authorize and access the system.
Second, all the requests will be managed by the relevant departments.
The department staff will update the status of the request if it is in their department.
Moreover, the employees will provide all the necessary information when submitting a request.
The managers and administrators will have more access to the system’s features than the employees.

6.1 Constraints
The Internal Operations Service Hub will only be available to the employees of the company.
The software will not be used for external customers.
The first version of the system will only include the basic features,
such as creating and managing the support requests.
The system will not replace the existing work flows of the company’s departments.


6.2 Unknowns
The following questions need to be clarified before developing the system.
What statuses will the system include?
The options can be Open, In Progress, Waiting for Information, Resolved, Closed.
Will the users be able to send a request to multiple services?
Will the employees be able to attach screenshots or documents to the request?
Will the users receive email or system notifications about the request updates?
Can the employees reopen a closed request?
Will the managers have access to the entire list of requests or only the ones in their department?

## Non-Goals
The initial release of the Internal Operations Service Hub will not include the following features:
The software will not replace the entire work flow of the departments,
such as the existing procedures in IT, HR, Finance.
The system will not make decisions on behalf of the department staff.
The system will not be used for the requests from the external customers.
The software will not function as a chat or communication tool.

## Acceptance Criteria
The Internal Operations Service Hub will be delivered when:
An employee can successfully submit a request to a specific department.
The request will have a unique ID after submission.
The employee will be able to view their request in their request list.
The employee can view the request status ,authorized department staff can update it.
The department staff will be able to access the list of the requests in their department.
The staff will update the status of the employee’s request and add their comments or notes, if required.
The employees will be able to easily determine whether their request is open, resolved, or closed.
The users will not be granted access to the information or requests
that they should not see, depending on their access level.

An Example Scenario:
An employee has a problem with their company laptop.
Instead of contacting the IT department via email,
they open the Internal Operations Service Hub.
The user selects the IT department, enters a short request title,
and describes their problem.
After submitting the request form, the system will generate a request ID
and add the request to the list of pending requests.
The employee will see the request in their request list with the Open status.
The IT staff will access the Internal Operations Service Hub and review the list of pending requests.
After examining the details of the request, they will update the status to In Progress.
The employee will be able to see the updated status in their request list.
Eventually, the IT staff will resolve the problem with the laptop
and update the request status to Resolved or Closed.
They will also add a short comment to indicate that the request is done.