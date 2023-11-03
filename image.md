```
gem "image_processing", ">= 1.2"
```

```
bin/rails active_storage:install
bin/rails db:migrate
```

```
class Post < ApplicationRecord
  has_one_attached :image
end
```

```
rails generate migration AddAttachmentImageToPosts image:attachment
```


### app/views/posts/_form.html.erb
```
 <div class='pt-8'>
    <%= form.label :image, class: "block" %>
    <%= form.file_field :image, class: "file-input file-input-bordered w-full max-w-xs"  %>
  </div>```

  ```
  ### app/views/posts/_post.html.erb

  ```
    <p class="mb-2">
  <% if post.image.attached? %>
    <strong class="text-md text-gray-800">Image:</strong>
    <div class="mb-2">
      <%= image_tag url_for(post.image), class: "w-full h-auto rounded" %>
    </div>
  <% end %>
</p>
```

