### API Documentation for State Usage (Frontend)

This documentation provides details on how the frontend can interact with the backend to retrieve information about Nigerian states and their local government areas (LGAs). Below are the available endpoints, request formats, response structures, and example usage.

---
``` baseEndpoint: https://100daysofcoding-production.up.railway.app/```
### 1. **Get All States**

#### **Endpoint:**
```
GET baseEndpoint/api/v1/states
```

#### **Description:**
This endpoint retrieves all Nigerian states along with their corresponding IDs, aliases, and local government areas (LGAs).

#### **Response Format:**
- **Status:** `200 OK`
- **Content-Type:** `application/json`

```json
[
  {
    "id": 1,
    "state": "Abia",
    "alias": "abia",
    "lgas": [
      { "id": 1, "name": "Aba North" },
      { "id": 2, "name": "Arochukwu" }
      ...
    ]
  },
  {
    "id": 2,
    "state": "Adamawa",
    "alias": "adamawa",
    "lgas": [
      { "id": 1, "name": "Demsa" },
      { "id": 2, "name": "Fufure" }
      ...
    ]
  }
]
```

#### **Example Request:**
```bash
GET baseEndpoint/api/v1/states
```

#### **Example Response:**
```json
[
  {
    "id": 1,
    "state": "Abia",
    "alias": "abia",
    "lgas": [
      { "id": 1, "name": "Aba North" },
      { "id": 2, "name": "Arochukwu" }
    ]
  },
  {
    "id": 2,
    "state": "Adamawa",
    "alias": "adamawa",
    "lgas": [
      { "id": 1, "name": "Demsa" },
      { "id": 2, "name": "Fufure" }
    ]
  }
]
```

---

### 2. **Get State by ID**

#### **Endpoint:**
```
GET baseEndpoint/api/v1/states/:id
```

#### **Description:**
This endpoint retrieves a single state by its ID, along with its alias and local government areas (LGAs).

#### **Path Parameters:**
- `id`: The numeric ID of the state (starting from 1).

#### **Response Format:**
- **Status:** `200 OK`
- **Content-Type:** `application/json`

```json
{
  "id": 1,
  "state": "Abia",
  "alias": "abia",
  "lgas": [
    { "id": 1, "name": "Aba North" },
    { "id": 2, "name": "Arochukwu" }
  ]
}
```

#### **Example Request:**
```bash
GET baseEndpoint/api/v1/states/1
```

#### **Example Response:**
```json
{
  "id": 1,
  "state": "Abia",
  "alias": "abia",
  "lgas": [
    { "id": 1, "name": "Aba North" },
    { "id": 2, "name": "Arochukwu" }
  ]
}
```

---

### 3. **Get State by Name**

#### **Endpoint:**
```
GET baseEndpoint/api/v1/states/:name
```

#### **Description:**
This endpoint retrieves a single state by its name (case-insensitive) along with its alias and local government areas (LGAs).

#### **Path Parameters:**
- `name`: The name of the state (e.g., `Abia` or `adamawa`).

#### **Response Format:**
- **Status:** `200 OK`
- **Content-Type:** `application/json`

```json
{
  "id": 1,
  "state": "Abia",
  "alias": "abia",
  "lgas": [
    { "id": 1, "name": "Aba North" },
    { "id": 2, "name": "Arochukwu" }
  ]
}
```

#### **Example Request:**
```bash
GET baseEndpoint/api/v1/states/Abia
```

#### **Example Response:**
```json
{
  "id": 1,
  "state": "Abia",
  "alias": "abia",
  "lgas": [
    { "id": 1, "name": "Aba North" },
    { "id": 2, "name": "Arochukwu" }
  ]
}
```

---

### Error Handling:

#### **Common Errors:**
- **404 Not Found:** If a state or LGA is not found.
  
#### **Example Error Response:**
```json
{
  "message": "State not found"
}
```

---

### Frontend Integration

1. **Fetching All States:**

You can use `fetch` to get all states and display them in a dropdown or list.

```javascript
fetch('baseEndpoint/api/v1/states')
  .then(response => response.json())
  .then(data => {
    console.log(data); // Array of states
  })
  .catch(error => console.error('Error:', error));
```

2. **Fetching a State by ID:**

To get the details of a specific state by ID:

```javascript
fetch('baseEndpoint/api/v1/states/1')
  .then(response => response.json())
  .then(data => {
    console.log(data); // Single state object
  })
  .catch(error => console.error('Error:', error));
```

3. **Fetching a State by Name:**

To get the details of a specific state by name:

```javascript
fetch('baseEndpoint/api/v1/states/Abia')
  .then(response => response.json())
  .then(data => {
    console.log(data); // Single state object
  })
  .catch(error => console.error('Error:', error));
```

---

### Usage Tips:
- Ensure the frontend properly handles 404 errors when a state is not found.
- Cache state data if the data rarely changes to reduce server requests.

