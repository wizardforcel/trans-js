# 第7章：添加评论功能

在这一章中，我们将通过添加用户对博客文章发表评论的功能来增强我们的博客应用。评论为用户提供了与内容互动并分享想法的方式。让我们深入了解实现评论功能吧！

## 7.1 创建评论模型

首先，让我们创建一个新的模型`Comment`，用于表示博客文章上的评论。在`models/comment.js`文件中，添加以下代码：

```jsjavascript

const mongoose = require('mongoose');

const commentSchema = new mongoose.Schema({

content: {

type: String,

required: true,

},

postId: {

type: mongoose.Schema.Types.ObjectId,

ref: 'Post',

required: true,

},

createdAt: {

type: Date,

default: Date.now,

},

});

const Comment = mongoose.model('Comment', commentSchema);

module.exports = Comment;

```

在这段代码中，我们定义了`Comment`模式，其中包括`content`字段用于存储评论内容，`postId`字段用于与相应的博客文章建立关系，以及`createdAt`字段用于存储评论的创建日期。我们导出了`Comment`模型，以便在应用的其他部分使用。

## 7.2 添加评论创建路由

接下来，让我们添加一个路由来处理评论的创建。在`routes/comments.js`文件中，添加以下代码：

```jsjavascript

const express = require('express');

const router = express.Router();

const Comment = require('../models/comment');

// Create comment route

router.post('/create', (req, res) => {

const { content, postId } = req.body;

// Validate input fields

if (!content || !postId) {

return res.status(400).json({ error: 'Please provide comment content and associated post ID' });

}

// Create a new comment

const newComment = new Comment({ content, postId });

// Save the comment to the database

newComment.save()

.then(() => {

res.status(201).json({ message: 'Comment created successfully' });

})

.catch((error) => {

res.status(500).json({ error: 'An error occurred while creating the comment' });

});

});

module.exports = router;

```

在这段代码中，我们定义了一个路由来处理评论的创建。我们从请求体中提取`content`和`postId`，并验证这两个字段是否存在。如果没有提供，我们返回一个400状态码和错误信息。

我们使用提取的数据创建一个新的`Comment`模型实例，并通过`save`方法将其保存到数据库中。如果保存操作成功，我们返回一个201状态码和成功信息。否则，我们返回一个500状态码和错误信息。

## 7.3 获取某个帖子的评论

为了获取特定博客文章的所有评论，我们将添加一个路由，该路由接受一个帖子ID作为参数。在`routes/comments.js`文件中，添加以下代码：

```jsjavascript

// Get comments by post ID route

router.get('/post/:postId', (req, res) => {

const postId = req.params.postId;

// Find comments by post ID

Comment.find({ postId })

.then((comments) => {

res.status(200).json(comments);

})

.catch((error) => {

res.status(500).json({ error: 'An error occurred while retrieving comments' });

});

});

module.exports = router;

```

在这段代码中，我们定义了一个接受

`postId`作为参数。我们使用`Comment`模型的`find`方法来获取所有与指定帖子ID相关联的评论。如果获取成功，我们返回一个200状态码和评论数组。如果发生错误，我们返回一个500状态码和错误信息。

## 7.4 在前端展示评论

为了在前端的博客页面展示评论，更新你的博客帖子模板（例如，`views/post.ejs`），并加入以下代码：

```jshtml

<!-- Your existing blog post content here -->

<!-- Comments section -->

<h2>Comments</h2>

<div id="comments-container">

<% comments.forEach((comment) => { %>

<div class="comment">

<p><%= comment.content %></p>

<p>Posted on <%= comment.createdAt.toDateString() %></p>

</div>

<% }) %>

</div>

<!-- Comment form -->

<form id="comment-form" action="/comments/create" method="POST">

<input type="hidden" name="postId" value="<%= post._id %>">

<textarea name="content" placeholder="Enter your comment"></textarea>

<button type="submit">Submit</button>

</form>

```

在这段代码中，我们遍历服务器传递的`comments`数组，并显示每条评论的内容和创建日期。我们还提供了一个评论表单，其中包含一个隐藏的帖子 ID 字段和一个用于输入评论内容的文本框。

## 7.5 提升用户体验

为了提升用户体验，我们可以添加一些 JavaScript 功能，支持通过 AJAX 提交评论，并动态更新评论区。将以下代码添加到你的前端 JavaScript 文件中（例如，`public/js/main.js`）：

```jsjavascript

const commentForm = document.getElementById('comment-form');

const commentsContainer = document.getElementById('comments-container');

commentForm.addEventListener('submit', (event) => {

event.preventDefault();

const formData = new FormData(commentForm);

const content = formData.get('content');

const postId = formData.get('postId');

const comment = { content, postId };

fetch('/comments/create', {

method: 'POST',

headers: {

'Content-Type': 'application/json',

},

body: JSON.stringify(comment),

})

.then((response) => response.json())

.then(() => {

// Clear the comment form

commentForm.reset();

// Fetch and update the comments section

fetch(`/comments/post/${postId}`)

.then((response) => response.json())

.then((comments) => {

updateComments(comments);

})

.catch((error) => {

console.error('An error occurred while retrieving comments:', error);

});

})

.catch((error) => {

console.error('An error occurred while submitting the comment:', error);

});

});

function updateComments(comments) {

commentsContainer.innerHTML = '';

comments.forEach((comment) => {

const commentElement = document.createElement('div');

commentElement.classList.add('comment');

const contentElement = document.createElement('p');

contentElement.textContent = comment.content;

const dateElement = document.createElement('p');

dateElement.textContent = `Posted on ${new Date(comment.createdAt).toDateString()}`;

commentElement.appendChild(contentElement);

commentElement.appendChild(dateElement);

commentsContainer.appendChild(commentElement);

});

}

```

在这段代码中，我们为评论表单的提交事件添加了一个事件监听器。当表单提交时，我们会阻止默认的表单提交行为，并提取评论内容和帖子 ID。

然后我们发送一个 POST 请求到`/`

我们将评论数据作为 JSON 发送到`comments/create`端点。如果请求成功，我们清空评论表单，并获取更新后的评论内容。然后调用`updateComments`函数，动态更新评论区，展示新评论。

## 7.6 小结

恭喜！在本章中，我们成功实现了博客应用中的评论功能。用户现在可以对博客帖子发表评论，评论会存储在数据库中。我们还通过动态更新评论区、无需刷新页面，增强了用户体验。
