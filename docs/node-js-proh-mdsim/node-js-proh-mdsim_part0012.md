# 第8章：在我们的博客应用中实现搜索

在这一章中，我们将通过添加搜索功能来增强我们的博客应用，允许用户根据关键词搜索特定的博客文章。实现搜索将改善用户体验，并使用户更容易找到相关内容。让我们开始吧！

## 8.1 设置搜索索引

为了启用搜索功能，我们将使用一个强大的搜索引擎——Elasticsearch。按照以下步骤在你的应用中设置Elasticsearch：

### 8.1.1 安装Elasticsearch

首先，你需要在你的系统上安装Elasticsearch。访问Elasticsearch的官方网站（https://www.elastic.co/downloads/elasticsearch）并下载适用于你操作系统的版本。按照Elasticsearch提供的安装说明完成安装过程。

### 8.1.2 创建Elasticsearch索引

一旦安装了Elasticsearch，你需要创建一个索引来存储你的博客文章。索引类似于数据库表，用于组织和存储数据。在终端中运行以下命令来创建一个名为"blog_posts"的索引：

```jsshell

curl -XPUT http://localhost:9200/blog_posts

```

### 8.1.3 安装Elasticsearch客户端库

为了在我们的Node.js应用中与Elasticsearch进行交互，我们将使用官方的Elasticsearch JavaScript客户端库，名为"elasticsearch"。在你的项目目录中运行以下命令来安装它：

```jsshell

npm install elasticsearch

```

设置好Elasticsearch并安装客户端库后，我们可以继续实现搜索功能。

## 8.2 实现搜索路由

我们先从创建一个新路由来处理搜索请求开始。在`routes/search.js`文件中，添加以下代码：

```jsjavascript

const express = require('express');

const router = express.Router();

const { Client } = require('elasticsearch');

// Create Elasticsearch client

const client = new Client({ node: 'http://localhost:9200' });

// Search route

router.get('/', (req, res) => {

const { query } = req.query;

// Perform search query

client

.search({

index: 'blog_posts',

body: {

query: {

match: {

content: query,

},

},

},

})

.then((response) => {

const hits = response.body.hits.hits.map((hit) => hit._source);

res.status(200).json(hits);

})

.catch((error) => {

res.status(500).json({ error: 'An error occurred while performing the search' });

});

});

module.exports = router;

```

在这段代码中，我们创建了一个新路由来处理对`/search`端点的GET请求。我们从请求的查询参数中提取搜索查询。

使用Elasticsearch客户端，我们对"blog_posts"索引执行搜索查询。我们使用匹配查询在博客帖子的"content"字段中搜索提供的查询内容。搜索结果作为命中返回，我们将其映射以提取源数据（即博客帖子的内容）。

如果搜索成功，我们返回一个200状态码，并将命中结果以JSON格式返回。如果出现错误，我们返回一个500状态码，并附带错误信息。

## 8.3 更新博客帖子创建路由

为了保持搜索索引的最新状态，我们需要更新创建新博客帖子的路由。在`routes/posts.js`文件中，按以下方式更新创建路由：

```jsjavascript

const express = require('express');

const router = express.Router();

const Post = require('../models/post');

const { Client } = require('elasticsearch');

// Create Elasticsearch client

const client

= new Client({ node: 'http://localhost:9200' });

// Create post route

router.post('/create', (req, res) => {

const { title, content } = req.body;

// Validate input fields

if (!title || !content) {

return res.status(400).json({ error: 'Please provide a title and content for the post' });

}

// Create a new post

const newPost = new Post({ title, content });

// Save the post to the database

newPost.save()

.then(() => {

// Index the new post in Elasticsearch

client.index({

index: 'blog_posts',

body: {

title,

content,

},

});

res.status(201).json({ message: 'Post created successfully' });

})

.catch((error) => {

res.status(500).json({ error: 'An error occurred while creating the post' });

});

});

module.exports = router;

```

在这段代码中，在将新帖子保存到数据库后，我们使用客户端的`index`方法将帖子索引到Elasticsearch中。我们指定索引为"blog_posts"，并将帖子的标题和内容作为索引请求的主体。

这确保了新创建的帖子被添加到搜索索引中，从而使其可以被搜索。

## 8.4 将搜索表单添加到前端

为了允许用户进行搜索，我们将在前端添加一个搜索表单。更新你博客的主页模板（例如，`views/home.ejs`），并添加以下代码：

```jshtml

<!-- Your existing homepage content here -->

<!-- Search form -->

<form id="search-form" action="/search" method="GET">

<input type="text" name="query" placeholder="Search...">

<button type="submit">Search</button>

</form>

```

这段代码添加了一个简单的搜索表单，其中包括一个用于输入搜索查询的文本框和一个提交按钮。表单的`action`设置为`/search`端点，这是我们在后端定义的。

## 8.5 显示搜索结果

要在专用的搜索结果页面上显示搜索结果，请在你的视图目录中创建一个新的模板文件，命名为`search_results.ejs`。在文件中添加以下代码：

```jshtml

<!-- Your existing page structure and header here -->

<!-- Search results -->

<h2>Search Results</h2>

<div id="search-results-container">

<% if (results.length === 0) { %>

<p>No results found.</p>

<% } else { %>

<% results.forEach((result) => { %>

<div class="search-result">

<h3><%= result.title %></h3>

<p><%= result.content %></p>

</div>

<% }) %>

<% } %>

</div>

<!-- Your existing footer and scripts here -->

```

在这段代码中，我们遍历从服务器传递过来的`results`数组，并显示每个搜索结果的标题和内容。如果没有找到结果，我们会显示一条消息，指示未找到任何结果。

## 8.6 总结

恭喜！在这一章节中，我们通过Elasticsearch在博客应用中实现了搜索功能。现在用户可以根据关键词搜索特定的博客文章，从而提升整体用户体验。

我们设置了Elasticsearch，创建了搜索路由，更新了博客文章创建路由以便索引文章，添加了一个搜索表单到前端，并在专门的页面上展示了搜索结果。
