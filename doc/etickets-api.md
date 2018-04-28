HOST: http://172.18.157.240:8000

# E-Tickets

E-Tickets API 文档

## User [/api/user]

### Register [POST]

* Request (application/json)
    {
        "username": "user8888",
        "password": "abcd12345",
        "nickname": "Superbaby"
    }

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Register successfully.",
        "data": {
            "username": "user8888",
            "nickname": "Superbaby",
            "avatar": "/images/avatar/default.png"
        }
    }

* Response 409 (application/json)
    {
        "status": "CONFLICT",
        "message": "Username conflict.",
        "data": {}
    }

* Response 500 (application/json)
    {
        "status": "UNKNOWN_ERROR",
        "message": "Something wrong.",
        "data": {}
    }

## User-Info [/api/user/$username]

### Get User-Info [GET]

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "User Infomation.",
        "data": {
            "username": "user8888",
            "nickname": "Superbaby",
            "avatar": "/images/avatar/default.png"
        }
    }

* Response 404 (application/json)
    {
        "status": "NOT_FOUND",
        "message": "User does not exist.",
        "data": {}
    }


### Update User-Info [PATCH]

* Request (application/json)
    {
        "nickname": "Angelababy",
        "avatar": "/images/avatar/user888820180501122330.png"
    }

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Update User Info successfully.",
        "data": {
            "username": "user8888",
            "nickname": "Angelababy",
            "avatar": "/images/avatar/user888820180501122330.png"
        }
    }

* Response 401 (application/json)
    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. Please login.",
        "data": {}
    }


## Admin [/api/admin]

### Admin Reginter [POST]

* Request (application/json)
    {
        "username": "admin",
        "password": "admin",
    }

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Admin register successfully.",
        "data": {
            "admin_username": "admin",
        }
    }

* Response 409 (application/json)
    {
        "status": "CONFLICT",
        "message": "Admin username conflict.",
        "data": {}
    }

* Response 500 (application/json)
    {
        "status": "UNKNOWN_ERROR",
        "message": "Something wrong.",
        "data": {}
    }

## User Session [/api/session/user]

### User Login [POST]

* Request (application/json)
    {
        "username": "user8888",
        "password": "abcd12345"
    }

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "User confirm.",
        "data": {
            "username": "user8888"
        }
    }

* Response 404 (application/json)
    {
        "status": "NOT_FOUND",
        "message": "User does not exit.",
        "data": {}
    }

* Response 403 (application/json)
    {
        "status": "FORBIDDEN",
        "message": "Password wrong.",
        "data": {}
    }

### User Logout [DELETE]

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Log out successfully.",
        "data": {}
    }

* Response 401 (application/json)
    {
		"status": "UNAUTHORIZED",
		"message": "You have not logged in.",
		"data": {}
	}

## Admin Session [/api/session/admin]

### Admin Login [POST]

* Request (application/json)
    {
        "username": "admin",
        "password": "admin"
    }

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Admin confirm.",
        "data": {
            "username": "admin"
        }
    }

* Response 404 (application/json)
    {
        "status": "NOT_FOUND",
        "message": "Admin does not exit.",
        "data": {}
    }

* Response 403 (application/json)
    {
        "status": "FORBIDDEN",
        "message": "Password wrong.",
        "data": {}
    }

### Admin Logout [DELETE]

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Admin log out successfully.",
        "data": {}
    }

* Response 401 (application/json)
    {
		"status": "UNAUTHORIZED",
		"message": "You have not logged in.",
		"data": {}
	}



