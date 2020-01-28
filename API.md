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
        
        POST /add/<user_id>

2. Add limit to expense

        POST /budget/<user_id>

### Read

1. View all expenses and graphs

        GET /view/<user_id>

2. View individual expense

        GET /view/<user_id>/<expense_id>

3. View expenses according to it's category

        GET /category/<user_id>

### Update

1. Edit expense

        POST /edit/<user_id>/<expense_id>


### Delete

1. Delete expense

        PUT /delete/<user_id>/<expense_id>

