```
rails g migration AddShortDescToModles short_desc:text
```

```
def create
    @post = BlogPost.new(post_params)
    @post.short_desc = generate_short_description(@post.content)
//
  end
  ```

```
  def update
    @post.attributes = post_params
    @post.short_desc = generate_short_description(@post.content)
//
  end
  ```

  ```
   private

  def generate_short_description(content)
    ActionController::Base.helpers.strip_tags(content.to_s).truncate(200)
  end
  ```

  ```
     params.require(:blog_post).permit(
      :short_desc,
      //
    )
  end```