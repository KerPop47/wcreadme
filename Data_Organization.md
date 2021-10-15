#Data Oganization

What information do we want to store, where

The current design is to store the information in SQL, with the different tables relating to each other. This will ensure, for example, that every review's user will have a user account associated with it.

Databases:
- Webcomic
- Creator
- Users

### Webcomic
The thing being reviewed. The Overall values should be calculated and updated every time a new review is submitted, instead of being recalculated every time the comic is queried 

- Name
- URL Link
- Creator
- Picture
- Creation Date
- Overall Genre
- Overall Rating
- Overall Tropes
- Host-generated summary
- no. episodes
- start date
- in/complete
- tvtropes link
- hosting sites/services
- List of Reviews
    - Review
        - User
        - Score
        - Review
        - Genre
        - Tropes
    - Review
        - Etc.

### Creator
Many creators create multiple comics, so it would be good to group them

- Name
- Pic
- site
- bio
- List of webcomics

### User
Our users should have public pages too

- Public name
- User picture
- List of high reviews
- List of all reviews
- Spread of ratings
- Spread of genres