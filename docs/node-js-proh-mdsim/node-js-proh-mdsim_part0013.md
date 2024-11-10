# 第9章：实现用户认证和授权

在本章中，我们将重点实现用户认证和授权，以确保我们的博客应用程序的安全性。用户认证确保只有注册用户才能访问某些功能，而授权则控制每个用户的访问级别和权限。让我们开始吧！

## 9.1 用户模型和注册

首先，让我们更新我们的用户模型，以包含与认证相关的字段。在`models/user.js`文件中，修改代码如下：

```jsjavascript

const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({

username: { type: String, required: true, unique: true },

email: { type: String, required: true, unique: true },

password: { type: String, required: true },

});

const User = mongoose.model('User', userSchema);

module.exports = User;

```

在这里，我们将`username`、`email`和`password`字段添加到用户模式中。`username`和`email`字段被标记为`required`（必填）和`unique`（唯一），确保每个用户拥有唯一的用户名和电子邮件地址。`password`字段将存储哈希后的密码以确保安全。

为了启用用户注册，我们将在`routes/users.js`文件中创建一个注册路由。添加以下代码：

```jsjavascript

const express = require('express');

const router = express.Router();

const bcrypt = require('bcrypt');

const User = require('../models/user');

// User registration route

router.post('/register', async (req, res) => {

const { username, email, password } = req.body;

try {

// Check if the username or email already exists

const existingUser = await User.findOne({ $or: [{ username }, { email }] });

if (existingUser) {

return res.status(409).json({ error: 'Username or email already exists' });

}

// Hash the password

const hashedPassword = await bcrypt.hash(password, 10);

// Create a new user

const newUser = new User({ username, email, password: hashedPassword });

await newUser.save();

res.status(201).json({ message: 'User registered successfully' });

} catch (error) {

res.status(500).json({ error: 'An error occurred while registering the user' });

}

});

module.exports = router;

```

在这段代码中，我们处理对`/register`端点的`POST`请求。首先，我们检查提供的用户名或电子邮件是否已经存在于数据库中。如果找到具有相同用户名或电子邮件的用户，我们返回409状态码并附带错误信息。

如果用户名和电子邮件唯一，我们使用bcrypt对密码进行哈希处理，安全性设定成本因子为10。然后，我们创建一个带有哈希密码的新用户实例，并将其保存到数据库中。

## 9.2 用户登录与认证

接下来，让我们实现用户登录功能。更新`routes/users.js`文件，添加以下代码：

```jsjavascript

const express = require('express');

const router = express.Router();

const bcrypt = require('bcrypt');

const jwt = require('jsonwebtoken');

const User = require('../models/user');

// User login route

router.post('/login', async (req, res) => {

const { username, password } = req.body;

try {

// Check if the user exists

const user = await User.findOne({ username });

if (!user) {

return res.status(401).json({ error: 'Invalid username or password' });

}

// Compare the provided password with the stored hashed password

const passwordMatch = await bcrypt.compare(password, user.password);

if

(!passwordMatch) {

return res.status(401).json({ error: 'Invalid username or password' });

}

// Generate a JWT token

const token = jwt.sign({ username: user.username }, 'your-secret-key');

res.status(200).json({ token });

} catch (error) {

res.status(500).json({ error: 'An error occurred while logging in' });

}

});

module.exports = router;

```

在这段代码中，我们处理对`/login`端点的`POST`请求。首先，我们检查数据库中是否存在提供的用户名。如果没有，我们返回401状态码并附带错误信息。

如果找到该用户，我们使用bcrypt比较提供的密码和存储的哈希密码。如果密码匹配，我们使用`jsonwebtoken`库生成一个JSON Web令牌（JWT）。该JWT将用于认证和授权目的。

然后，令牌作为响应返回给客户端。

## 9.3 使用身份验证中间件保护路由

为了保护某些路由并允许只有经过认证的用户访问它们，我们将创建一个身份验证中间件。在`middleware/auth.js`文件中，添加以下代码：

```jsjavascript

const jwt = require('jsonwebtoken');

// Authentication middleware

const authenticate = (req, res, next) => {

const token = req.headers.authorization;

if (!token) {

return res.status(401).json({ error: 'Unauthorized' });

}

try {

const decoded = jwt.verify(token, 'your-secret-key');

req.user = decoded.username;

next();

} catch (error) {

res.status(401).json({ error: 'Invalid token' });

}

};

module.exports = authenticate;

```

在这段代码中，我们定义了一个名为`authenticate`的身份验证中间件函数。该中间件检查请求的`Authorization`头中是否存在JWT令牌。如果没有找到令牌，我们返回一个401状态码，并附带“未授权”错误信息。

如果存在令牌，我们使用与令牌生成相同的密钥进行验证。如果令牌有效，我们从解码后的令牌中提取用户名，并将其设置在`req.user`属性中以供后续使用。

## 9.4 保护路由并实现授权

现在，我们已经有了身份验证中间件，可以保护路由并实现授权。在`routes/posts.js`文件中，更新代码如下：

```jsjavascript

const express = require('express');

const router = express.Router();

const Post = require('../models/post');

const authenticate = require('../middleware/auth');

// Create post route (protected)

router.post('/create', authenticate, (req, res) => {

// Rest of the code

});

// Update post route (protected)

router.put('/update/:postId', authenticate, (req, res) => {

// Rest of the code

});

// Delete post route (protected)

router.delete('/delete/:postId', authenticate, (req, res) => {

// Rest of the code

});

module.exports = router;

```

在这段代码中，我们将`authenticate`中间件应用于`/create`、`/update`和`/delete`路由。这确保了只有经过认证的用户可以访问这些路由。包含已认证用户用户名的`req.user`属性可以用于授权逻辑。

现在，只有经过认证的用户才能创建、更新或删除博客文章。

## 9.5 总结

做得好！在这一章中，我们在博客应用中实现了用户认证和授权。我们为用户创建了一个注册路由，供用户注册，一个登录路由，供用户进行身份验证，并保护了某些

路由已被保护，确保只有经过认证的用户可以访问它们。

我们还通过使用从JWT令牌中提取的用户名实现了一个简单的授权机制。这为未来构建更细粒度的访问控制和权限系统奠定了基础。
