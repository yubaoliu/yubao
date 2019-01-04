---
title: "Web Development Notes"
---

# Dev Environments
## Essential tools
- atom
- Activate Power Mode (just for fun)
- emmet
- markdown-writer

**How to install plugins:**
E.g.:

```sh
cd ~/.atom/packages
git clone https://github.com/emmetio/emmet-atom
cd emmet-atom
npm install
```


### **emmet**

For example:

! + TAB ->

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>

</body>
</html>
~~~

<hr>

div*3 + TAB ->

~~~html
    <div></div>
    <div></div>
    <div></div>
~~~
<hr>

div{YO}*3 ->

{% highlight html %}
<div>YO</div>
<div>YO</div>
<div>YO</div>
{% endhighlight %}

<hr>

div{Yo$}*3 ->

{% highlight html %}
      <div>Yo1</div>
      <div>Yo2</div>
      <div>Yo3</div>
{% endhighlight %}

<hr>

(div{Yo$}>p)*3 ->
{% highlight HTML %}
<div>Yo1
  <p></p>
</div>
<div>Yo2
  <p></p>
</div>
<div>Yo3
  <p></p>
</div>
{% endhighlight %}

<hr>
.a ->

```HTML
<div class="a"></div>
```

<hr>
span.a ->
```html
<span class="a"></span>
```


###  markdown-writer
Make Atom a better Markdown editor and an easier static blogging tool.
**setting**:

| item                 | values  |
|:-------------------- |:------- |
| Site Engine          | jekyll  |
| Site image directory | images/ |


# comments
- [Gitment](https://github.com/imsun/gitment)
- [gitalk](https://gitalk.github.io/)
- [disqus](https://disqus.com/)

# Jekyll
## plugins
- [Jekyll Admin](https://jekyll.github.io/jekyll-admin/)
- [jekyll-paginate](https://github.com/jekyll/jekyll-paginate)

# Usefule Websites
- [tinypng](https://tinypng.com/)
