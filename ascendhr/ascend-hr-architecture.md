# AscendHR - DynamoDB Architecture

> Alternative to PostgreSQL using DynamoDB (NoSQL)

---

## Why DynamoDB for Lambda?

| Feature | DynamoDB | PostgreSQL |
|---------|----------|------------|
| Cold start | ✅ Instant connection | ⚠️ Needs connection pool |
| Scaling | ✅ Auto-scale | ⚠️ Manual scaling |
| Cost | ✅ Pay per request | 💰 Always running |
| Schema | ⚠️ Flexible (careful!) | ✅ Strict |
| Queries | ⚠️ Limited patterns | ✅ Flexible SQL |
| AWS Native | ✅ Best integration | ⚠️ Need RDS/Neon |

**Best for:** Simple queries, high scale, serverless-first

---

## Updated Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         FRONTEND                                │
│                     Vite + React App                            │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API GATEWAY                                │
└───┬─────────┬─────────┬─────────┬─────────┬─────────┬──────────┘
    │         │         │         │         │         │
    ▼         ▼         ▼         ▼         ▼         ▼
┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐ ┌───────┐
│ Auth  │ │Employee│ │  Org  │ │ Leave │ │Announce│ │Report │
│Lambda │ │Lambda  │ │Lambda │ │Lambda │ │Lambda  │ │Lambda │
└───────┘ └───────┘ └───────┘ └───────┘ └───────┘ └───────┘
    │         │         │         │         │         │
    └─────────┴─────────┴────┬────┴─────────┴─────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │    DynamoDB     │
                    │  (Single Table) │
                    └─────────────────┘
```

---

## Tech Stack Update

| Layer | Technology |
|-------|------------|
| Database | **DynamoDB** |
| ORM/Client | **ElectroDB** (schema + type-safe) |
| Schema Control | **ElectroDB Entities** |

---

## Single Table Design

DynamoDB works best with **Single Table Design** - all data in one table with different access patterns.

### Table Structure

```
Table: ascend-hr

Primary Key:
- PK (Partition Key): string
- SK (Sort Key): string

Global Secondary Indexes (GSI):
- GSI1: GSI1PK, GSI1SK (for alternate queries)
- GSI2: GSI2PK, GSI2SK (for more queries)
```

### Entity Patterns

| Entity | PK | SK | Example |
|--------|----|----|---------|
| User | `USER#<id>` | `USER#<id>` | `USER#123` / `USER#123` |
| Employee | `EMP#<id>` | `EMP#<id>` | `EMP#456` / `EMP#456` |
| Employee by Dept | `DEPT#<deptId>` | `EMP#<id>` | `DEPT#eng` / `EMP#456` |
| Department | `DEPT#<id>` | `DEPT#<id>` | `DEPT#eng` / `DEPT#eng` |
| Position | `DEPT#<deptId>` | `POS#<id>` | `DEPT#eng` / `POS#dev` |
| Leave Request | `EMP#<empId>` | `LEAVE#<id>` | `EMP#456` / `LEAVE#789` |
| Leave by Status | `LEAVE#<status>` | `<date>#<id>` | `LEAVE#pending` / `2024-01-15#789` |
| Announcement | `ANN#<id>` | `ANN#<id>` | `ANN#001` / `ANN#001` |

---

## ElectroDB Setup

### Why ElectroDB?

- ✅ Type-safe schema definition
- ✅ Auto-generates PK/SK patterns
- ✅ Validates data before write
- ✅ Simple query API
- ✅ Works great with TypeScript

### Install

```bash
pnpm add electrodb @aws-sdk/client-dynamodb
```

---

## Schema Definitions with ElectroDB

### packages/database/entities/employee.entity.ts

