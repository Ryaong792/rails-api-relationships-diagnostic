# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
    Joining tables conbine two tables togethere without really chaning your orginal table.
    Also helps organizing your data and make it less complex when adding/removing
    relationships

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
  class Profiles < ActiveModel::Serializer
  attributes :id, :given_name, :surnamem, email
end

class Movies < ActiveModel::Serializer
attributes :id, :title, :release_date, :length
end

class Favorites < ActiveModel::Serializer
  attributes :id, :date
  has_one :profile
  has_one :movies
end
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
    has_many :favorites, class_name: 'Movies'

    has_many :movies, through: :favorite
  end

  ```rb
  class Movie < ActiveRecord::Base
  has_many :prfiles, class_name: 'Movies'

  has_many :profiles, through: :favorite
end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
  belongs_to :movie, inverse_of: :appointments
  belongs_to :profile, inverse_of: :appointments
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
    to help show what is information is displayed on the page
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
  attributes :id, :given_name, :surnamem, :email, :favorite
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
  bin/rails generate scaffold favorite movies:references profile:references
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    it will destroy all relationship of the item you want to destroy.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    # < Your Response Here >
  ```
