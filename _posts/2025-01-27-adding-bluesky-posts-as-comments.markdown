---
layout: post
title:  "How to Add Bluesky Comments to Jekyll Blog Hosted on GitHub Pages"
date:   2025-01-27 21:07:00 -0500
categories: 
  - jekyll 
  - blog
  - bluesky
  
---

TLDR: If you just want to see what I did, please check out the [git commit].

Hopefully this will help someone who is trying to setup Bluesky comments on a [Jekyll] blog hosted on [GitHub Pages].

Before you begin, this will be a lot easier if you're using [Jekyll] and [Minima] hosted on [GitHub Pages]. Check out my
previous [blog post](blog_post) for more information.

I added a new file [`_includes/bluesky_comments.html`](bluesky_comments.html), just in case I wanted to add more to it later:
```html
<div id="bluesky-comments"></div>
```

Then I pulled [`_includes/custom-head.html`](custom-head.html) and [`_layouts/post.html`](post.html) from the [Minima] repo and modified them.

On the bottom of [`_layouts/post.html`](post.html), underneath the disqus comment section, I added:
```liquid
  {%- if page.bluesky_post_uri -%}
    {%- include bluesky_comments.html -%}
  {%- endif -%}
```

Then I added the css and react / javascript to the [`_includes/custom-head.html`](custom-head.html) file.
```liquid
{%- if page.bluesky_post_uri and jekyll.environment == "production" -%}
<link rel="stylesheet" href="https://unpkg.com/bluesky-comments@0.8.0/dist/bluesky-comments.css">
<!-- Add this new importmap before any other scripts -->
<script type="importmap">
  {
    "imports": {
      "react": "https://esm.sh/react@18",
      "react-dom": "https://esm.sh/react-dom@18"
    }
  }
</script>
<!-- Add this new module script -->
<script type="module">
  import {BlueskyComments} from 'https://unpkg.com/bluesky-comments@0.8.0/dist/bluesky-comments.es.js';
  document.addEventListener('DOMContentLoaded', function() {
    const uri = '{{page.bluesky_post_uri}}';
    const author = 'uglydata.dev';
    BlueskyComments.init('bluesky-comments', {
      uri,
      author,
      commentFilters: [BlueskyComments.Filters.NoPins],
    });
  });
</script>
{%- endif -%}
```

This will add the div if there is a uri defined in the post.

Then I (manually, ugh) posted on Bluesky, and added the 
[Bluesky post](bluesky_post)'s uri to the [blog post](blog_post)'s markdown page.

```markdown
bluesky_post_uri: https://bsky.app/profile/uglydata.dev/post/3lgpcc66x4c2m
```

This isn't a perfect solution, but it is a fast and easy one. If you have any questions, please post them on Bluesky below!

Things I would do in the future to improve this:
- Automate the Bluesky posting process.
  - Also add the post uri to the markdown post.
- Host the required css and js on the GitHub Pages site.
- Rewrite the javascript in something more fun and less React.

This was mostly thanks to the work of [Emily Liu] and [Cory Zue]. And Cory, if you're reading this, this took me more than five minutes.

[Using Bluesky posts as blog comments](https://emilyliu.me/blog/comments) by [Emily Liu]
[Adding Bluesky-powered comments to any website in five minutes](https://www.coryzue.com/writing/bluesky-comments/) by [Cory Zue]
[Adding Bluesky comments to your Jekyll Site](https://khattamicah.xyz/portfolio/research-and-writing/writing/blogs/2024-11-25-adding-bluesky-comments/) by [Micah Alex]

[Emily Liu]: https://emilyliu.me/
[Cory Zue]: https://www.coryzue.com/
[Micah Alex]: https://khattamicah.xyz

[Minima]: https://github.com/jekyll/minima
[Jekyll]: https://jekyllrb.com/
[GitHub Pages]: https://pages.github.com/

[git commit]: https://github.com/pastanton/pastanton.github.io/commit/dd9165397c0ece65ad3032b501972560862d79e6
[bluesky_comments.html]: https://github.com/pastanton/pastanton.github.io/blob/dd9165397c0ece65ad3032b501972560862d79e6/_includes/bluesky_comments.html
[custom-head.html]: https://github.com/pastanton/pastanton.github.io/blob/dd9165397c0ece65ad3032b501972560862d79e6/_includes/custom-head.html
[post.html]: https://github.com/pastanton/pastanton.github.io/blob/dd9165397c0ece65ad3032b501972560862d79e6/_layouts/post.html
[blog_post]: https://github.com/pastanton/pastanton.github.io/blob/dd9165397c0ece65ad3032b501972560862d79e6/_posts/2025-01-26-creating-a-blog.markdown
[bluesky_post]: https://bsky.app/profile/uglydata.dev/post/3lgpcc66x4c2m
[Bluesky]: https://bsky.app/