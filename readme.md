# Planet API - REST API Design

**Assignmet for Full Stack with Node.JS**
**Made By:** `Lucas Modin`
**Base URL:**  `/api/v1`

## Collections
I have identified the following collections:
* Planets
* Moons
* Stars
* Systems (read: Star Systems)
* Galaxies

## Domain Model (draft)
The domain model draft for the design of the system.

![DOMAIN MODEL](/domain-model.png)


## Collections and Endpoints
### 1. Galaxies
We follow the ordering of the methods:
GET ---> POST ---> PUT/PATCH ---> DELETE

| Method | Endpoint | Comment|
|--|--|--|
| GET |  /galaxies| list all galaxies |
| POST |  /galaxies| create a galaxy |
| GET |  /galaxies/{galaxyId}| retrieve 1 galaxy |
| PUT |  /galaxies/{galaxyId}| replace the whole resource |
| PATCH |  /galaxies/{galaxyId}| partial update |
| DELETE |  /galaxies/{galaxyId}| delete |

**Sub-collections for galaxies**
|Method| Endpoint |Comment |
|--|--|--|
| GET | /galaxies/{galaxyId}/systems | list all the systems in the galaxy | 
|POST |/galaxies/{galaxyId}/systems |create a system within the galaxy |

### 2. Systems
| Method | Endpoint | Comment|
|--|--|--|
| GET |  /systems| list all systems |
| POST |  /systems| create a system |
| GET |  /systems/{systemId}| retrieve 1 system |
| PUT |  /systems/{systemId}| replace the whole resource |
| PATCH |  /systems/{systemId}| partial update |
| DELETE |  /systems/{systemId}| delete |

**Sub-collections for Systems**
|Method| Endpoint |Comment |
|--|--|--|
| GET | /systems/{systemId}/stars | list all the stars in the system | 
|POST |/systems/{systemId}/stars |create a star within the system |
| GET | /systems/{systemId}/planets | list all the planets in the system | 
|POST |/systems/{systemId}/planets |create a planet within the system |

### 3. Stars
| Method | Endpoint | Comment|
|--|--|--|
| GET |  /stars| list all stars |
| POST |  /stars| create a star |
| GET |  /stars/{starId}| retrieve 1 star |
| PUT |  /stars/{starId}| replace the whole resource |
| PATCH |  /stars/{starId}| partial update |
| DELETE |  /stars/{starId}| delete |

### 4. Planets
| Method | Endpoint | Comment|
|--|--|--|
| GET |  /planets| list all planets |
| POST |  /planets| create a planet |
| GET |  /planets/{planetId}| retrieve 1 planet |
| PUT |  /planets/{planetId}| replace the whole resource |
| PATCH |  /planets/{planetId}| partial update |
| DELETE |  /planets/{planetId}| delete |

**Sub-collections for Planets**
|Method| Endpoint |Comment |
|--|--|--|
| GET | /planets/{planetId}/moons | list all the moons orbiting the planet | 
|POST |/planets/{planetId}/moons |create a moon orbiting the planet |
### 5. Moons

| Method | Endpoint | Comment|
|--|--|--|
| GET |  /moons| list all moons |
| POST |  /moons| create a moon|
| GET |  /moons/{moonId}| retrieve 1 moon |
| PUT |  /moons/{moonId}| replace the whole resource |
| PATCH |  /moons/{moonId}| partial update |
| DELETE |  /moons/{moonId}| delete |

## Resource Schemas
### 1. Galaxy
```json
{
"id": "example_id",
"name": "Milky Way",
"discoveredBy": "2 Chainz",
"distanceLightYears": 0,
"createdAt": "2025-09-03T12:00:00Z",
"updatedAt": "2025-09-03T12:00:00Z"
}
```

### 2. System    
```json
{
"id": "system_1111111111",
"galaxyId": "example_id",
"name": "solar system",
"ageBillionYears": 4.6,
"createdAt": "2025-09-03T12:00:00Z",
"updatedAt": "2025-09-03T12:00:00Z"
}
```

### 3. Star
```json
{
"id": "star_2chainz",
"systemId": "system_1111111111",
"name": "sun",
"massKg": 1.9885e30,
"radiusKm": 696349,
"createdAt": "2025-09-03T12:00:00Z",
"updatedAt": "2025-09-03T12:00:00Z"
}
```

### 4. Planet

```json
{
"id": "pl_juicyj",
"systemId": "system_1111111111",
"name": "earth",
"massKg": 5.972e24,
"radiusKm": 6371,
"hasLife": true,
"createdAt": "2025-09-03T12:00:00Z",
"updatedAt": "2025-09-03T12:00:00Z"
}
```

### 5. Moon
```json
{
"id": "moon_guccimane",
"planetId": "pl_juicyj",
"name": "moon",
"massKg": 7.347e22,
"radiusKm": 1737.4,
"createdAt": "2025-09-03T12:00:00Z",
"updatedAt": "2025-09-03T12:00:00Z"
}
```

## Error model and status codes
Errors should display  a human message with a meaningful code.
The message and code will be envoloped in an **error** body.
A requestId has been added to add traceability

```json
{
"error": {
	"code": "RESOURCE_NOT_FOUND",
	"message": "planet not found",
	"requestId": "req_123"
	}
}
``` 
*Note to self: a `detail` array could be added for a more detailed error message with field validation errors*
