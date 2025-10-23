# processing_plant_releases

# Mock Devices API Documentation

This document describes all available API endpoints for managing mock devices.

**Base URL**: `http://34.93.200.117:3000/api/mock`

---

## Table of Contents
- [Create Operations](#create-operations)
- [Read Operations](#read-operations)
- [Update Operations](#update-operations)
- [Delete Operations](#delete-operations)
- [Response Format](#response-format)
- [Error Codes](#error-codes)

---

## Create Operations

### 1. Create Mock Device
Create a new mock device.

**Endpoint**: `POST http://34.93.200.117:3000/api/mock`

**Request Body**:
```json
{
  "deviceId": "DEVICE_001",
  "deviceName": "Test Device 1",
  "voltage": 220.5,
  "amp": 10.2,
  "power": 2248.2
}
```

**Parameters**:
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| deviceId | string | Yes | Unique identifier for the device |
| deviceName | string | No | Name/description of the device |
| voltage | number | No | Voltage value (must be positive) |
| amp | number | No | Amperage value (must be positive) |
| power | number | No | Power value (must be positive) |

**Success Response** (201):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Test Device 1",
    "voltage": "220.50",
    "amp": "10.20",
    "power": "2248.20",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T10:30:00.000Z"
  }
}
```

**Error Response** (409):
```json
{
  "success": false,
  "error": "Device with this deviceId already exists"
}
```

---

### 2. Upsert Mock Device
Create a new device or update if it already exists (based on deviceId).

**Endpoint**: `POST http://34.93.200.117:3000/api/mock/upsert`

**Request Body**:
```json
{
  "deviceId": "DEVICE_001",
  "deviceName": "Updated Device Name",
  "voltage": 230.0,
  "amp": 12.5,
  "power": 2875.0
}
```

**Parameters**: Same as Create Mock Device

**Success Response** (200):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Updated Device Name",
    "voltage": "230.00",
    "amp": "12.50",
    "power": "2875.00",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T11:15:00.000Z"
  }
}
```

---

## Read Operations

### 3. Get All Mock Devices
Retrieve all mock devices ordered by creation date (newest first).

**Endpoint**: `GET http://34.93.200.117:3000/api/mock`

**Query Parameters**: None

**Success Response** (200):
```json
{
  "success": true,
  "data": [
    {
      "id": 2,
      "device_id": "DEVICE_002",
      "device_name": "Test Device 2",
      "voltage": "110.00",
      "amp": "5.50",
      "power": "605.00",
      "created_at": "2025-10-23T11:00:00.000Z",
      "updated_at": "2025-10-23T11:00:00.000Z"
    },
    {
      "id": 1,
      "device_id": "DEVICE_001",
      "device_name": "Test Device 1",
      "voltage": "220.50",
      "amp": "10.20",
      "power": "2248.20",
      "created_at": "2025-10-23T10:30:00.000Z",
      "updated_at": "2025-10-23T10:30:00.000Z"
    }
  ]
}
```

---

### 4. Get Mock Devices (Paginated)
Retrieve mock devices with pagination support.

**Endpoint**: `GET http://34.93.200.117:3000/api/mock/paginated`

**Query Parameters**:
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| limit | number | No | 10 | Number of records per page |
| offset | number | No | 0 | Number of records to skip |

**Example Request**:
```
GET http://34.93.200.117:3000/api/mock/paginated?limit=5&offset=10
```

**Success Response** (200):
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "device_id": "DEVICE_001",
      "device_name": "Test Device 1",
      "voltage": "220.50",
      "amp": "10.20",
      "power": "2248.20",
      "created_at": "2025-10-23T10:30:00.000Z",
      "updated_at": "2025-10-23T10:30:00.000Z"
    }
  ],
  "total": 25,
  "limit": 5,
  "offset": 10
}
```

---

### 5. Get Mock Device by ID
Retrieve a specific mock device by its primary key ID.

**Endpoint**: `GET http://34.93.200.117:3000/api/mock/:id`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | number | Yes | Primary key ID of the device |

**Example Request**:
```
GET http://34.93.200.117:3000/api/mock/1
```

**Success Response** (200):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Test Device 1",
    "voltage": "220.50",
    "amp": "10.20",
    "power": "2248.20",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T10:30:00.000Z"
  }
}
```

**Error Response** (404):
```json
{
  "success": false,
  "error": "Mock device not found"
}
```

---

### 6. Get Mock Device by Device ID
Retrieve a specific mock device by its unique device_id.

**Endpoint**: `GET http://34.93.200.117:3000/api/mock/device/:deviceId`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| deviceId | string | Yes | Unique device identifier |

