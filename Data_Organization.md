# Data Oganization

What information do we want to store, where

The current design is to store the information in SQL, with the different tables relating to each other. This will ensure, for example, that every review's user will have a user account associated with it.

Databases:
- [Webcomic](#webcomic)
- [Review](#review)
- [Creator](#creator)
- [Users](#user)
- [Genre](#genre)
- [Trope](#trope)

### Webcomic
The thing being reviewed. The Overall values should be calculated and updated every time a new review is submitted, instead of being recalculated every time the comic is queried 

- Name
- Translated name
- Aka
- Link
    - Current
    - Start
    - Home
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
- List of Review IDs
- List of Recommendations 
    - TODO: Expand

Stats like counts can be returned via query quickly, so long as there isn't calculation involved

### Review
Data for each review

- Review ID
- Webcomic
- User
- Score
    - Overall
    - Story
    - Art
    - Reread value
- Review
- Genre
- Tropes
- Date
- Number found useful

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
- Has Read List
- To Read List

### Genre
An entry for every genre

- Name
- TvTropes link
- Description

Info like a list of applicable comics can be generated upon request, as opposed to stored

### Trope
An entry for every trope

- Name
- TvTropes Link (?)
- Description

Info like a list of applicable comics can be generated upon request
