# Bottery Public API Documentation

## Base URL
All API endpoints are relative to: `https://cloud.bottery.ai/`

## Authentication
Most endpoints require authentication. This is done by including a valid JWT (JSON Web Token) in the `Authorization` header with the format `Bearer {token}` for each request. You can obtain a JWT by making a POST request to the `/api/auth` endpoint with your API key.

## API Key Validation
You can validate your API key using the `/api/key` endpoint. If the key is valid, you will receive a `success` status in the response.

## Endpoints

### POST /api/auth
**Description:** Authenticate with your API key and receive a JWT for further requests.

**Request Body:**
```json
{
    "api_key": "your_api_key"
}
```
**Response:**
```json
{
    "status": "success",
    "token": "your_token",
    "scope": ["global"]
}
```
Currently all API keys have a `global` scope.  More discrete scopes are planned in the near future.

### POST /api/key
**Description:** Validate your API key.

**Request Body:**
```json
{
    "api_key": "your_api_key"
}
```
**Response:**
```json
{
    "status": "success",
    "message": "key is valid"
}
```

### POST /api/agents
**Description:** Get a list of all the agents associated with the authenticated user. Authentication required.

**Response:**
```json
[
    {
        "id": "agent_id",
        "name": "agent_name",
        "status": "agent_status",
        "user_id": "user_id"
    },
    ...
]
```

### POST /api/agent/:agent_id
**Description:** Fetch information about a specific agent. The agent ID should be provided as a parameter in the URL. Authentication required.

**Response:**
```json
{
    "id": "agent_id",
    "name": "agent_name",
    "status": "agent_status",
    "user_id": "user_id"
}
```

### POST /api/conversations
**Description:** Get a list of all the conversations associated with the authenticated user. Authentication required.

**Response:**
```json
[
    {
        "id": "conversation_id",
        "agent_id": "agent_id",
        "status": "conversation_status",
        "user_id": "user_id"
    },
    ...
]
```

### POST /api/conversations/:conversation_id
**Description:** Fetch the messages in a specific conversation. The conversation ID should be provided as a parameter in the URL. Authentication required.

**Response:**
```json
[
    {
        "id": "message_id",
        "conversation_id": "conversation_id",
        "message": "message_content",
        "sender": "sender_type"
    },
    ...
]
```

### POST /api/conversations/new
**Description:** Create a new conversation. Authentication required.

**Request Body:**
```json
{
    "agent_id": "your_agent_id"
}
```
**Response:**
```json
{
    "status": "success",
    "id": "new_conversation_id"
}
```

### POST /api/conversations/msg/:conversation_id
**Description:** Add a message to a specific conversation. The conversation ID should be provided as a parameter in the URL. Authentication required.

**Request Body:**
```json
{
    "message": "your_message"
}
```
**Response:**
```json
{
    "id": "new_message_id"
}
```

**Note:** All the POST requests require a `Content-Type` header set to `application/json`. The response examples are indicative and actual responses may vary.