```typescript
import { Entity } from 'electrodb'
import { client } from '../client'

export const EmployeeEntity = new Entity(
  {
    model: {
      entity: 'employee',
      version: '1',
      service: 'ascendhr',
    },
    attributes: {
      id: {
        type: 'string',
        required: true,
      },
      employeeCode: {
        type: 'string',
        required: true,
      },
      firstName: {
        type: 'string',
        required: true,
      },
      lastName: {
        type: 'string',
        required: true,
      },
      email: {
        type: 'string',
        required: true,
      },
      phone: {
        type: 'string',
      },
      departmentId: {
        type: 'string',
        required: true,
      },
      positionId: {
        type: 'string',
        required: true,
      },
      reportsToId: {
        type: 'string',
      },
      status: {
        type: ['active', 'inactive', 'terminated'] as const,
        default: 'active',
      },
      startDate: {
        type: 'string',
        required: true,
      },
      terminationDate: {
        type: 'string',
      },
      avatarUrl: {
        type: 'string',
      },
      roleId: {
        type: 'string',
        required: true,
      },
      createdAt: {
        type: 'string',
        default: () => new Date().toISOString(),
      },
      updatedAt: {
        type: 'string',
        default: () => new Date().toISOString(),
        set: () => new Date().toISOString(),
      },
    },
    indexes: {
      // Primary: Get employee by ID
      byId: {
        pk: {
          field: 'PK',
          composite: ['id'],
          template: 'EMP#${id}',
        },
        sk: {
          field: 'SK',
          composite: [],
          template: 'EMP#PROFILE',
        },
      },
      // GSI1: Get employees by department
      byDepartment: {
        index: 'GSI1',
        pk: {
          field: 'GSI1PK',
          composite: ['departmentId'],
          template: 'DEPT#${departmentId}',
        },
        sk: {
          field: 'GSI1SK',
          composite: ['lastName', 'firstName'],
          template: 'EMP#${lastName}#${firstName}',
        },
      },
      // GSI2: Get employees by status
      byStatus: {
        index: 'GSI2',
        pk: {
          field: 'GSI2PK',
          composite: ['status'],
          template: 'STATUS#${status}',
        },
        sk: {
          field: 'GSI2SK',
          composite: ['startDate', 'id'],
          template: '${startDate}#${id}',
        },
      },
      // GSI3: Get employees by manager
      byManager: {
        index: 'GSI3',
        pk: {
          field: 'GSI3PK',
          composite: ['reportsToId'],
          template: 'MANAGER#${reportsToId}',
        },
        sk: {
          field: 'GSI3SK',
          composite: ['lastName'],
          template: 'EMP#${lastName}',
        },
      },
    },
  },
  { client, table: process.env.TABLE_NAME! }
)
```

### packages/database/entities/leave-request.entity.ts

```typescript
import { Entity } from 'electrodb'
import { client } from '../client'

export const LeaveRequestEntity = new Entity(
  {
    model: {
      entity: 'leaveRequest',
      version: '1',
      service: 'ascendhr',
    },
    attributes: {
      id: {
        type: 'string',
        required: true,
      },
      employeeId: {
        type: 'string',
        required: true,
      },
      leaveTypeId: {
        type: 'string',
        required: true,
      },
      startDate: {
        type: 'string',
        required: true,
      },
      endDate: {
        type: 'string',
        required: true,
      },
      daysCount: {
        type: 'number',
        required: true,
      },
      reason: {
        type: 'string',
      },
      status: {
        type: ['pending', 'approved', 'rejected', 'cancelled'] as const,
        default: 'pending',
      },
      approverId: {
        type: 'string',
      },
      approvedAt: {
        type: 'string',
      },
      rejectionReason: {
        type: 'string',
      },
      createdAt: {
        type: 'string',
        default: () => new Date().toISOString(),
      },
    },
    indexes: {
      // Primary: Get leave request by ID
      byId: {
        pk: {
          field: 'PK',
          composite: ['id'],
          template: 'LEAVE#${id}',
        },
        sk: {
          field: 'SK',
          composite: [],
          template: 'LEAVE#DETAILS',
        },
      },
      // GSI1: Get leaves by employee
      byEmployee: {
        index: 'GSI1',
        pk: {
          field: 'GSI1PK',
          composite: ['employeeId'],
          template: 'EMP#${employeeId}',
        },
        sk: {
          field: 'GSI1SK',
          composite: ['startDate', 'id'],
          template: 'LEAVE#${startDate}#${id}',
        },
      },
      // GSI2: Get leaves by status (for approvers)
      byStatus: {
        index: 'GSI2',
        pk: {
          field: 'GSI2PK',
          composite: ['status'],
          template: 'LEAVE_STATUS#${status}',
        },
        sk: {
          field: 'GSI2SK',
          composite: ['createdAt', 'id'],
          template: '${createdAt}#${id}',
        },
      },
      // GSI3: Get leaves by approver
      byApprover: {
        index: 'GSI3',
        pk: {
          field: 'GSI3PK',
          composite: ['approverId', 'status'],
          template: 'APPROVER#${approverId}#${status}',
        },
        sk: {
          field: 'GSI3SK',
          composite: ['createdAt'],
          template: '${createdAt}',
        },
      },
    },
  },
  { client, table: process.env.TABLE_NAME! }
)
```

