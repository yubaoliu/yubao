---
title:  "Welcome to Jekyll!"
---

# Install and Usage
## Overview
[jekyllrb-doc](https://jekyllrb.com/docs/)

## Run server
``sh
bundle exec jekyll serve  --watch
``

# Frontmatter
permalink: /:categories/:year/:month/:day/:title.html (.php)

# Themes
## Deploy your theme
1. Download from [RubygemsThemes](https://rubygems.org/) or [jekyllthemes](http://jekyllthemes.org/)
1. Search `jekyll-theme`
1. vim *gemfile*:
``
gem "classic-jekyll-theme"
``
1. Run ``bundle install``
1. Vim *_config.yaml*:
``
theme: classic-jekyll-theme
``

## Recommeded Themes
1. [bohu-jekyll-theme](https://llawlight.github.io/bohu-jekyll-theme/)
2. [classic-jekyll-theme](https://github.com/Balancingrock/classic-jekyll-theme)
1. [suyan/suyan.github.io](https://github.com/suyan/suyan.github.io)

# Grammer
## Loop

~~~
{% for post in site.posts %}
  {{ post.title }} <br>
{% endfor %}
~~~

## Condition sentence

``or`` and ``and`` can be used in condition

```
{% if page.title == "My First Post" %}
  This is the first post
{% elsif page.title == "My Second Post" %}
  This is the second post
{% else %}
    This is another post
{% endif %}
```

## Access yml file

_data/people.yml:
```
- name: "name-A"
  occupation: "O-A"
- name: "naeme-B"
  occupation: "O-B"
- name: "konan"
  occupation: "tantei"
```

home.html:

```
\{\% for person in site.data.people %}
  \{\{ person.name }}, {{ person.occupation }}
\{\% endfor %}
```

## Access static_files

```
\{\% for file in site.static_files %}
  \{\{ file.path}} <br>
\{\% endfor %}
```

- *file.basename*
- *file.extname*



# Math - Latex
Refer
1. [Write LaTeX Equations in Jekyll Using MathJax & Kramdown](https://lyk6756.github.io/2016/11/25/write_latex_equations.html)
2. [http://docs.mathjax.org/en/latest/start.html#using-a-content-delivery-network-cdn](http://docs.mathjax.org/en/latest/start.html#using-a-content-delivery-network-cdn)


# Images

*image.html*:

```html
<img src="{{ include.file }}" alt="{{ include.description }}">
<span class="caption">{{ include.description }}</span>
```

Including the file:

```sh
---
layout: post
title: Image Caption Example
---

\{\% include image.html file="img.jpg" description="Triangle_area_from_coordinates" \%\}
```


{% include image.html file="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Triangle_area_from_coordinates_JCB.jpg/732px-Triangle_area_from_coordinates_JCB.jpg" description="This is an image." height="240" weight="320" %}


## Reference
- [How to Create Image Captions with Jekyll](https://www.kevinmcgillivray.net/captions-for-images-with-jekyll/)


<hr>

# Original Example

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
