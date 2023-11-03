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

