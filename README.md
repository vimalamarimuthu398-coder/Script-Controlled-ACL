# Script-Controlled ACL – Restrict Record Access Based on Field Value

## Project Overview

This project demonstrates how to implement Script-Controlled Access Control Lists (ACLs) in ServiceNow to restrict users from accessing records based on user roles and field values.

In this project, users are given different custom roles such as `bb1`, `bb2`, `bb3`, and `bb4`. Access to the **Institution Details** table is controlled using READ, CREATE, WRITE, and DELETE ACLs.

The READ ACL restricts users so that only users with the required role can access the permitted records, while administrators retain full access.

## Objectives

- Understand Access Control Lists (ACLs) in ServiceNow.
- Create custom users and roles.
- Create a custom table for institution details.
- Implement record-level access control.
- Implement READ, CREATE, WRITE, and DELETE ACLs.
- Control access based on user roles and record field values.
- Verify access permissions for different users.

## Technologies Used

- ServiceNow
- ServiceNow ACL
- JavaScript
- GitHub

## User Roles

| Role | Access Granted |
|------|-----------------|
| `bb1` | Read access |
| `bb2` | Create access |
| `bb3` | Write access |
| `bb4` | Delete access |

Administrators have full access to all records regardless of role.

## Custom Table

A custom table named `u_institution_details` is created in ServiceNow.

### Table Fields

| Field | Type |
|-------|------|
| Student Roll Number | Auto Number |
| Student Name | Reference (User) |
| Faculty Name | Reference (User) |
| Branch | Choice (ECE, EEE, CSE) |
| Email | String |
| Phone Number | String |
| Description | Multi String |

## ACL Implementation

### 1. READ ACL

A record-level READ ACL is created for the `u_institution_details` table.

The ACL uses the `bb1` role along with a data condition where **Branch = EEE**.

The script allows administrators full access and allows users with the required role to access the records.

```javascript
(function () {
    // Allow admin users full access
    if (gs.hasRole('admin')) {
        return true;
    }

    // Allow only EEE branch users to see EEE records
    if (gs.hasRole('bb1')) {
        return true;
    }

    // Deny access for all others
    return false;
})();
```

### 2. CREATE ACL

A record-level CREATE ACL is created for the `u_institution_details` table.

- The `bb2` role is added to the ACL.
- Users with the required role can access the **New** button and create records.

### 3. WRITE ACL

A record-level WRITE ACL is created for the `u_institution_details` table.

- The `bb3` role is added to the ACL.
- Users with the required role can view and edit the permitted records.

### 4. DELETE ACL

A record-level DELETE ACL is created for the `u_institution_details` table.

- The `bb4` role is added to the ACL.
- Users with the required role can delete the permitted records.

## Access Control Flow

| Roles Assigned | Access Level |
|-----------------|--------------|
| Admin | Full access |
| `bb1` | Read |
| `bb1` + `bb2` | Read, Create |
| `bb1` + `bb2` + `bb3` | Read, Create, Write |
| `bb1` + `bb2` + `bb3` + `bb4` | Read, Create, Write, Delete |

## Verification

The ACLs are tested by impersonating different users and accessing the Student Records list. The following access conditions are verified:

- Users with the required read role can view the permitted records.
- Users without the required role cannot access the records.
- Administrators can access all records.
- Users with create permission can create records.
- Users with write permission can edit records.
- Users with delete permission can delete records.

## Project Outcome

This project provides an understanding of how Script-Controlled READ, WRITE, CREATE, and DELETE ACLs can be used to enforce record-level security in ServiceNow.

It demonstrates how user roles and record field values can be evaluated to control access to sensitive data across forms and lists.

## Team Members

- Vimala M
- Viswa Bharathi N
- Yasmin Asmath S
- Yuvasri T

## GitHub Repository

This repository contains the project files, implementation details, screenshots, and supporting documentation for the Script-Controlled ACL project.