### packages/database/entities/department.entity.ts

```typescript
import { Entity } from 'electrodb'
import { client } from '../client'

export const DepartmentEntity = new Entity(
  {
    model: {
      entity: 'department',
      version: '1',
      service: 'ascendhr',
    },
    attributes: {
      id: {
        type: 'string',
        required: true,
      },
      name: {
        type: 'string',
        required: true,
      },
      description: {
        type: 'string',
      },
      parentId: {
        type: 'string',
      },
      isActive: {
        type: 'boolean',
        default: true,
      },
      createdAt: {
        type: 'string',
        default: () => new Date().toISOString(),
      },
    },
    indexes: {
      byId: {
        pk: {
          field: 'PK',
          composite: ['id'],
          template: 'DEPT#${id}',
        },
        sk: {
          field: 'SK',
          composite: [],
          template: 'DEPT#DETAILS',
        },
      },
      // GSI1: List all departments
      all: {
        index: 'GSI1',
        pk: {
          field: 'GSI1PK',
          composite: [],
          template: 'DEPTS',
        },
        sk: {
          field: 'GSI1SK',
          composite: ['name'],
          template: '${name}',
        },
      },
    },
  },
  { client, table: process.env.TABLE_NAME! }
)
```

---

## DynamoDB Client

### packages/database/client.ts

```typescript
import { DynamoDBClient } from '@aws-sdk/client-dynamodb'

export const client = new DynamoDBClient({
  region: process.env.AWS_REGION || 'ap-southeast-1',
})
```

### packages/database/index.ts

```typescript
// Export all entities
export { EmployeeEntity } from './entities/employee.entity'
export { DepartmentEntity } from './entities/department.entity'
export { PositionEntity } from './entities/position.entity'
export { LeaveRequestEntity } from './entities/leave-request.entity'
export { LeaveTypeEntity } from './entities/leave-type.entity'
export { AnnouncementEntity } from './entities/announcement.entity'
export { UserEntity } from './entities/user.entity'
export { RoleEntity } from './entities/role.entity'
```

---

## Using ElectroDB in Services

### apps/api/employee/services/employee.service.ts

```typescript
import { EmployeeEntity } from '@ascend-hr/database'
import { v4 as uuid } from 'uuid'

export const employeeService = {
  // Create employee
  async create(data: CreateEmployeeInput) {
    const id = uuid()
    const employeeCode = await generateEmployeeCode()
    
    const result = await EmployeeEntity.create({
      id,
      employeeCode,
      ...data,
    }).go()
    
    return result.data
  },
  
  // Get by ID
  async getById(id: string) {
    const result = await EmployeeEntity.get({ id }).go()
    return result.data
  },
  
  // List all employees (paginated)
  async list(params: { limit?: number; cursor?: string }) {
    const result = await EmployeeEntity.query
      .byStatus({ status: 'active' })
      .go({
        limit: params.limit || 20,
        cursor: params.cursor,
      })
    
    return {
      data: result.data,
      cursor: result.cursor, // Use for next page
    }
  },
  
  // List by department
  async listByDepartment(departmentId: string) {
    const result = await EmployeeEntity.query
      .byDepartment({ departmentId })
      .go()
    
    return result.data
  },
  
  // List by manager (direct reports)
  async listByManager(managerId: string) {
    const result = await EmployeeEntity.query
      .byManager({ reportsToId: managerId })
      .go()
    
    return result.data
  },
  
  // Update employee
  async update(id: string, data: UpdateEmployeeInput) {
    const result = await EmployeeEntity.patch({ id })
      .set(data)
      .go()
    
    return result.data
  },
  
  // Change status
  async changeStatus(id: string, status: string, terminationDate?: string) {
    const result = await EmployeeEntity.patch({ id })
      .set({ 
        status,
        terminationDate,
      })
      .go()
    
    return result.data
  },
  
  // Search employees (limited in DynamoDB)
  async search(query: string) {
    // DynamoDB doesn't support full-text search
    // Option 1: Use GSI with begins_with
    // Option 2: Use OpenSearch for complex search
    // Option 3: Filter in memory (small dataset only)
    
    const result = await EmployeeEntity.query
      .byStatus({ status: 'active' })
      .go()
    
    // Filter in memory (ok for < 1000 employees)
    const filtered = result.data.filter(emp => 
      emp.firstName.toLowerCase().includes(query.toLowerCase()) ||
      emp.lastName.toLowerCase().includes(query.toLowerCase()) ||
      emp.email.toLowerCase().includes(query.toLowerCase())
    )
    
    return filtered
  },
}
```

