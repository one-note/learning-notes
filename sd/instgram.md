
# Instagram
media service: uploads images to cloud
feeds-service: provides the feeds
account-service: manages user profile, followers and following
post-service: manages the post
like-service: manages the likes on post
comment-service: manages the comments on post

- when user writes the post it goes to post service
  {
    post:{
      text: "message"
      media: binary
    }
  }
- post services writes the data to database
  postId | text | createdBy | createdAt
- post service publishes the message into the queue of each of the follower (when post owner is not celebrity)
- whenever followers come online they get the posts from the queue
- when post owner is a celebrity, whenever the followers come online they first query the database/cache to check if any posts available from
  from the celebrity. this polling happens periodically.
- post service uses media-service to upload the media file into a cloud storage.
- feeds service reads media files from cloud storage using the media-url
- feed json can look like this
  {
   postId:
   createdBy:
   createdAt:
   post:{
    text: message
    mediaUrl: url
    likeCount: 10
    commentCount: 10
   }
  }
- like service manages likes for a given post or comment
  {
    postId:
    likedBy:
    likedAt:
  } 
- comment service manages comments for a given post
  {
    postId:
    comment:{
     text: ""
    }
    commentBy:
    commentAt:
  }  
- account-service manages the acountOwner and followerAccount Mapping. Also it manages profile service of users.
  accountId | followingId
    1          10
    1          20
    20          2
    2           1
    3           1
    
    1 is following 10, 20
    1 has followers 2,3
    so when any message is posted by 1 it should be visible by 2,3.
    
