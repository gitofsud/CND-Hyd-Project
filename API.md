# API

## Authentication

### Login

        POST /api/auth

### Logout

        GET /api/logout

### Registration

        POST /api/user

## Expense

### Create

1. Add expense
        
        POST /api/expense

### Read

1. View all expenses and graphs

        GET /api/expense

2. View individual expense

        GET /api/expense/<expense_id>

### Update

1. Edit expense

        PUT /api/expense/<expense_id>


### Delete

1. Delete expense

        DELETE /api/expense/<expense_id>

