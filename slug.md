```
gem "friendly_id"
```

```
bundle install
```

```
rails g migration AddSlugToModles slug:uniq
```


```
rails generate friendly_id
```

```
rails db:migrate
```
```
class MOdels < ApplicationRecord
  extend FriendlyId
  friendly_id :field, use: :slugged
end
```


```
@user = User.friendly.find(params[:id])
```

```
   def set_post
      @post = Post.friendly.find(params[:id])
      redirect_to @post, status: :moved_permanently if params[:id] != @post.slug
    end
    
    ```