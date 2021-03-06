HOST: http://172.18.157.240:8000

# E-Tickets - User

E-Tickets-User API 文档（普通用户专用）

Admin, Cinema Owner 的 API 见其它文档。


## User [/api/user]

### 注册 [POST]

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

### 获取用户信息 [GET]

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


### 更新用户信息 [PATCH]

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


## User Session [/api/session/user]

### 用户登录 [POST]

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

### 用户登出 [DELETE]

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

## User Avatar [/api/user/avatar/$username]

### 上传头像 (不会更新User数据，只拿到图片地址) [POST]

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

## Movie [/api/movie/$movie_id]

### 获取电影详情 [GET]

* Response 200 (application/json)

    {
	    "status": "OK",
        "message": "Find movies.",
		"data": {
    		"movie_id": 7,
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
		}
	}

* Response 404 (application/json)

    {
	    "status": "NOT_FOUND",
		"message": "Cannot find any movie.",
		"data": {}
	}

## Movies - by status [/api/movies/status/$status_id]

### 通过电影未上映、热映中、下映检索电影 [GET]

* Response 200 (application/json)

	{
    	"status": "OK",
        "message": "Find movies.",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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
                },
                {
                	//...
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

## Movies - by keyword [/api/movies/$key_word]

### 根据key检索电影 [GET]

* Response 200 (application/json)

    {
    	"status": "OK",
        "message": "Find movies.",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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

## Movies - by Title [/api/movies/title/$key_word]

### 标题检索电影 [GET]

* Response 200 (application/json)

    {
    	"status": "OK",
        "message": "Find movies. Search by title",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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

## Movies - by Director [/api/movies/director/$key_word]

### 导演检索电影 [GET]

* Response 200 (application/json)

    {
    	"status": "OK",
        "message": "Find movies. Search by director",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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

## Movies - by Actor [/api/movies/actor/$key_word]

### 演员检索电影 [GET]

* Response 200 (application/json)

    {
    	"status": "OK",
        "message": "Find movies. Search by actor",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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

## Movies - by Tag [/api/movies/tag/$key_word]

### 标签检索电影 [GET]

* Response 200 (application/json)

    {
    	"status": "OK",
        "message": "Find movies. Search by tag",
        "data": {
            "movies": [
                {
                	"movie_id": 7,
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


## Cinema [/api/cinema/$cinema_id]

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


## Movie hall [/api/cinema/$cinema_id/moviehall/$hall_id]

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


## Movie Schedule [/api/schedule/$schedule_id]

### 通过 schedule_id 获取排片信息 [GET]

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


## Order [/api/order]

### 创建订单 [POST]

* Request (application/json)

    {
		"username": "qyb225",
		"schedule_id": 5,
		"seat_id": 131
	}

* Response 200 (application/json)

    {
		"status": "OK",
		"message": "Create order successfully.",
		"data": {
		    "username": "qyb225",
			"order_id": 7
		}
	}

* Response 400 (application/json)

    {
        "status": "BAD_REQUEST",
		"message": "Cannot create this order, check you params.",
		"data": {}
	}

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
		"message": "Permission denied. Please login.",
		"data": {}
	}

* Response 500 (application/json)

    {
	    "status": "INTERNAL_ERROR",
		"message": "Cannot create this order",
		"data": {}
	}


## Order [/api/order/$username/$order_id]

### 订单信息查询 [GET]

* Response 200 (application/json)

	{
		"status": "OK",
		"message": "Get order information.",
		"data": {
			"order_id": 2,
			"username": "qyb225",
			"schedule_id": 5,
			"seat": 121,
			"is_paid": 1
		}
	}

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
		"message": "Permission denied. Please login.",
		"data": {}
	}


* Response 404 (application/json)

	{
		"status": "NOT_FOUND",
		"message": "Cannot find any order.",
		"data": {}
	}


## Order Payment [/api/order/payment/$order_id]

### 支付订单 [PATCH]

* Request

	{
		"username": "qyb225",
		"is_paid": true
	}

* Response 200 (application/json)

	{
		"status": "OK",
		"message": "Successful payment.",
		"data": {
			"order_id": "1"
		}
	}

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
		"message": "Permission denied. Please login.",
		"data": {}
	}


* Response 404 (application/json)

	{
		"status": "NOT_FOUND",
		"message": "Order does not exist or has been paid.",
		"data": {}
	}


## Paid Orders [/api/orders/$username/paid-orders]

### 用户所有支付订单 [GET]

* Response 200 (application/json)

	{
		"status": "OK",
		"message": "Find orders!",
		"data": [
			{
				"order_id": 1,
				"username": "qyb225",
				"schedule_id": 5,
				"seat": 120,
				"is_paid": 1
			},
			{
				"order_id": 2,
				"username": "qyb225",
				"schedule_id": 5,
				"seat": 121,
				"is_paid": 1
			}
		]
	}

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
		"message": "Permission denied. Please login.",
		"data": {}
	}


* Response 404 (application/json)

	{
		"status": "NOT_FOUND",
		"message": "Cannot find any paid order.",
		"data": {}
	}


## Unpaid Orders [/api/orders/$username/unpaid-orders]

### 用户所有未支付订单 [GET]

* Response 200 (application/json)

	{
		"status": "OK",
		"message": "Find unpaid orders!",
		"data": [
			{
				"order_id": 3,
				"username": "qyb225",
				"schedule_id": 5,
				"seat": 130,
				"is_paid": 0
			},
			{
				"order_id": 4,
				"username": "qyb225",
				"schedule_id": 5,
				"seat": 131,
				"is_paid": 0
			}
		]
	}

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
		"message": "Permission denied. Please login.",
		"data": {}
	}


* Response 404 (application/json)

	{
		"status": "NOT_FOUND",
		"message": "Cannot find any unpaid order.",
		"data": {}
	}


## Comment [/api/comment]

### 发布评论 [POST]

* Request (application/json)

    {
        "username": "qyb225",
        "movie_id": 8,
        "is_recommended": true,
        "comment_content": "这部电影真好看，墙裂推荐",
        "is_spoiled": false
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Comment created!",
        "data": {
            "comment_id": 4,
            "username": "qyb225",
            "movie_id": 8,
            "is_recommended": true,
            "comment_content": "这部电影真好看，墙裂推荐",
            "is_spoiled": false
        }
    }

* Response 400 (application/json)

    {
        "status": "BAD_REQUEST",
        "message": "Movie is not exists.",
        "data": {}
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied.",
        "data": {}
    }

* Response 409 (application/json)

    {
        "status": "CONFLICT",
        "message": "You have made a comment.",
        "data": {}
    }

* Response 500 (applicaton/json)

	{
        "status": "UNKNOWN_ERROR",
        "message": "Something wrong.",
        "data": {}
    }

### 删除评论 [DELETE]

* Request (application/json)

    {
        "username": "qyb225",
        "movie_id": 8,
    }

* Response 200 (applicaton/json)

    {
        "status": "OK",
        "message": "Delete this comment successfully.",
        "data": {}
    }

* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied.",
        "data": {}
    }

## Movie's All Comments [/api/comments/all-comments/movieid/$movie_id]

### 一部电影的全部评论 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "All comments.",
        "data": [
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            },
            {
                "comment_id": 10,
                "username": "user2",
                "movie_id": 9,
                "is_recommended": 0,
                "comment_content": "我觉得这个电影一般吧",
                "is_spoiled": 0,
                "time": "2018-05-26 20:33:38"
            },
            {
                "comment_id": 9,
                "username": "user1",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "主角死了，死得好惨",
                "is_spoiled": 1,
                "time": "2018-05-26 20:32:49"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }

## Amount of movie's comments [/api/comments/all-comments/movieid/$movie_id/amount]

### 一部电影的全部评论数量 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Amount of comments.",
        "data": {
            "amount": 3
        }
    }

## One Page of Movie's All Comments [/api/comments/all-comments/movieid/$movie_id/page/$page_id/page-amount/$max_page_item_amount]


### 获取电影全部评论中的一页 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "All comments.",
        "data": [
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            },
            {
                "comment_id": 10,
                "username": "user2",
                "movie_id": 9,
                "is_recommended": 0,
                "comment_content": "我觉得这个电影一般吧",
                "is_spoiled": 0,
                "time": "2018-05-26 20:33:38"
            },
            {
                "comment_id": 9,
                "username": "user1",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "主角死了，死得好惨",
                "is_spoiled": 1,
                "time": "2018-05-26 20:32:49"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }

## Movie's Unspoiled Comments [/api/comments/unspoiled-comments/movieid/$movie_id]

### 一部电影的非剧透评论 [GET]

* Response 200 (applicaton/json)

    {
        "status": "OK",
        "message": "Unspoiled comments.",
        "data": [
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            },
            {
                "comment_id": 10,
                "username": "user2",
                "movie_id": 9,
                "is_recommended": 0,
                "comment_content": "我觉得这个电影一般吧",
                "is_spoiled": 0,
                "time": "2018-05-26 20:33:38"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }


## Amount of movie's unspoiled comments [/api/comments/unspoiled-comments/movieid/$movie_id/amount]

### 一部电影的非剧透评论数量 [GET]

* Response 200 (applicaiton/json)

    {
        "status": "OK",
        "message": "Amount of unspoiled comments.",
        "data": {
            "amount": 2
        }
    }

## One Page of Movie's Unspoiled Comments [/api/comments/unspoiled-comments/movieid/$movie_id/page/$page_id/page-amount/$max_page_item_amount]

### 获取电影非剧透评论中的一页 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Unspoiled comments.",
        "data": [
            {
                "comment_id": 10,
                "username": "user2",
                "movie_id": 9,
                "is_recommended": 0,
                "comment_content": "我觉得这个电影一般吧",
                "is_spoiled": 0,
                "time": "2018-05-26 20:33:38"
            },
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }

## User's comments [/api/comments/user/$username]

### 某用户发布的所有评论 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get user comments.",
        "data": [
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            },
            {
                "comment_id": 1,
                "username": "qyb225",
                "movie_id": 8,
                "is_recommended": 1,
                "comment_content": "这部电影真好看，墙裂推荐",
                "is_spoiled": 0,
                "time": "2018-05-26 19:17:54"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }


## Amount of user's comments [/api/comments/user/$username/amount]

### 某用户发布的评论数量 [GET]

* Response 200 (applicaiton/json)

    {
        "status": "OK",
        "message": "Amount of comments.",
        "data": {
            "amount": 2
        }
    }

## One Page of User's Comments [/api/comments/user/$username/page/$page_id/page-amount/$max_page_item_amount]

### 获取某用户评论中的一页 [GET]

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Get user comments.",
        "data": [
            {
                "comment_id": 11,
                "username": "qyb225",
                "movie_id": 9,
                "is_recommended": 1,
                "comment_content": "超级好看，墙裂推荐！",
                "is_spoiled": 0,
                "time": "2018-05-26 20:39:19"
            },
            {
                "comment_id": 1,
                "username": "qyb225",
                "movie_id": 8,
                "is_recommended": 1,
                "comment_content": "这部电影真好看，墙裂推荐",
                "is_spoiled": 0,
                "time": "2018-05-26 19:17:54"
            }
        ]
    }

* Response 404 (application/json)

    {
        "status": "NOT_FOUND",
        "message": "Cannot find any comment.",
        "data": {}
    }