**Example Request**:
```
GET http://34.93.200.117:3000/api/mock/device/DEVICE_001
```

**Success Response** (200):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Test Device 1",
    "voltage": "220.50",
    "amp": "10.20",
    "power": "2248.20",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T10:30:00.000Z"
  }
}
```

**Error Response** (404):
```json
{
  "success": false,
  "error": "Mock device not found"
}
```

---

### 7. Search Mock Devices by Name
Search for mock devices by name (case-insensitive partial match).

**Endpoint**: `GET http://34.93.200.117:3000/api/mock/search`

**Query Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | string | Yes | Search term for device name |

**Example Request**:
```
GET http://34.93.200.117:3000/api/mock/search?name=Test
```

**Success Response** (200):
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "device_id": "DEVICE_001",
      "device_name": "Test Device 1",
      "voltage": "220.50",
      "amp": "10.20",
      "power": "2248.20",
      "created_at": "2025-10-23T10:30:00.000Z",
      "updated_at": "2025-10-23T10:30:00.000Z"
    },
    {
      "id": 2,
      "device_id": "DEVICE_002",
      "device_name": "Test Device 2",
      "voltage": "110.00",
      "amp": "5.50",
      "power": "605.00",
      "created_at": "2025-10-23T11:00:00.000Z",
      "updated_at": "2025-10-23T11:00:00.000Z"
    }
  ]
}
```

---

### 8. Get Mock Devices by Voltage Range
Retrieve devices within a specified voltage range.

**Endpoint**: `GET http://34.93.200.117:3000/api/mock/voltage-range`

**Query Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| min | number | Yes | Minimum voltage value |
| max | number | Yes | Maximum voltage value |

**Example Request**:
```
GET http://34.93.200.117:3000/api/mock/voltage-range?min=100&max=250
```

**Success Response** (200):
```json
{
  "success": true,
  "data": [
    {
      "id": 2,
      "device_id": "DEVICE_002",
      "device_name": "Test Device 2",
      "voltage": "110.00",
      "amp": "5.50",
      "power": "605.00",
      "created_at": "2025-10-23T11:00:00.000Z",
      "updated_at": "2025-10-23T11:00:00.000Z"
    },
    {
      "id": 1,
      "device_id": "DEVICE_001",
      "device_name": "Test Device 1",
      "voltage": "220.50",
      "amp": "10.20",
      "power": "2248.20",
      "created_at": "2025-10-23T10:30:00.000Z",
      "updated_at": "2025-10-23T10:30:00.000Z"
    }
  ]
}
```

---

## Update Operations

### 9. Update Mock Device (Full Update)
Update all fields of a mock device by its primary key ID.

**Endpoint**: `PUT http://34.93.200.117:3000/api/mock/:id`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | number | Yes | Primary key ID of the device |

**Request Body**:
```json
{
  "deviceName": "Updated Device Name",
  "voltage": 240.0,
  "amp": 15.0,
  "power": 3600.0
}
```

**Parameters**:
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| deviceName | string | No | Updated device name |
| voltage | number | No | Updated voltage value |
| amp | number | No | Updated amperage value |
| power | number | No | Updated power value |

**Example Request**:
```
PUT http://34.93.200.117:3000/api/mock/1
```

**Success Response** (200):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Updated Device Name",
    "voltage": "240.00",
    "amp": "15.00",
    "power": "3600.00",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T12:00:00.000Z"
  }
}
```

---

### 10. Update Mock Device (Partial Update)
Update specific fields of a mock device by its primary key ID.

**Endpoint**: `PATCH http://34.93.200.117:3000/api/mock/:id`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | number | Yes | Primary key ID of the device |

**Request Body** (include only fields to update):
```json
{
  "voltage": 250.0,
  "amp": 16.5
}
```

**Parameters** (all optional, include only what needs to be updated):
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| deviceName | string | No | Device name to update |
| voltage | number | No | Voltage value to update |
| amp | number | No | Amperage value to update |
| power | number | No | Power value to update |

**Example Request**:
```
PATCH http://34.93.200.117:3000/api/mock/1
```

**Success Response** (200):
```json
{
  "success": true,
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Updated Device Name",
    "voltage": "250.00",
    "amp": "16.50",
    "power": "3600.00",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T12:30:00.000Z"
  }
}
```

---

## Delete Operations

### 11. Delete Mock Device by ID
Delete a mock device by its primary key ID.

**Endpoint**: `DELETE http://34.93.200.117:3000/api/mock/:id`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| id | number | Yes | Primary key ID of the device |

**Example Request**:
```
DELETE http://34.93.200.117:3000/api/mock/1
```

