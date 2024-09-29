Design Reddit: System Design Mock Interview

1. Introduction
   design reddit homepage

2. Interview

daily users : 50 million users
image and text in post
top posts 24 hours
consider logged-in users

title - 50 char _ 2 byte => 100 byte
content - 300 char _ 2 byte => 600 byte
image => 100 to 200 kb per image

The average amount of data in each post is about 50.4KB
It's situation where we have to call 6.2 billion posts a day.

It there a way to reduce this amount of data?
=> Instead of the image, we think it would be better to send a small thumbnail Image
first and import a full-sized image when the user clicks on the image.

Each service will need a web server, an application server, a ranking service, a feed service, a user service, a post service, and an object store to store images

You can't put posts in a single database, you can use NOSQL, which is good for horizontal expansion, and if you want to store posts consistently in a horizontally expanded database, your PostID can be put as an integer basis, but this can't be put exactly, so you can use the concept of consistent hashing to save posts without having to redistribute them even if you increase the number of shards.

If you're in an on-premise environment to import images, you'll need a system to import them, and if you're using aws or gcp, you can use s3 or cloud storage.

By saving the top 25 posts in the cache, you can quickly pass the database to users without querying it every time.

And the crawler is in charge of creating feeds and updating the cache, so you can crawl the top posts every few hours to update the cache.
