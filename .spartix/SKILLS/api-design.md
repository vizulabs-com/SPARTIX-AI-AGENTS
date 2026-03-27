# Skill: API Design

## Name
api-design

## Version
1.0.0

## Description
Design RESTful and GraphQL APIs following industry standards including endpoint structure, resource modeling, versioning strategy, pagination patterns, error handling conventions, authentication schemes, and rate limiting policies.

## Parameters
- **api_style**: API style (REST, GraphQL, gRPC, WebSocket, hybrid)
- **versioning**: Versioning strategy (URL path, header, query parameter)
- **auth_scheme**: Authentication scheme (OAuth2, API key, JWT, mTLS)
- **pagination**: Pagination strategy (cursor, offset, keyset)
- **spec_format**: Specification format (OpenAPI 3.x, GraphQL SDL, Protobuf)

## Outputs
- API specification document in the specified format
- Endpoint inventory with HTTP methods, paths, and descriptions
- Request/response schema definitions with examples
- Error code catalog with descriptions and resolution guidance
- Authentication and authorization flow documentation

## Prerequisites
- Business requirements and data models must be available from predecessor tasks
- API style and versioning strategy must be specified in the task packet
- Security requirements must be defined for authentication scheme selection

## Approved Categories
- 05_BACKEND_AND_API_SPECIALISTS
- 20_MCP_ARCHITECTURE_AND_INTEGRATION

## Usage Rules
- All endpoints must follow consistent naming conventions and HTTP method semantics
- Error responses must use a standardized error format across all endpoints
- Breaking changes must be managed through versioning — never modify existing contracts
