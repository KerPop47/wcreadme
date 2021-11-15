# Data Organization: SQL Commands version!

Sketches of what the table create commands are going to be, which outlines:
    - the columns
    - the data types
    - default values
    - linking
    - can be null?


- Webcomics(
    webcomic_id INT 
        NOT NULL
        AUTO_INCREMENT,
    insertion_date TIMESTAMP
        NOT NULL 
        DEFAULT NOW()
        ON UPDATE CURRENT_TIMESTAMP
    vernacular_name VARCHAR
        NOT NULL,
    english_name VARCHAR
        NOT NULL,
    url_current VARCHAR
        NOT NULL,
    url_start VARCHAR,
    url_home VARCHAR,
    author VARCHAR,
    picture_directory VARCHAR,
    overall_rating FLOAT(4,2),
    summary MEDIUMTEXT,
    num_pages INT
        NOT NULL,
    update_schedule INT,
    first_post_date DATE,
    status INT 
        NOT NULL,
    tvtropes_url VARCHAR,
    PRIMARY KEY (webcomic_id),
    FOREIGN KEY (author)
        REFERENCES Creator(creator_id),
    FOREIGN KEY (hosting_sources)
        REFERENCES Hosting_Sites(host_id),
    FOREIGN KEY (status)
        REFERENCES Statuses(status_id),
    FOREIGN KEY (update_schedule)
        REFERENCES Schedules(schedule_id),
    UNIQUE(vernacular_name),
    UNIQUE(english_name),
    UNIQUE(url_current),
    UNIQUE(url_start),
    UNIQUE(url_home)
);

- Reviews(
    review_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    target_webcomic INT 
        NOT NULL,
    insertion_date  TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    source_user VARCHAR,
    score_overall FLOAT(4,2),
    score_story FLOAT(4,2),
    score_art FLOAT(4,2),
    score_reread FLOAT(4,2),
    review MEDIUMTEXT,
    PRIMARY KEY (review_id),
    FOREIGN KEY (source_user) 
        REFERENCES Users(user_id),
    FOREIGN KEY (target_webcomic) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(source_user,target_webcomic)
);

- Creators(
    creator_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    name VARCHAR 
        NOT NULL,
    picture_directory VARCHAR,
    site_url VARCHAR,
    biography MEDIUMTEXT,
    PRIMARY KEY(creator_id)
);

- Users(
    user_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    user_name VARCHAR 
        NOT NULL,
    minimum_rating FLOAT(4,2),
    maximum_rating FLOAT(4,2),
    PRIMARY KEY(user_id),
    UNIQUE(user_name)
);

- Hosting_Sites(
    host_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    insertion_date TIMESTAMP
        NOT NULL 
        DEFAULT NOW()
        ON UPDATE CURRENT_TIMESTAMP,
    name VARCHAR 
        NOT NULL,
    home_url VARCHAR,
    description MEDIUMTEXT,
    PRIMARY KEY(host_id),
    UNIQUE(name),
    UNIQUE(home_url)
);

- Aliases(
    alias_id INT
        NOT NULL
        AUTO_INCREMENT,
    webcomic_id INT
        NOT NULL,
    alias_name VARCHAR NOT NULL,
    PRIMARY KEY (alias_id),
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(alias_name,webcomic_id)
);

- Genres(
    genre_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    name VARCHAR 
        NOT NULL,
    tvtropes_url VARCHAR,
    description MEDIUMTEXT,
    PRIMARY KEY(genre_id),
    UNIQUE(name)
);

- Tropes(
    trope_id INT 
        NOT NULL 
        AUTO_INCREMENT,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    name VARCHAR 
        NOT NULL,
    tvtropes_url VARCHAR,
    description MEDIUMTEXT,
    PRIMARY KEY(trope_id),
    UNIQUE(name)
);

- Statuses(
    status_id INT
        NOT NULL
        AUTO_INCREMENT,
    name VARCHAR 
        NOT NULL,
    PRIMARY KEY (status_id),
    UNIQUE(name)
);

- Schedules(
    schedule_id INT
        NOT NULL
        AUTO_INCREMENT,
    name VARCHAR,
    period_days DECIMAL(5,2),
    PRIMARY KEY (schedule_id),
    UNIQUE(name),
    UNIQUE(period_days)
);

-- connection dbs below here

