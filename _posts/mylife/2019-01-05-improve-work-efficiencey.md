---
layout: "post"
title: "Improve Work Efficiencey"
date: "2019-01-05 10:57"
---


# Marp
## Header

```yaml
<!-- page_number: true -->
<!-- $size: 16:9 -->
<!-- $theme: gaia -->
```

## Background

Local:

```sh
![bg](https://www.colesclassroom.com/wp-content/uploads/2017/08/Sunset-pexels-photo-132037_BLOG.jpg)
```
For global:

```css
<style>
.slide {
  background: url(bg-image.jpg) no-repeat center center;
  background-size: cover;
}
</style>
```

## figure

```markdown
![My image](/images/my-image.png)

{:.image-caption}
*The caption for my image*

.image-caption {
  text-align: center;
  font-size: .8rem;
  color: light-grey;
}
```

## Marp Next (Marpit)

```markdown
---
backgroundImage: url(bg-image.jpg)
---
```
OR

```css
<style>
section {
  background: #fff url(bg-image.jpg) no-repeat center center;
  background-size: cover;
}
</style>
```