**Success Response** (200):
```json
{
  "success": true,
  "message": "Mock device deleted successfully",
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Test Device 1",
    "voltage": "220.50",
    "amp": "10.20",
    "power": "2248.20",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T10:30:00.000Z"
  }
}
```

**Error Response** (404):
```json
{
  "success": false,
  "error": "Mock device not found"
}
```

---

### 12. Delete Mock Device by Device ID
Delete a mock device by its unique device_id.

**Endpoint**: `DELETE http://34.93.200.117:3000/api/mock/device/:deviceId`

**Path Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| deviceId | string | Yes | Unique device identifier |

**Example Request**:
```
DELETE http://34.93.200.117:3000/api/mock/device/DEVICE_001
```

**Success Response** (200):
```json
{
  "success": true,
  "message": "Mock device deleted successfully",
  "data": {
    "id": 1,
    "device_id": "DEVICE_001",
    "device_name": "Test Device 1",
    "voltage": "220.50",
    "amp": "10.20",
    "power": "2248.20",
    "created_at": "2025-10-23T10:30:00.000Z",
    "updated_at": "2025-10-23T10:30:00.000Z"
  }
}
```

---

## Response Format

All API responses follow a consistent format:

### Success Response
```json
{
  "success": true,
  "data": { /* response data */ }
}
```

### Error Response
```json
{
  "success": false,
  "error": "Error message description"
}
```

### Paginated Response
```json
{
  "success": true,
  "data": [ /* array of items */ ],
  "total": 100,
  "limit": 10,
  "offset": 0
}
```

---

## Error Codes

| Status Code | Description |
|-------------|-------------|
| 200 | Success |
| 201 | Created successfully |
| 400 | Bad Request - Invalid parameters or validation error |
| 404 | Not Found - Resource doesn't exist |
| 409 | Conflict - Duplicate device_id |
| 500 | Internal Server Error |

---

## Common Validation Errors

### Invalid deviceId
```json
{
  "success": false,
  "error": "deviceId (string) is required"
}
```

### Invalid voltage/amp/power
```json
{
  "success": false,
  "error": "voltage must be a positive number"
}
```

### Missing required parameters
```json
{
  "success": false,
  "error": "Missing device data"
}
```

### No fields to update
```json
{
  "success": false,
  "error": "No valid fields to update"
}
```

---

## Database Schema

```sql
CREATE TABLE mock_devices (
    id SERIAL PRIMARY KEY,
    device_id VARCHAR(50) NOT NULL UNIQUE,
    device_name VARCHAR(100),
    voltage DECIMAL(10, 2),
    amp DECIMAL(10, 2),
    power DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Example Usage with cURL

### Create a device
```bash
curl -X POST http://34.93.200.117:3000/api/mock \
  -H "Content-Type: application/json" \
  -d '{
    "deviceId": "DEVICE_001",
    "deviceName": "Test Device 1",
    "voltage": 220.5,
    "amp": 10.2,
    "power": 2248.2
  }'
```

### Get all devices
```bash
curl -X GET http://34.93.200.117:3000/api/mock
```

### Update a device
```bash
curl -X PATCH http://34.93.200.117:3000/api/mock/1 \
  -H "Content-Type: application/json" \
  -d '{
    "voltage": 250.0
  }'
```

### Delete a device
```bash
curl -X DELETE http://34.93.200.117:3000/api/mock/1
```

---

## Example Usage with JavaScript (Fetch API)

### Create a device
```javascript
const response = await fetch('http://34.93.200.117:3000/api/mock', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    deviceId: 'DEVICE_001',
    deviceName: 'Test Device 1',
    voltage: 220.5,
    amp: 10.2,
    power: 2248.2
  })
});
const data = await response.json();
console.log(data);
```

### Get all devices with pagination
```javascript
const response = await fetch('http://34.93.200.117:3000/api/mock/paginated?limit=10&offset=0');
const data = await response.json();
console.log(data);
```

### Update a device
```javascript
const response = await fetch('http://34.93.200.117:3000/api/mock/1', {
  method: 'PATCH',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    voltage: 250.0,
    amp: 16.5
  })
});
const data = await response.json();
console.log(data);
```

---

## Notes

1. All numeric fields (voltage, amp, power) are stored as `DECIMAL(10, 2)` in the database
2. The `device_id` field has a UNIQUE constraint and cannot be duplicated
3. All timestamps are in ISO 8601 format
4. Search operations are case-insensitive
5. The `updated_at` field is automatically updated on any modification
6. Pagination uses 0-based offset indexing

---

**Last Updated**: October 23, 2025
