# HTML/CSS Intro with Tumblr Themes

Goal of this tutorial is introduction to HTML/CSS and basics of Tumblr theme building

---
## 1. Page skeleton

Let's open your theme editor by going to

```
http://tumblr.com/customize/<NAME-OF-YOUR-TEST-BLOG-HERE>
```

There are some basic elements are common to any web page. Here are the basics:
 
 
```html
<!DOCTYPE HTML>
<html lang="en">
<head>
    <title>Amazing Tumblr blog</title>
</head>
<body>
<header>
    <h1>Title of this amazing blog</h1>
    <p>Description goes here</p>
</header>

<section>
    <article>
        <h2>My text post</h2>
    </article>
</section>

<footer>
    <nav>
        Previous page / Next page
    </nav>
</footer>
</body>
</html>
```

Click 'update' and see the above HTML render in your theme.

---
## 2. Styles

Let's add some styling. Copy and insert code below before `</head>` in your theme:

```html
<style src="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.css"></style>
<style>
    body {
        font-family: "Helvetica";
    }
    header {
        text-align: center;
        border-bottom: 2px solid rgb(0, 0, 0);
    }
    article {
        background: rgb(240, 240, 240);
        padding: 20px;
        margin: 20px;
    }
    footer {
        border-top: 2px solid black;
        text-align: center;
    }
</style>
```

You will see that theme looks a bit better now.

---
## 3. Actual content

Tumblr themes work by showing actual content in place of certain tags. For example:

**Title of the browser tab**
Replace this: `<title>Amazing Tumblr blog</title>`
With this: `<title>{Title}</title>`

**Big title on the top of the page**
Replace this: `<h1>Amazing Tumblr blog</h1>`
With this: `<h1>{Title}</h1>`

**Description under the title**
Replace this: `<p>Description goes here</p>`
With this: `<p>{Description}</p>`


Now you will see actual title and description of your blog!


---
## 4. Actual posts

Right now, your theme is only displaying placeholder post. Your theme needs a special tag to display your posts.

**Replace this:**
```html
<section>
    <article>
        <h2>My tumblr post title</h2>
    </article>
</section>
```

**With this**:
```html
{block:Posts}
<section>
    {block:Text}
    <article>
        {block:Title}
            <h2>{Title}</h2>
        {/block:Title}
        <p>{Body}</p>
    </article>
    {/block:Text}
</section>
{/block:Posts}

```

Now you will have actual posts!

---
## 5. Buttons

Let's add some stuff - 'like' button and note count. Insert the code below right under line with `<p>{Body}</p>` 

```html
<aside>
    <div class='post-note-count'>Notes: {NoteCount}</div>
    <div class='post-like-button'>{LikeButton}</div>
</aside>
```

We now have actual buttons you can interact with!

---
## 6. Post types

Tumblr has several post types, and they all look different. Right now, we are only showing text posts. Let's add image posts and link posts.

`{/block:Text}` is where we stop coding our text post styles. After that line, add following code:

```html
{block:Photo}
<article>
    <img src="{PhotoURL-500}" alt="{PhotoAlt}">
    {block:Caption}
        {Caption}
    {/block:Caption}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
    </aside>
</article>
{/block:Photo}

{block:Link}
<article>
    <h2><a href="{URL}" {Target}>{Name}</a></h2>
    {block:Description}
        {Description}
    {/block:Description}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
    </aside>
</article>
{/block:Link}
```

You will now see that images started appearing!

---
## 7. Reblog button

We have like button, but no reblog button. Let's add one right next to like button.

After this line: `<div class='post-like-button'>{LikeButton}</div>`
Add this line: `<div class='post-reblog-button'>{ReblogButton}</div>`

**NOTE**: You will have to add this to all of the post types we have in the theme.

---
## 8. More styling

Right now, all styles in our theme live in a `<style></style>` tag. Right before `</style>`, add some more styles:

```css
aside{
    border-top: 1px solid rgb(0, 0, 0);
    display: flex;
    padding: 5px;
}
aside div {
    margin: 0 5px;
}
```

---
## 9. Rest of the post styles

Just as before, let's add support for more post types. After `{/block:Link}` line, add following:

```html
{block:Answer}
    <article>
        {Question}
        {Asker}
        {Answer}
        <aside>
            <div class='post-note-count'>Notes: {NoteCount}</div>
            <div class='post-like-button'>{LikeButton}</div>
            <div class='post-reblog-button'>{ReblogButton}</div>
        </aside>
    </article>
{/block:Answer}

{block:Video}
<article>
    {Video-500}
    {block:Caption}
        {Caption}
    {/block:Caption}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
        <div class='post-reblog-button'>{ReblogButton}</div>
    </aside>
</article>
{/block:Video}

{block:Audio}
<article>
    {AudioPlayerWhite}
    {block:Caption}
        {Caption}
    {/block:Caption}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
        <div class='post-reblog-button'>{ReblogButton}</div>
    </aside>
</article>
{/block:Audio}

{block:Quote}
<article>
    {Quote}
    {block:Source}
        {Source}
    {/block:Source}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
        <div class='post-reblog-button'>{ReblogButton}</div>
    </aside>
</article>
{/block:Quote}

{block:Photoset}
<article>
    {Photoset-500}
    {block:Caption}
        {Caption}
    {/block:Caption}
    <aside>
        <div class='post-note-count'>Notes: {NoteCount}</div>
        <div class='post-like-button'>{LikeButton}</div>
        <div class='post-reblog-button'>{ReblogButton}</div>
    </aside>
</article>
{/block:Photoset}
```

Now you will see all post types displayed in your theme.

---
## 10. Previous / Next buttons

You will see that we have prev/next buttons on the bottom of the page, but they don't do anything. That's
because they are just placeholders. If we want them to actually do something, we need to change a few things.

Replace these lines:
```html
<nav>
    Previous page / Next page
</nav>
```

With this:
```html
<nav>
{block:PreviousPage}
    <a class='previous-button' href="{PreviousPage}">Previous page</a>
{/block:PreviousPage}
{block:NextPage}
    <a class='next-button' href="{NextPage}">Next page</a>
{/block:NextPage}
</nav>
```

Let's also add some basic styling. Right before `</style>`, add:

```
.previous-button,
.next-button {
    display: inline-block;
    padding: 10px;
    margin: 10px;
    border-radius: 3px;
    text-decoration: none;
    background: black;
    color: white;
}
```

Now we have actual working buttons.

---
## Bonus tasks

- Style the page in the way you like it. [HERE](http://w3schools.com/cssref) is a reference to all the CSS properties you can use

