# API

## Authentication

### Login

        POST /api/v1/auth

### Logout

        GET /api/v1/logout

### Registration

        POST /api/v1/user

## Expense

### Create

1. Add expense
        
        POST /api/v1/expense

### Read

1. View all expenses and graphs

        GET /api/v1/expense

2. View individual expense

        GET /api/v1/expense/<expense_id>

### Update

1. Edit expense

        PUT /api/v1/expense/<expense_id>


### Delete

1. Delete expense

        DELETE /api/v1/expense/<expense_id>