### apps/api/leave/services/leave.service.ts

```typescript
import { LeaveRequestEntity } from '@ascend-hr/database'
import { v4 as uuid } from 'uuid'

export const leaveService = {
  // Create leave request
  async createRequest(employeeId: string, data: CreateLeaveInput) {
    const id = uuid()
    
    const result = await LeaveRequestEntity.create({
      id,
      employeeId,
      ...data,
      status: 'pending',
    }).go()
    
    return result.data
  },
  
  // Get pending requests for approver
  async getPendingForApprover(approverId: string) {
    const result = await LeaveRequestEntity.query
      .byApprover({ 
        approverId, 
        status: 'pending' 
      })
      .go()
    
    return result.data
  },
  
  // Get employee's leave history
  async getEmployeeLeaves(employeeId: string, year?: string) {
    let query = LeaveRequestEntity.query.byEmployee({ employeeId })
    
    if (year) {
      query = query.begins({ startDate: year })
    }
    
    const result = await query.go()
    return result.data
  },
  
  // Approve leave
  async approve(id: string, approverId: string) {
    const result = await LeaveRequestEntity.patch({ id })
      .set({
        status: 'approved',
        approverId,
        approvedAt: new Date().toISOString(),
      })
      .go()
    
    return result.data
  },
  
  // Reject leave
  async reject(id: string, approverId: string, reason: string) {
    const result = await LeaveRequestEntity.patch({ id })
      .set({
        status: 'rejected',
        approverId,
        rejectionReason: reason,
      })
      .go()
    
    return result.data
  },
}
```

---

## SST Configuration for DynamoDB

### sst.config.ts

```typescript
import { SSTConfig } from 'sst'
import { Api, Table } from 'sst/constructs'

export default {
  config() {
    return {
      name: 'ascend-hr',
      region: 'ap-southeast-1',
    }
  },
  stacks(app) {
    app.stack(function Stack({ stack }) {
      // DynamoDB Table
      const table = new Table(stack, 'Table', {
        fields: {
          PK: 'string',
          SK: 'string',
          GSI1PK: 'string',
          GSI1SK: 'string',
          GSI2PK: 'string',
          GSI2SK: 'string',
          GSI3PK: 'string',
          GSI3SK: 'string',
        },
        primaryIndex: { partitionKey: 'PK', sortKey: 'SK' },
        globalIndexes: {
          GSI1: { partitionKey: 'GSI1PK', sortKey: 'GSI1SK' },
          GSI2: { partitionKey: 'GSI2PK', sortKey: 'GSI2SK' },
          GSI3: { partitionKey: 'GSI3PK', sortKey: 'GSI3SK' },
        },
      })
      
      // API
      const api = new Api(stack, 'Api', {
        defaults: {
          function: {
            bind: [table],
            environment: {
              TABLE_NAME: table.tableName,
            },
          },
        },
        routes: {
          // Auth
          'ANY /auth/{proxy+}': 'apps/api/auth/index.handler',
          
          // Employee
          'ANY /employees/{proxy+}': 'apps/api/employee/index.handler',
          'GET /employees': 'apps/api/employee/index.handler',
          'POST /employees': 'apps/api/employee/index.handler',
          
          // Organization
          'ANY /departments/{proxy+}': 'apps/api/organization/index.handler',
          'ANY /positions/{proxy+}': 'apps/api/organization/index.handler',
          
          // Leave
          'ANY /leave-types/{proxy+}': 'apps/api/leave/index.handler',
          'ANY /leave-requests/{proxy+}': 'apps/api/leave/index.handler',
          
          // Announcement
          'ANY /announcements/{proxy+}': 'apps/api/announcement/index.handler',
          
          // Report
          'ANY /reports/{proxy+}': 'apps/api/report/index.handler',
        },
      })
      
      stack.addOutputs({
        ApiUrl: api.url,
        TableName: table.tableName,
      })
    })
  },
} satisfies SSTConfig
```