- Hosts_Comics_Connections(
    host_id INT 
        NOT NULL,
    webcomic_id INT 
        NOT NULL,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (host_id) 
        REFERENCES Hosting_Sites(host_id),
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(host_id,webcomic_id)
);

- Has_Reads(
    user_id INT 
        NOT NULL,
    webcomic_id INT 
        NOT NULL,
    FOREIGN KEY (user_id) 
        REFERENCES Users(user_id),
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(user_id,webcomic_id)
);

- To_Reads(
    user_id INT 
        NOT NULL,
    webcomic_id INT 
        NOT NULL,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) 
        REFERENCES Users(user_id),
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(user_id,webcomic_id)
);

- Genre-User_Connection(
    user_id INT 
        NOT NULL,
    genre_id INT 
        NOT NULL,
    FOREIGN KEY (user_id) 
        REFERENCES Users(user_id),
    FOREIGN KEY (genre_id) 
        REFERENCES Genres(genre_id),
    UNIQUE(user_id,genre_id)
);

- Trope-User_Connection(
    user_id INT 
        NOT NULL,
    trope_id INT 
        NOT NULL,
    FOREIGN KEY (user_id) 
        REFERENCES Users(user_id),
    FOREIGN KEY (trope_id) 
        REFERENCES Tropes(trope_id),
    UNIQUE(user_id,trope_id)
);


- Creators_Webcomics_Connections(
    creator_id INT 
        NOT NULL,
    webcomic_id INT 
        NOT NULL,
    FOREIGN KEY (creator_id) 
        REFERENCES Creators(creator_id),
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(creator_id,webcomic_id)
);

- Tropes_Reviews_Connections(
    trope_id INT 
        NOT NULL,
    review_id INT 
        NOT NULL,
    FOREIGN KEY (trope_id) 
        REFERENCES Tropes(trope_id),
    FOREIGN KEY (review_id) 
        REFERENCES Reviews(review_id),
    UNIQUE(trope_id,review_id)
);

- Genres_Reviews_Connections(
    genre_id INT 
        NOT NULL,
    review_id INT 
        NOT NULL,
    FOREIGN KEY (genre_id) 
        REFERENCES Genres(genre_id),
    FOREIGN KEY (review_id) 
        REFERENCES Reviews(review_id),
    UNIQUE(genre_id,review_id)
);

- Users_Reviews_Likes(
    user_id INT 
        NOT NULL,
    review_id INT 
        NOT NULL,
    FOREIGN KEY (user_id) 
        REFERENCES user(user_id),
    FOREIGN KEY (review_id) 
        REFERENCES Reviews(review_id),
    UNIQUE(user_id,review_id)
);

- Webcomic_Genres_Connections(
    webcomic_id INT 
        NOT NULL,
    genre_id INT 
        NOT NULL,
    number_of_hits INT 
        NOT NULL 
        DEFAULT 1,
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    FOREIGN KEY (trope_id) 
        REFERENCES Genres(genre_id),
    UNIQUE(webcomic_id,genre_id)
);

- Webcomic_Tropes_Connections(
    webcomic_id INT 
        NOT NULL,
    trope_id INT 
        NOT NULL,
    insertion_date TIMESTAMP 
        NOT NULL 
        DEFAULT NOW() 
        ON UPDATE CURRENT_TIMESTAMP,
    number_of_hits INT 
        NOT NULL
        DEFAULT 1,
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    FOREIGN KEY (trope_id) 
        REFERENCES Tropes(trope_id),
    UNIQUE(webcomic_id,trope_id)
);

- Webcomic_Hosts_Connections(
    webcomic_id INT 
        NOT NULL,
    host_site_id INT 
        NOT NULL,
    FOREIGN KEY (webcomic_id) 
        REFERENCES Webcomics(webcomic_id),
    FOREIGN KEY (host_site_id) 
        REFERENCES Host_Sites(host_id),
    UNIQUE(webcomic_id,host_site_id)
);

- Webcomic_Webcomic_Connections(
    webcomic_id1 INT 
        NOT NULL,
    webcomic_id2 INT 
        NOT NULL,
    FOREIGN KEY (webcomic_id1) 
        REFERENCES Webcomics(webcomic_id),
    FOREIGN KEY (webcomic_id2) 
        REFERENCES Webcomics(webcomic_id),
    UNIQUE(webcomic_id1,webcomic_id2)
);

