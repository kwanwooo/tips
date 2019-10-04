# JSON Web Token

## 组成
分为三部分的字符串(头部、载荷与签名)

### 头部 header

头部用于描述关于该JAWT最基本的信息，例如类型以及所用的算法等

```javascript
{
    "typ":"JWT",
    "alg":"HS256"
}
```

进行bash64编码

```javascript
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9
```

### 载荷 Payload

实质的信息

```javascript
{
    "iss": "John Wu JWT",
    "iat": 1441593502,
    "exp": 1441594722,
    "aud": "www.example.com",
    "sub": "jrocket@example.com",
    "from_user": "B",
    "target_user": "A"
}
```

iss JWT的签发者
sub JWT所面向的用户
aud 接收JWT的一方
exp 过期时间，unix时间戳
iat 什么时候签发的

将上面的JSON对象进行bash64编码,称为载荷

```javascript
eyJpc3MiOiJKb2huIFd1IEpXVCIsImlhdCI6MTQ0MTU5MzUwMiwiZXhwIjoxNDQxNTk0NzIyLCJhdWQiOiJ3d3cuZXhhbXBsZS5jb20iLCJzdWIiOiJqcm9ja2V0QGV4YW1wbGUuY29tIiwiZnJvbV91c2VyIjoiQiIsInRhcmdldF91c2VyIjoiQSJ9
```

### 签名

将上面的两个编码后的字符串都用 ```.``` 连接,形成

```javascript
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJKb2huIFd1IEpXVCIsImlhdCI6MTQ0MTU5MzUwMiwiZXhwIjoxNDQxNTk0NzIyLCJhdWQiOiJ3d3cuZXhhbXBsZS5jb20iLCJzdWIiOiJqcm9ja2V0QGV4YW1wbGUuY29tIiwiZnJvbV91c2VyIjoiQiIsInRhcmdldF91c2VyIjoiQSJ9
```

最后将上面拼接完成的字符串用HS256算法进行加密，我们需要提供一个密钥（secret）。如果我们用mystar作为密钥的话，那么就可以得到我们加密后的内容

```javascript
rSWamyAYwuHCo7IFAgd1oRpSP7nzL7BF5t7ItqpKViM
```

最后形成完整JWT

```javascript
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJKb2huIFd1IEpXVCIsImlhdCI6MTQ0MTU5MzUwMiwiZXhwIjoxNDQxNTk0NzIyLCJhdWQiOiJ3d3cuZXhhbXBsZS5jb20iLCJzdWIiOiJqcm9ja2V0QGV4YW1wbGUuY29tIiwiZnJvbV91c2VyIjoiQiIsInRhcmdldF91c2VyIjoiQSJ9.rSWamyAYwuHCo7IFAgd1oRpSP7nzL7BF5t7ItqpKViM
```

### 签名的目的

服务器根据JWT的头部alg字段来得知加密算法，计算一遍签名和接收到的签名是否一致，若不一致则表示这个Token已经被修改，应该拒绝这个Token，返回一个HTTP 401 Unauthorized响应。

### 信息会暴露

JWT中，不应该再载荷里面加入任何敏感数据， 比如密码。

### JWT的适用场景

经常用于用户认证和授权系统， 实现Web应用的单点登录等等