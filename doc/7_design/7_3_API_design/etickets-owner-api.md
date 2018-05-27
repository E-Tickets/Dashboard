HOST: http://172.18.157.240:8000

# E-Tickets - Cinema Owner

E-Tickets-Owner API 文档（影院老板专用）

Admin, User 的 API 见其它文档。

## Owner [/api/owner]

### 注册 [POST]

* Request (application/json)

    {
        "username": "ownerqyb225",
        "password": "abcd12345",
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema boss register successfully.",
        "data": {
            "username": "user8888",
        }
    }

* Response 409 (application/json)

    {
        "status": "CONFLICT",
        "message": "Cinema boss username conflict.",
        "data": {}
    }

* Response 500 (application/json)

    {
        "status": "UNKNOWN_ERROR",
        "message": "Something wrong.",
        "data": {}
    }

## Session [/api/session/owner]

### 登录 [POST]

* Request (applicaton/json)

    {
        "username": "ownerqyb225",
        "password": "123456"
    }

* Response 200 (applicaton/json)

    {
        "status": "OK",
        "message": "Cinema boss confirm.",
        "data": {
            "username": "ownerqyb225"
        }
    }

* Response 403 (applicaton/json)

    {
        "status": "FORBIDDEN",
        "message": "Password wrong.",
        "data": {}
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cinema owner does not exist.",
        "data": {}
    }

### 登出 [DELETE]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema Owner log out successfully.",
        "data": {}
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "You have not logged in.",
        "data": {}
    }

## Cinema [/api/cinema]

### 创建影院 [POST]

* Request (application/json)

    {
        "username": "ownerqyb225",
        "cinema_name": "Beijing International Cinema",
        "cinema_location": "Beijing"
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Create cinema successfully.",
        "data": {
            "cinema_id": 4,
            "owner": "ownerqyb225",
            "cinema_name": "Beijing International Cinema",
            "cinema_location": "Beijing"
        }
    }


* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not a cinema owner.",
        "data": {}
    }

* Response 500 (application/json)

    {
        "status": "INTERNAL_ERROR",
        "message": "Cannot create this cinema."
        "data": {}
    }


## MovieHall [/api/cinema/moviehall]

### 创建影厅 [POST]

* Request (application/json)

    {
        "username": "ownerqyb225",
        "cinema_id": 4,
        "hall_id": 1,
        "size_id": 3,
        "size": 480
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Create movie hall successfully.",
        "data": {
            "cinema_id": 4,
            "hall_id": 1,
            "size_id": 3,
            "size": 480
        }
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not the owner of this cinema.",
        "data": {}
    }

* Response 500 (application/json)

    {
        "status": "INTERNAL_ERROR",
        "message": "Cannot create this movie hall."
        "data": {}
    }

## Cinema Info [/api/cinema/$cinema_id]

### 获取电影院信息 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema information.",
        "data": {
            "cinema_id": 1,
            "cinema_name": "Qubic cinema",
            "cinema_location": "Guangzhou",
            "owner": "ownerqyb225"
        }
    }

* Response 404 (application/json)

     {
        "status": "NOT_FOUND",
        "message": "Cinema does not exist.",
        "data": {}
    }

## Movie halls [/api/cinema/$cinema_id/moviehalls]

### 影院所有影厅信息 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Moviehall search by cinema_id.",
        "data": [
            {
                "cinema_id": 1,
                "hall_id": 1,
                "size_id": 2,
                "size": 320
            },
            {
                "cinema_id": 1,
                "hall_id": 2,
                "size_id": 3,
                "size": 480
            },
            {
                "cinema_id": 1,
                "hall_id": 3,
                "size_id": 3,
                "size": 480
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any movie halls.",
        "data": {}
    }


## Movie hall Info [/api/cinema/$cinema_id/moviehall/$hall_id]

### 影院某个影厅信息 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Movie Hall information.",
        "data": {
            "cinema_id": 1,
            "hall_id": 1,
            "size_id": 2,
            "size": 320
        }
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any movie halls.",
        "data": {}
    }


## Cinemas - Owner [/api/cinemas/owner/$owner_username]

