HOST: http://172.18.157.240:8000

# E-Tickets - Admin

E-Tickets-Owner API 文档（伟大的系统管理员 —— 我，专用）

Owner, User 的 API 见其它文档。

## Session [/api/session/owner]

### 登录 [POST]

* Request (applicaton/json)

    {
        "username": "handsomeadmin",
        "password": "123456"
    }

* Response 200 (applicaton/json)

    {
        "status": "OK",
        "message": "Admin confirm.",
        "data": {
            "admin_username": "handsomeadmin"
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
        "message": "Admin does not exist.",
        "data": {}
    }

### 登出 [DELETE]

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

### 创建电影 [POST]

* Request (application/json)

    {
        "movie_title":"Interstellar",
        "poster":"/images/poster/interstellar.png",
        "director":"Christopher Nolan",
        "actors":["Matthew McConaughey", "Anne Hathaway", "Jessica Chastain"],
        "tags":["Science Fiction","Space", "Love", "Adventure"]
    }

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Create movie successfully.",
        "data": {
            "movie_title": "Interstellar",
            "poster": "/images/poster/interstellar.png",
            "director": "Christopher Nolan",
            "actors": [
                "Matthew McConaughey",
                "Anne Hathaway",
                "Jessica Chastain"
            ],
            "tags": [
                "Science Fiction",
                "Space",
                "Love",
                "Adventure"
            ]
        }
    }


* Response 401 (application/json)

    {
        "status": "UNAUTHORIZED",
        "message": "Permission denied. You are not admin",
        "data": {}
    }

* Response 500 (application/json)

    {
	    "status": "INTERNAL_ERROR",
		"message": "Cannot create this movie.",
		"data": {}
	}

## Movie Poster [/api/movie/poster]

### 上传电影海报 (不会更新数据，只拿到图片地址) [POST]

* Request (multipart/form-data)
    Content-Disposition: form-data; name="poster"; filename="xxx.png"

* Response 200 (application/json)

    {
        "status": "OK",
        "message": "Upload successfully.",
        "data": {
		    "poster": "/images/poster/poster.png"
		}
    }

* Response 401 (application/json)

    {
	    "status": "UNAUTHORIZED",
        "message": "Permission denied. Please login as admin.",
        "data": {}
	}


## Movie [/api/movie/$movie_id]

### 获取电影详情 [GET]

* Response 200 (application/json)

    {
	    "status": "OK",
        "message": "Find movies.",
		"data": {
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

## Movies - by keyword [/api/movies/$key_word]

### 根据key检索电影 [GET]

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
				},
				{
					"title": "Inception",
					"poster": "/images/poster/inception.png",
					"director": "Christopher Nolan",
					"actors": [
						" Leonardo DiCaprio",
						"Joseph Gordon-Levitt",
						"Ellen Page"
					],
					"tags": [
						"Science Fiction",
						"Action",
						"Suspense"
					]
				},
				{
					"title": "Dunkirk",
					"poster": "/images/poster/dunkirk.png",
					"director": "Christopher Nolan",
					"actors": [
						"Fionn Whitehead",
						"Barry Keoghan",
						"Mark Rylance"
					],
					"tags": [
						"War",
						"Suspense"
					]
				},
				{
					"title": "Interstellar",
					"poster": "/images/poster/interstellar.png",
					"director": "Christopher Nolan",
					"actors": [
						"Matthew McConaughey",
						"Anne Hathaway",
						"Jessica Chastain"
					],
					"tags": [
						"Science Fiction",
						"Space",
						"Love",
						"Adventure"
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
				},
				{
					"title": "Inception",
					"poster": "/images/poster/inception.png",
					"director": "Christopher Nolan",
					"actors": [
						" Leonardo DiCaprio",
						"Joseph Gordon-Levitt",
						"Ellen Page"
					],
					"tags": [
						"Science Fiction",
						"Action",
						"Suspense"
					]
				},
				{
					"title": "Dunkirk",
					"poster": "/images/poster/dunkirk.png",
					"director": "Christopher Nolan",
					"actors": [
						"Fionn Whitehead",
						"Barry Keoghan",
						"Mark Rylance"
					],
					"tags": [
						"War",
						"Suspense"
					]
				},
				{
					"title": "Interstellar",
					"poster": "/images/poster/interstellar.png",
					"director": "Christopher Nolan",
					"actors": [
						"Matthew McConaughey",
						"Anne Hathaway",
						"Jessica Chastain"
					],
					"tags": [
						"Science Fiction",
						"Space",
						"Love",
						"Adventure"
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

