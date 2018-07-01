# Restful API 设计

## 一、Resource

在 Restful API 中，每个API请求可以抽象为对某一种资源的访问。基于这一点，我们设计了每一个 API 对应的资源，通过 HTTP 方法对相应资源做增删改查操作：

* **/api/user**: 用户

* **/api/admin**: 管理员

* **/api/owner**: 影院管理者

* **/api/session**: 用户会话，用于登录登出

* **/api/movie**: 单个影片

* **/api/movies**: 多个影片

* **/api/cinema**: 单个影院

* **/api/cinemas**: 多个影院

* **/api/schedule**: 单个电影排片

* **/api/schedules**: 多个电影排片

* **/api/order**: 单个订单

* **/api/orders**: 多个订单

* **/api/comment**: 单个评论

* **/api/comments**: 多个评论

---

## 二、Http 方法

* **POST**: 添加资源

* **GET**: 获取资源

* **PUT**: 完整更新资源，需提供完整资源对象

* **PATCH**: 局部更新资源，提供局部更新字段

* **DELETE**: 删除资源