### 某影院老板的所有影院信息 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema search by owner.",
        "data": [
            {
                "cinema_id": 1,
                "cinema_name": "Qubic cinema",
                "cinema_location": "Guangzhou",
                "owner": "ownerqyb225"
            },
            {
                "cinema_id": 2,
                "cinema_name": "Wonderful Cinema",
                "cinema_location": "Guangzhou",
                "owner": "ownerqyb225"
            },
            {
                "cinema_id": 3,
                "cinema_name": "Pk Cinema",
                "cinema_location": "Beijing",
                "owner": "ownerqyb225"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any cinemas.",
        "data": {}
    }


## Cinemas - Location [/api/cinemas/location/$location]

### 某地的所有影院 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema search by location.",
        "data": [
            {
                "cinema_id": 1,
                "cinema_name": "Qubic cinema",
                "cinema_location": "Guangzhou",
                "owner": "ownerqyb225"
            },
            {
                "cinema_id": 2,
                "cinema_name": "Wonderful Cinema",
                "cinema_location": "Guangzhou",
                "owner": "ownerqyb225"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any cinemas.",
        "data": {}
    }


## Cinemas - CinemaName [/api/cinemas/cinema-name/$cinema_name]

### 某名字的所有影院 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Cinema search by name.",
        "data": [
            {
                "cinema_id": 1,
                "cinema_name": "Qubic cinema",
                "cinema_location": "Guangzhou",
                "owner": "ownerqyb225"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any cinemas.",
        "data": {}
    }

## Movie Schedule [/api/schedule]

### 创建排片 [POST]

* Request (application/json)

    {
        "username": "ownerqyb225",
        "cinema_id": 4,
        "hall_id": 1,
        "movie_id": 8,
        "time": "2018-05-03-15-00",
        "price": 80
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Create schedule successfully.",
        "data": {
            "schedule_id": 6,
            "movie_id": 8,
            "cinema_id": 4,
            "hall_id": 1,
            "time": "2018-05-03-15-00",
            "price": 80
        }
    }

* Response 400 (application/json)

    {
        "status": "BAD_REQUEST",
        "message": "Invalid params",
        "data": {}
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not a cinema owner.",
        "data": {}
    }


## Movie Schedule [/api/schedule/$schedule_id]

### 通过 id 获取排片详情 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get schedule infomation successfully.",
        "data": {
            "schedule_id": 5,
            "cinema_id": 1,
            "hall_id": 1,
            "time": "2018/05/03-15:00",
            "movie_id": 8,
            "price": 80,
            "seat": [
                120,
                121,
                130,
                131
            ]
        }
    }


* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any schedules.",
        "data": {}
    }


### 删除排片 [DELETE]

* Request (applicaton/json)

    {
        "username": "ownerqyb225",
        "cinema_id": 1
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Delete schedule successfully.",
        "data": {}
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not the owner of this schedule.",
        "data": {}
    }


## Movie Schedules - cinema_id [/api/schedules/cinemaid/$cinema_id]

### 某影院的所有排片 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get schedules successfully.",
        "data": [
            {
                "schedule_id": 1,
                "cinema_id": 1,
                "hall_id": 1,
                "time": "2018/05/03-12:00",
                "movie_id": 7,
                "price": 80
            },
            {
                "schedule_id": 5,
                "cinema_id": 1,
                "hall_id": 1,
                "time": "2018/05/03-15:00",
                "movie_id": 8,
                "price": 80
            }
        ]
    }


* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any schedules.",
        "data": {}
    }


## Movie Schedules - movie_id [/api/schedules/movieid/$movie_id]

### 某电影的排片情况 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get schedules successfully.",
        "data": [
            {
                "schedule_id": 1,
                "cinema_id": 1,
                "hall_id": 1,
                "time": "2018/05/03-12:00",
                "movie_id": 7,
                "price": 80
            },
            {
                "schedule_id": 2,
                "cinema_id": 2,
                "hall_id": 1,
                "time": "2018/05/03-13:00",
                "movie_id": 7,
                "price": 80
            },
            {
                "schedule_id": 3,
                "cinema_id": 3,
                "hall_id": 1,
                "time": "2018/05/03-13:00",
                "movie_id": 7,
                "price": 80
            }
        ]
    }


* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any schedules.",
        "data": {}
    }


## Movie Schedules - movie_id and location [/api/schedules/movieid/$movie_id/location/$location]

### 某地区某电影排片情况 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get schedules successfully.",
        "data": [
            {
                "schedule_id": 1,
                "cinema_id": 1,
                "hall_id": 1,
                "time": "2018/05/03-12:00",
                "movie_id": 7,
                "price": 80
            },
            {
                "schedule_id": 2,
                "cinema_id": 2,
                "hall_id": 1,
                "time": "2018/05/03-13:00",
                "movie_id": 7,
                "price": 80
            }
        ]
    }


* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any schedules.",
        "data": {}
    }