---

## DynamoDB Access Patterns Summary

### Employee Queries

| Query | Index | Key Condition |
|-------|-------|---------------|
| Get by ID | Primary | PK = `EMP#<id>` |
| List by department | GSI1 | GSI1PK = `DEPT#<deptId>` |
| List by status | GSI2 | GSI2PK = `STATUS#<status>` |
| List by manager | GSI3 | GSI3PK = `MANAGER#<managerId>` |

### Leave Request Queries

| Query | Index | Key Condition |
|-------|-------|---------------|
| Get by ID | Primary | PK = `LEAVE#<id>` |
| List by employee | GSI1 | GSI1PK = `EMP#<empId>` |
| List pending (all) | GSI2 | GSI2PK = `LEAVE_STATUS#pending` |
| List for approver | GSI3 | GSI3PK = `APPROVER#<id>#pending` |

---

## DynamoDB Limitations & Workarounds

| Limitation | Workaround |
|------------|------------|
| No full-text search | Use OpenSearch or filter in memory |
| No JOIN | Denormalize data or multiple queries |
| No aggregate (COUNT, SUM) | Maintain counters separately |
| Max 25 items per batch | Split into multiple batches |
| Max 400KB per item | Split large data |

### Example: Maintaining Counters

```typescript
// Counter entity for department headcount
export const CounterEntity = new Entity({
  model: { entity: 'counter', version: '1', service: 'ascendhr' },
  attributes: {
    id: { type: 'string', required: true },
    count: { type: 'number', default: 0 },
  },
  indexes: {
    byId: {
      pk: { field: 'PK', composite: ['id'], template: 'COUNTER#${id}' },
      sk: { field: 'SK', composite: [], template: 'COUNTER' },
    },
  },
}, { client, table: process.env.TABLE_NAME! })

// Increment when adding employee
async function incrementDepartmentCount(departmentId: string) {
  await CounterEntity.update({ id: `dept_${departmentId}` })
    .add({ count: 1 })
    .go()
}
```

---

## Folder Structure Update

```
packages/database/
├── client.ts                 # DynamoDB client
├── index.ts                  # Export all entities
├── entities/
│   ├── employee.entity.ts
│   ├── user.entity.ts
│   ├── department.entity.ts
│   ├── position.entity.ts
│   ├── role.entity.ts
│   ├── leave-type.entity.ts
│   ├── leave-request.entity.ts
│   ├── leave-balance.entity.ts
│   ├── announcement.entity.ts
│   └── counter.entity.ts
└── package.json
```

---

## PostgreSQL vs DynamoDB Comparison

| Feature | PostgreSQL + Drizzle | DynamoDB + ElectroDB |
|---------|---------------------|----------------------|
| Schema control | ✅ Migrations | ✅ Entity definitions |
| Type safety | ✅ Full | ✅ Full |
| Cold start | ⚠️ ~500ms | ✅ ~50ms |
| Complex queries | ✅ Full SQL | ⚠️ Plan indexes |
| Full-text search | ✅ Built-in | ❌ Need OpenSearch |
| Cost (low traffic) | 💰 $15-50/mo | ✅ $1-5/mo |
| Cost (high traffic) | 💰 $50-200/mo | 💰 $10-50/mo |
| Learning curve | ✅ SQL knowledge | ⚠️ New patterns |

---

## Recommendation

| Choose | When |
|--------|------|
| **PostgreSQL** | Complex queries, reports, familiar SQL |
| **DynamoDB** | Simple CRUD, high scale, fastest cold starts |

For **AscendHR** with reports feature → **PostgreSQL is easier**

But if cost and cold start are priority → **DynamoDB works fine**

---

## Quick Start with DynamoDB

```bash
# Install dependencies
pnpm add electrodb @aws-sdk/client-dynamodb

# Create entity file
# packages/database/entities/employee.entity.ts

# Use in Lambda
import { EmployeeEntity } from '@ascend-hr/database'

// Create
await EmployeeEntity.create({ ... }).go()

// Query
await EmployeeEntity.query.byDepartment({ departmentId }).go()

# Update
await EmployeeEntity.patch({ id }).set({ ... }).go()

// Delete
await EmployeeEntity.delete({ id }).go()
```
