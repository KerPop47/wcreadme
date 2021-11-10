# Data Organization: SQL Commands version!

Sketches of what the table create commands are going to be, which outlines:
    - the columns
    - the data types
    - default values
    - linking
    - can be null?


- webcomics(
    webcomic\_id INT NOT NULL AUTO\_INCREMENT,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP
    vernacular\_name VARCHAR NOT NULL,
    english\_name VARCHAR NOT NULL,
    nicknames VARCHAR NOT NULL DEFAULT "[]",
    url\_current VARCHAR NOT NULL,
    url\_start VARCHAR,
    url\_home VARCHAR,
    author VARCHAR,
    picture\_directory VARCHAR,
    overall\_genre VARCHAR,
    overall\_rating FLOAT(4,2),
    overall\_tropes VARCHAR,
    summary MEDIUMTEXT,
    hosting\_sources VARCHAR,
    related\_works VARCHAR,
    num\_pages INT NOT NULL,
    first\_post\_date DATE,
    status ENUM('ongoing', 'complete', 'no longer updating',),
    tvtropes\_page VARCHAR,
    reviewers VARCHAR NOT NULL DEFAULT "[]",
);

- reviews(
    review\_id INT NOT NULL AUTO\_INCREMENT,
    webcomic\_target INT NOT NULL,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP,
    source\_user VARCHAR,
    score\_overall FLOAT(4,2),
    score\_story FLOAT(4,2),
    score\_art FLOAT(4,2),
    score\_reread FLOAT(4,2),
    review MEDIUMTEXT,
    genres VARCHAR NOT NULL DEFAULT "[]",
    tropes VARCHAR NOT NULL DEFAULT "[]",
    number\_found\_useful INT NOT NULL
);

- creators(
    creator\_id INT NOT NULL AUTO\_INCREMENT,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP,
    name VARCHAR NOT NULL,
    picture\_directory VARCHAR,
    site\_url VARCHAR,
    biography MEDIUMTEXT,
    assoc\_works VARCHAR NOT NULL DEFAULT "[]"
);

- users(
    user\_id INT NOT NULL AUTO\_INCREMENT,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP,
    user\_name VARCHAR NOT NULL,
    positive\_reviews VARCHAR NOT NULL DEFAULT "[]",
    all\_reviews VARCHAR NOT NULL DEFAULT "[]",
    minimum\_rating FLOAT(4,2),
    maximum\_rating FLOAT(4,2),
    genres VARCHAR NOT NULL DEFAULT "[]",
    has\_read VARCHAR NOT NULL DEFAULT "[]",
    to\_read VARCHAR NOT NULL DEFAULT "[]"
);

- genres(
    genre\_id INT NOT NULL AUTO\_INCREMENT,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP,
    name VARCHAR NOT NULL,
    tvtropes\_url VARCHAR,
    description MEDIUMTEXT
);

- tropes(
    trope\_id INT NOT NULL AUTO\_INCREMENT,
    insertion\_date TIMESTAMP NOT NULL DEFAULT CURRENT\_TIMESTAMP,
    name VARCHAR NOT NULL,
    tvtropes\_url VARCHAR,
    description MEDIUMTEXT
);
