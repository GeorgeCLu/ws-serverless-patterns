# Users Service

A serverless users management API built with AWS SAM, featuring JWT authorization via Amazon Cognito.

## Architecture

- **API Gateway**: REST API with Lambda authorizer
- **Lambda Functions**: Users CRUD operations and JWT authorization
- **DynamoDB**: Users data storage
- **Cognito**: User authentication and authorization

## API Endpoints

- `GET /users` - List all users
- `PUT /users` - Create new user
- `GET /users/{userid}` - Get specific user
- `PUT /users/{userid}` - Update user
- `DELETE /users/{userid}` - Delete user

## Deployment

```bash
sam build
sam deploy --guided
```

## Authentication

Use the Cognito User Pool for authentication. Get access token:

```bash
aws cognito-idp initiate-auth --auth-flow USER_PASSWORD_AUTH --client-id <client-id> --auth-parameters USERNAME=<username>,PASSWORD=<password> --query 'AuthenticationResult.AccessToken' --output text
```

Include the token in API requests:
```bash
curl -H "Authorization: <access-token>" https://<api-endpoint>/users
```

## Configuration

- **UserPoolAdminGroupName**: Admin group name (default: `apiAdmins`)
- Users in admin group have elevated permissions