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

## User Avatar Upload[/api/user/avatar/$username]

### Upload and get addr (不会更新User数据，只拿到图片地址) [POST]

* Request (multipart/form-data)
    Content-Disposition: form-data; name="avatar"; filename="xxx.png"

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Upload successfully.",
        "data": {
		    "avatar": "/images/avatar/avatarxxxx.png"
		}
    }

* Response 401 (application/json)
    {
	    "status": "UNAUTHORIZED",
        "message": "Permission denied. Please login.",
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

## Movie [/api/movie]

### Create a movie [POST]

* Request (application/json)
    {
	    "movie_title":"The Dark Knight",
	    "poster":"/images/poster/the-dark-knight.png",
	    "director":"Christopher Nolan",
	    "actors":["Christian Bale","Heath Ledger","Aaron Eckhart"],
	    "tags":["Crime","DC"]
	}

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Create movie successfully.",
        "data": {
		    "movie_title":"The Dark Knight",
	        "poster":"/images/poster/the-dark-knight.png",
	        "director":"Christopher Nolan",
	        "actors":["Christian Bale","Heath Ledger","Aaron Eckhart"],
	        "tags":["Crime","DC"]
		}
	}

* Response 401 (application/json)
    {
	    "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not admin,
        "data": {}
	}

* Response 500 (application/json)
    {
		"status" = "INTERNAL_ERROR";
        "message" = "Cannot create this movie.";
        "data" = {};
	}

## Movie Poster Upload [/api/movie/poster]

### Upload and get addr (不会更新Movie数据，只拿到图片地址) [POST]

* Request (multipart/form-data)
    Content-Disposition: form-data; name="poster"; filename="xxx.png"

* Response 200 (application/json)
    {
        "status": "OK",
        "message": "Upload successfully.",
        "data": {
		    "poster": "/images/poster/posterxxxx.png"
		}
    }

* Response 401 (application/json)
    {
	    "status": "UNAUTHORIZED",
        "message": "Permission denied. Please login as admin.",
        "data": {}
	}



## Movies include key_word [/api/movies/$key_word]

### Search movies by key words [GET]

* Response 200 (application/json)
    {
    	"status": "OK",
        "message": "Find movies.",
        "data": {
            "movies": [
                {
                    "title": "The Dark Knight",
                    "poster": "/images/poster/the-dark-knight.png",
                    "director": "Christopher Nolan",
                    "actors": [
                        "Christian Bale",
                        "Heath Ledger",
                        "Aaron Eckhart"
                    ],
                    "tags": [
                        "Crime",
                        "DC"
                    ]
                }
            ]
        }
	}

* Response 404 (application/json)
    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

## Movies with key_word title [/api/movies/title/$key_word]

### Search movies by title [GET]

* Response 200 (application/json)
    {
    	"status": "OK",
        "message": "Find movies. Search by title",
        "data": {
            "movies": [
                {
                    "title": "The Dark Knight",
                    "poster": "/images/poster/the-dark-knight.png",
                    "director": "Christopher Nolan",
                    "actors": [
                        "Christian Bale",
                        "Heath Ledger",
                        "Aaron Eckhart"
                    ],
                    "tags": [
                        "Crime",
                        "DC"
                    ]
                }
            ]
        }
	}

* Response 404 (application/json)
    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

## Movies directed by key_word director [/api/movies/director/$key_word]

### Search movies by director [GET]

* Response 200 (application/json)
    {
    	"status": "OK",
        "message": "Find movies. Search by director",
        "data": {
            "movies": [
                {
                    "title": "The Dark Knight",
                    "poster": "/images/poster/the-dark-knight.png",
                    "director": "Christopher Nolan",
                    "actors": [
                        "Christian Bale",
                        "Heath Ledger",
                        "Aaron Eckhart"
                    ],
                    "tags": [
                        "Crime",
                        "DC"
                    ]
                }
            ]
        }
	}

* Response 404 (application/json)
    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

## Movies acted by key_word actor [/api/movies/actor/$key_word]

### Search movies by actor [GET]

* Response 200 (application/json)
    {
    	"status": "OK",
        "message": "Find movies. Search by actor",
        "data": {
            "movies": [
                {
                    "title": "The Dark Knight",
                    "poster": "/images/poster/the-dark-knight.png",
                    "director": "Christopher Nolan",
                    "actors": [
                        "Christian Bale",
                        "Heath Ledger",
                        "Aaron Eckhart"
                    ],
                    "tags": [
                        "Crime",
                        "DC"
                    ]
                }
            ]
        }
	}

* Response 404 (application/json)
    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

## Movies with key_word tag [/api/movies/tag/$key_word]

### Search movies by tag [GET]

* Response 200 (application/json)
    {
    	"status": "OK",
        "message": "Find movies. Search by tag",
        "data": {
            "movies": [
                {
                    "title": "The Dark Knight",
                    "poster": "/images/poster/the-dark-knight.png",
                    "director": "Christopher Nolan",
                    "actors": [
                        "Christian Bale",
                        "Heath Ledger",
                        "Aaron Eckhart"
                    ],
                    "tags": [
                        "Crime",
                        "DC"
                    ]
                }
            ]
        }
	}

* Response 404 (application/json)
    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

