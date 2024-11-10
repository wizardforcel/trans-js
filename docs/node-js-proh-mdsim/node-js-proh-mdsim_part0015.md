# 第 11 章：启用评论

在本章中，我们将实现用户在博客文章中发表评论的功能。启用评论将鼓励讨论和互动，增加我们的博客应用的活跃度。让我们一起实现这个令人兴奋的功能！

## 11.1 评论模型

为了支持评论，我们需要创建一个 Comment 模型。打开 `models/comment.js` 文件并添加以下代码：

```jsjavascript

const mongoose = require('mongoose');

const commentSchema = new mongoose.Schema({

postId: { type: mongoose.Schema.Types.ObjectId, ref: 'Post', required: true },

content: { type: String, required: true },

author: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },

createdAt: { type: Date, default: Date.now },

});

const Comment = mongoose.model('Comment', commentSchema);

module.exports = Comment;

```

在这段代码中，我们使用 Mongoose 的 Schema 定义了评论的结构。每条评论都属于一个特定的帖子（`postId`），并与作者（`author`）关联。`content` 字段保存实际的评论文本，`createdAt` 字段存储评论创建的时间戳。

## 11.2 评论路由

现在，让我们在 `routes/comments.js` 文件中创建处理评论的路由：

```jsjavascript

const express = require('express');

const router = express.Router();

const Comment = require('../models/comment');

const Post = require('../models/post');

const authenticate = require('../middleware/auth');

// Create comment route (protected)

router.post('/create', authenticate, async (req, res) => {

try {

const { postId, content } = req.body;

const post = await Post.findById(postId);

if (!post) {

return res.status(404).json({ error: 'Post not found' });

}

const comment = new Comment({

postId,

content,

author: req.user,

});

await comment.save();

res.status(201).json({ message: 'Comment created successfully' });

} catch (error) {

res.status(500).json({ error: 'An error occurred while creating the comment' });

}

});

// Get comments for a post route

router.get('/post/:postId', async (req, res) => {

try {

const postId = req.params.postId;

const comments = await Comment.find({ postId }).populate('author', 'username');

res.status(200).json(comments);

} catch (error) {

res.status(500).json({ error: 'An error occurred while fetching the comments' });

}

});

module.exports = router;

```

在上面的代码中，我们定义了两条路由。第一条路由（`/create`）处理新评论的创建。它需要身份验证（`authenticate` 中间件），确保只有登录用户才能发表评论。我们从请求体中提取 `postId` 和 `content`。然后，我们检查关联的帖子是否存在。如果帖子存在，我们创建一个新的评论实例，设置相应的值，并将其保存到数据库中。

第二条路由（`/post/:postId`）获取与特定帖子关联的所有评论。我们从请求参数中提取 `postId` 并用它来查找评论。`populate()` 方法用于将 `author` 的 ID 替换为评论作者的实际 `username`。

## 11.3 更新帖子模型

为了能够无缝地获取与帖子关联的评论，我们将更新 Post 模型。打开 `models/post.js` 文件并按如下方式修改：

```jsjavascript

const mongoose = require('mongoose');

const postSchema = new

mongoose.Schema({

title: { type: String, required: true },

content: { type: String, required: true },

likes: { type: Number, default: 0 },

comments: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Comment' }],

});

const Post = mongoose.model('Post', postSchema);

module.exports = Post;

```

在这段更新后的代码中，我们在帖子模式中添加了一个 `comments` 字段。它是一个评论 ID 的数组，引用 Comment 模型。

## 11.4 更新帖子路由

为了将评论与帖子关联起来，我们还需要修改 Post 路由。打开 `routes/posts.js` 文件并进行以下更改：

```jsjavascript

const express = require('express');

const router = express.Router();

const Post = require('../models/post');

const Comment = require('../models/comment');

const authenticate = require('../middleware/auth');

// Get single post route

router.get('/:postId', async (req, res) => {

try {

const postId = req.params.postId;

const post = await Post.findById(postId).populate('comments');

if (!post) {

return res.status(404).json({ error: 'Post not found' });

}

res.status(200).json(post);

} catch (error) {

res.status(500).json({ error: 'An error occurred while fetching the post' });

}

});

// Update post route (protected)

router.put('/:postId', authenticate, async (req, res) => {

try {

const postId = req.params.postId;

const { title, content } = req.body;

const post = await Post.findByIdAndUpdate(

postId,

{ title, content },

{ new: true }

);

if (!post) {

return res.status(404).json({ error: 'Post not found' });

}

res.status(200).json(post);

} catch (error) {

res.status(500).json({ error: 'An error occurred while updating the post' });

}

});

module.exports = router;

```

在第一个路由（`/:postId`）中，我们添加了`populate('comments')`方法来获取与帖子关联的评论。这确保了当我们获取单个帖子时，也能获取到它的评论。

第二个路由（`/:postId`）处理帖子的更新。我们从请求体中提取`postId`、`title`和`content`。我们使用`findByIdAndUpdate`根据ID查找帖子并更新其标题和内容。`{ new: true }`选项确保返回更新后的帖子作为响应。

## 11.5 总结

做得好！在本章中，我们在博客应用程序中实现了评论功能。用户现在可以在帖子下留下评论，从而促进讨论和互动。我们创建了评论模型，添加了用于创建和获取评论的路由，并将评论与帖子关联起来。

留下评论的功能为我们的应用程序增加了互动性，使其更加动态和吸引用户。
