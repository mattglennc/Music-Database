# Music-Database

In this MySQL project, we wrote the schema to implement a relational database which holds music, albums, artists, playists, users, and ratings.
We then implemented queries to be made on the database, which can be viewed in assignment4.ipynb, where the database and queries are tested 
using Python.

The schema is as follows:
	create table artist(
	    id int auto_increment primary key,
	    artist_name varchar(50) not null unique);

	create table album(
	    id int auto_increment primary key,
	    album_title varchar(50) not null,
	    artist_id int not null,
	    foreign key (artist_id) references artist(id),
	    unique (id,artist_id));

	create table song(
	    id int auto_increment primary key,
	    song_title varchar(50) not null,
	    artist_id int not null,
	    album_id int,
	    album_release date,
	    single_release date,
	    foreign key (artist_id) references artist(id),
	    foreign key (album_id) references album(id),
	    unique(song_title,artist_id));


	create table song_genre(
	    song_id int not null,
	    genre varchar(20) not null,
	    foreign key (song_id) references song(id));

	create table user(
	    username varchar(40) primary key);

	create table playlist(
	    id int auto_increment primary key,
	    playlist_title varchar(40) not null,
	    user varchar(40) not null,
	    date date not null,
	    time time not null,
	    foreign key (user) references user(username),
	    unique(id,user));

	create table song_playlist(
	    song_id int not null,
	    playlist_id int not null,
	    foreign key (song_id) references song(id),
	    foreign key (playlist_id) references playlist(id),
	    unique(song_id,playlist_id));

	create table rating(
	    user varchar(40) not null,
	    rating_number tinyint not null,
	    type enum('song','album','playlist') not null default 'song',
	    song_id int,
	    album_id int,
	    playlist_id int,
	    date date not null,
	    foreign key (user) references user(username),
	    foreign key (song_id) references song(id),
	    foreign key (album_id) references album(id),
	    foreign key (playlist_id) references playlist(id),
	    unique(user,song_id,album_id,playlist_id));
    
    
