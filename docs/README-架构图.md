# Authorization & Access Control Design

## 1. Background and Objectives

This document describes the design of the authorization model used across the platform.

The primary objectives are:

- Prevent direct coupling between users and system roles
- Separate authorization logic from organizational structure
- Provide a clear, auditable, and user-friendly permission model
- Enforce strict data and organizational boundaries
- Support long-term scalability across multiple Business Units (BUs)

---

## 2. Design Principles

The authorization model is based on the following principles:

- Users never receive permissions directly
- Roles define system capabilities, not user assignments
- Authorization must be explainable and auditable
- Organizational boundaries must be enforced consistently
- Permission evaluation must be deterministic and predictable

---

## 3. Core Concepts

| Concept | Description |
|------|-------------|
| User | An authenticated identity within the system. Users do not directly own roles or permissions. |
| Visual Group | A user-facing authorization group. Each Visual Group maps to exactly one Role. |
| Role | A system-defined set of permissions representing a capability. Roles are not user-facing. |
| Permission | An atomic system operation that can be executed by the platform. |
| Business Unit (BU) | An organizational boundary defining data scope and role eligibility. |
| Eligible Role | A governance rule that defines which roles may be used within a BU. |

---

## 4. High-Level Authorization Model

Authorization follows a strict and linear flow:

User → Visual Group → Role → Permission

Business Units apply constraints to this flow but never grant permissions themselves.

- Visual Groups are the only mechanism through which users gain access
- Roles define what actions are possible
- Permissions represent executable system operations
- Business Units restrict where and when permissions are effective

---

## 5. Authorization Flow Description

1. A User is assigned to one or more Visual Groups
2. Each Visual Group is associated with exactly one Role
3. The Role determines the set of Permissions available
4. The active Business Unit defines:
   - The data scope accessible to the user
   - The set of roles that are eligible within that scope
5. A permission is effective only when all conditions above are satisfied

---

## 6. Business Unit Responsibility Model

Business Units are explicitly **non-authoritative** with respect to permissions.

A Business Unit is responsible for:

- Defining data access scope (e.g. subtree, region, department)
- Defining which roles are eligible within that scope

A Business Unit does **not**:

- Assign roles to users
- Grant permissions directly
- Modify role definitions

---

## 7. Effective Permission Evaluation

At runtime, permissions are evaluated using the following logic:

- Collect all Roles derived from the User’s Visual Groups
- Filter Roles based on the current Business Unit’s eligible roles
- Resolve Permissions from the remaining Roles
- Restrict data access according to the Business Unit scope

Any failure in this chain results in access denial.

---

## 8. Example Scenario

User configuration:

- User: Alice
- Visual Group: Order Editor
- Active Business Unit: SG BU

Business Unit configuration:

- Eligible Roles: ORDER_VIEW, ORDER_EDIT
- Scope: SG BU subtree

Effective result:

- Alice can view and edit orders within the SG BU scope
- If Alice switches to a different BU where ORDER_EDIT is not eligible, edit permissions are automatically revoked
- No reassignment of roles or groups is required

---

## 9. Security and Governance Benefits

This design provides the following benefits:

- Clear separation between identity, capability, and governance
- Reduced risk of permission leakage across organizational boundaries
- Strong alignment between UI representation and actual permissions
- Predictable authorization behavior
- Simplified audit and compliance analysis

---

## 10. Change Impact Analysis

| Change Type | Impact |
|-----------|-------|
| Role modification | Affects all Visual Groups bound to the role |
| Visual Group membership change | Affects only assigned users |
| BU eligible role change | Affects only users operating under that BU |
| BU scope change | Affects data visibility only |

This ensures changes have a controlled and well-understood blast radius.

---

## 11. Visualization

The authorization model is visualized using Draw.io diagrams embedded in Confluence, including:

- Business Unit hierarchy
- Permission flow (User → Visual Group → Role → Permission)
- Explicit indication of BU scope and role eligibility constraints

---

## 12. Summary

Users never receive permissions directly.

Permissions flow through Visual Groups and Roles, while Business Units strictly enforce organizational and data boundaries.

This model ensures security, clarity, and scalability across the platform.
