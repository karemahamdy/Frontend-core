# Access Control Module — ERD & API Documentation (Markdown)

## 📌 Overview

This document summarizes the **ERD (Entity Relationship Diagram)** and **REST API Design** for the **Access Control Module** in the Tera ERP system.

---

# 🧩 1. Entity Relationship Diagram (ERD)

## **1.1 ERD Structure (Text Representation)**

```
Tenant (1) ──── (∞) User
Tenant (1) ──── (∞) Branch
Tenant (1) ──── (1) License

Branch (1) ──── (∞) User

User (1) ──── (∞) Session

User (∞) ──── (∞) Role
   through UserRole table

Role (∞) ──── (∞) Permission
   through RolePermission table

UserGroup (1) ──── (∞) User
UserGroup (1) ──── (∞) Role   (Roles assigned to groups)
```

---

## **1.2 Entities & Fields**

### **Tenant**

* TenantID (PK)
* Name
* LicenseID (FK)
* CreatedAt

### **Branch**

* BranchID (PK)
* TenantID (FK)
* BranchName
* Address

### **User**

* UserID
* FullName
* Username
* PasswordHash
* Email
* Department
* Status (Active / Inactive / Locked)
* TenantID (FK)
* BranchID (FK)
* UserGroupID (FK)
* Scope (Global / Branch)

### **UserGroup**

* GroupID
* GroupName
* TenantID

### **Role**

* RoleID
* RoleName
* Description

### **Permission**

* PermissionID
* Module
* Action
* Description

### **RolePermission**

* RoleID
* PermissionID

### **UserRole**

* UserID
* RoleID

### **Session**

* SessionID
* UserID
* TenantID
* StartTime
* ExpiryTime
* Status

### **License**

* TenantID
* MaxUsers
* MaxSessions

---

# 🌐 2. REST API Design

Below are the endpoints for authentication, user/role/permission management, session control, and branch access.

---

# 🔐 2.1 Authentication API

### **POST /api/auth/login**

* Input: username, password
* Output: JWT token, refresh token
* Validates license limits & concurrent sessions

### **POST /api/auth/logout**

Ends current user session.

### **POST /api/auth/refresh**

Returns new token.

---

# 👤 2.2 User Management API

### **GET /api/users**

List users for the tenant (filter by branch).

### **POST /api/users**

Create a new user.

### **GET /api/users/{id}**

Retrieve single user.

### **PUT /api/users/{id}**

Update user.

### **PATCH /api/users/{id}/status**

Activate / deactivate / lock.

### **DELETE /api/users/{id}**

Delete user.

---

# 🧩 2.3 User Group API

### **GET /api/user-groups**

### **POST /api/user-groups**

### **PUT /api/user-groups/{id}**

### **DELETE /api/user-groups/{id}**

### **POST /api/user-groups/{id}/assign-user**

Assign user to group.

### **POST /api/user-groups/{id}/assign-role**

Assign role to group.

---

# 🛡 2.4 Roles API

### **GET /api/roles**

### **POST /api/roles**

### **PUT /api/roles/{id}**

### **DELETE /api/roles/{id}**

---

# 🔐 2.5 Permissions API

### **GET /api/permissions**

### **POST /api/permissions**

### **PUT /api/permissions/{id}**

### **DELETE /api/permissions/{id}**

---

# 📌 2.6 Role–Permission Mapping

### **POST /api/roles/{roleId}/permissions**

Assign permissions to role.

### **GET /api/roles/{roleId}/permissions**

Retrieve permissions assigned to role.

---

# 👥 2.7 User–Role Mapping

### **POST /api/users/{userId}/roles**

Assign role to user.

### **GET /api/users/{userId}/roles**

Get user roles.

---

# 🌿 2.8 Branch Access API

### **GET /api/branches**

List branches for tenant.

### **POST /api/branches**

Create branch.

### **PATCH /api/users/{userId}/scope**

Set user access scope (Global / Branch-specific).

---

# 🎫 2.9 License API

(Access Control reads from License Module)

### **GET /api/license**

Returns:

* maxUsers
* maxSessions
* current active users
* current sessions

---

# 📡 2.10 Session API

### **GET /api/sessions**

List active sessions.

### **DELETE /api/sessions/{sessionId}**

Force logout.

---
Api format 

{
  "token": "<jwt-token>",
  "refreshToken": "<refresh-token>",
  "session": {
    "sessionId": "string",
    "startTime": "2025-11-18T12:00:00",
    "expiryTime": "2025-11-18T14:00:00",
    "status": "Active"
  },
  "user": {
    "userId": "string",
    "fullName": "string",
    "username": "string",
    "email": "string",
    "department": "string",
    "status": "Active",
    "scope": "Global | Branch",
    "tenantId": "string",
    "branchId": "string",
    "branch": {
      "branchId": "string",
      "branchName": "string",
      "address": "string"
    },
    "groups": [
      {
        "groupId": "string",
        "groupName": "string"
      }
    ],
    "roles": [
      {
        "roleId": "string",
        "roleName": "string",
        "description": "string"
      }
    ],
    "permissions": [
      {
        "permissionId": "string",
        "module": "string",
        "action": "Create | View | Edit | Delete | Approve",
        "description": "string"
      }
    ]
  },
  "tenant": {
    "tenantId": "string",
    "tenantName": "string",
    "license": {
      "maxUsers": 20,
      "maxSessions": 10,
      "currentActiveUsers": 8,
      "currentActiveSessions": 4
    }
  },
  "uiConfig": {
    "sidebar": [
      { "module": "Sales", "allowed": true },
      { "module": "Inventory", "allowed": false },
      { "module": "Manufacturing", "allowed": true },
      { "module": "HR", "allowed": true }
    ]
  }
}

# ✅ End of Document
