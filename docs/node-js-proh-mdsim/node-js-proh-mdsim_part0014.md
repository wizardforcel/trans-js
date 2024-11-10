# 第10章：提升用户体验

在本章中，我们将重点提升博客应用的用户体验，实施如用户个人资料和帖子点赞等功能。这些功能将允许用户个性化他们的账户，并以更具互动性的方式与帖子互动。让我们开始吧！

## 10.1 用户个人资料

为了提供个性化的用户资料，我们将更新用户模型并创建用户资料路由。我们从修改`models/user.js`文件开始：

```jsjavascript

const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({

username: { type: String, required: true, unique: true },

email: { type: String, required: true, unique: true },

password: { type: String, required: true },

bio: { type: String, default: '' },

avatar: { type: String, default: '' },

});

const User = mongoose.model('User', userSchema);

module.exports = User;

```

在这段代码中，我们向用户模式中添加了两个新字段：`bio`和`avatar`。`bio`字段将存储用户的简短简介或描述，而`avatar`字段将保存用户头像的URL。

接下来，让我们在`routes/users.js`文件中创建一个用户个人资料路由：

```jsjavascript

const express = require('express');

const router = express.Router();

const User = require('../models/user');

const authenticate = require('../middleware/auth');

// User profile route (protected)

router.get('/profile', authenticate, async (req, res) => {

try {

const user = await User.findOne({ username: req.user }, { password: 0 });

if (!user) {

return res.status(404).json({ error: 'User not found' });

}

res.status(200).json(user);

} catch (error) {

res.status(500).json({ error: 'An error occurred while fetching the user profile' });

}

});

module.exports = router;

```

在这段代码中，我们创建了一个`GET`路由用于获取用户个人资料。我们使用`authenticate`中间件来确保只有经过身份验证的用户可以访问此路由。`req.user`属性包含已认证用户的用户名。

在路由处理函数中，我们使用`findOne`方法根据用户名查找用户。我们从检索到的用户对象中排除了`password`字段以确保安全。如果找到了用户，我们将返回用户对象作为响应。

## 10.2 帖子点赞

为了让用户能够点赞帖子并与内容互动，我们将更新帖子模型并创建点赞路由。我们从修改`models/post.js`文件开始：

```jsjavascript

const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({

title: { type: String, required: true },

content: { type: String, required: true },

likes: { type: Number, default: 0 },

});

const Post = mongoose.model('Post', postSchema);

module.exports = Post;

```

在这段代码中，我们向帖子模式中添加了一个`likes`字段，用于存储帖子收到的点赞数量。

接下来，让我们在`routes/posts.js`文件中创建一个点赞路由：

```jsjavascript

const express = require('express');

const router = express.Router();

const Post = require('../models/post');

const authenticate = require('../middleware/auth');

// Like post route (protected)

router.put('/like/:postId', authenticate, async (req, res) => {

try {

const postId = req.params.postId;

const post = await Post.findById(postId);

if (!post) {

return res.status(404).json({ error: 'Post not found' });

}

// Check if the user has already liked the post

const hasLiked = post.likes.includes(req.user);

if (hasLiked) {

return res.status(400).json({ error: 'You have already liked this post' });

}

// Increment the likes count and add the user to the likes array

post.likes.push(req.user);

post.likesCount++;

await post.save();

res.status(200).json({ message: 'Post liked successfully' });

} catch (error) {

res.status(500).json({ error: 'An error occurred while liking the post' });

}

});

module.exports = router;

```

在这段代码中，我们创建了一个`PUT`路由用于点赞帖子。`authenticate`中间件确保只有经过身份验证的用户可以访问此路由。我们从请求参数中提取`postId`。

在路由处理函数中，我们首先根据`postId`查找帖子。如果未找到帖子，我们将返回404状态码和错误信息。

接下来，我们通过检查用户的用户名是否出现在帖子的`likes`数组中，来判断用户是否已经点赞。如果用户已经点赞，我们将返回一个400状态码，并附带错误信息。

如果用户还没有点赞该帖子，我们将递增`likesCount`字段，并将用户的用户名添加到`likes`数组中。然后，我们保存更新后的帖子，并作为响应发送成功信息。

## 10.3 总结

恭喜！在本章中，我们实现了用户资料和帖子点赞功能，以增强博客应用的用户体验。用户现在可以通过个人简介和头像个性化他们的资料，并通过点赞与帖子互动。

这些功能增加了个性化和互动性，使得应用变得更加有趣和用户友好。
