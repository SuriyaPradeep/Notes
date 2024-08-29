#priority-queue 
### Question
Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the `10` most recent tweets in the user's news feed.

Implement the `Twitter` class:

- `Twitter()` Initializes your twitter object.
- `void postTweet(int userId, int tweetId)` Composes a new tweet with ID `tweetId` by the user `userId`. Each call to this function will be made with a unique `tweetId`.
- `List<Integer> getNewsFeed(int userId)` Retrieves the `10` most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be **ordered from most recent to least recent**.
- `void follow(int followerId, int followeeId)` The user with ID `followerId` started following the user with ID `followeeId`.
- `void unfollow(int followerId, int followeeId)` The user with ID `followerId` started unfollowing the user with ID `followeeId`.

**Example 1:**

**Input**
["Twitter", "postTweet", "getNewsFeed", "follow", "postTweet", "getNewsFeed", "unfollow", "getNewsFeed"]
[[], [1, 5], [1], [1, 2], [2, 6], [1], [1, 2], [1]]
**Output**
[null, null, [5], null, null, [6, 5], null, [5]]

**Explanation**
Twitter twitter = new Twitter();
twitter.postTweet(1, 5); // User 1 posts a new tweet (id = 5).
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 1 tweet id -> [5]. return [5]
twitter.follow(1, 2);    // User 1 follows user 2.
twitter.postTweet(2, 6); // User 2 posts a new tweet (id = 6).
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 2 tweet ids -> [6, 5]. Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.unfollow(1, 2);  // User 1 unfollows user 2.
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 1 tweet id -> [5], since user 1 is no longer following user 2.

### Solution
```java
class Twitter {  
    static int timeStamp=0;  
    HashMap<Integer,User> map;  
  
    class Tweet{  
        int id;  
        int time;  
        Tweet next;  
        public Tweet(int id){  
            this.id=id;  
            time=timeStamp++;  
            next=null;  
        }  
    }  
    class User{  
        int id;  
        HashSet<Integer> follows;  
        Tweet tweetHead;  
        public User(int id){  
            this.id=id;  
            follows=new HashSet<>();  
            follow(id);  
            tweetHead=null;  
        }  
        public void follow(int id){  
            follows.add(id);  
        }  
        public void unfollow(int id){  
            follows.remove(id);  
        }  
        public void post(int tweetId){  
            Tweet currTweet=new Tweet(tweetId);  
            currTweet.next=tweetHead;  
            tweetHead=currTweet;  
        }  
    }  
  
    public Twitter() {  
        map=new HashMap<>();  
    }  
  
    public void postTweet(int userId, int tweetId) {  
        if(!map.containsKey(userId)){  
            map.put(userId,new User(userId));  
        }  
        map.get(userId).post(tweetId);  
    }  
  
    public List<Integer> getNewsFeed(int userId) {  
        List<Integer> res=new ArrayList<>();  
        if(!map.containsKey(userId)){  
            return res;  
        }  
        PriorityQueue<Tweet> pq=new PriorityQueue<>((a, b)->Integer.compare(b.time,a.time));  
        HashSet<Integer> users=map.get(userId).follows;  
        for(int user:users){  
            if(map.get(user).tweetHead!=null){  
                pq.add(map.get(user).tweetHead);  
            }  
        }  
        int n=1;  
        while(!pq.isEmpty() && n<=10){  
            Tweet currTweet=pq.poll();  
            res.add(currTweet.id);  
            n++;  
            if(currTweet.next!=null){  
                pq.add(currTweet.next);  
            }  
        }  
        return res;  
    }  
  
    public void follow(int followerId, int followeeId) {  
        if(!map.containsKey(followerId)){  
            map.put(followerId,new User(followerId));  
        }  
        if(!map.containsKey(followeeId)){  
            map.put(followeeId,new User(followeeId));  
        }  
        map.get(followerId).follow(followeeId);  
    }  
  
    public void unfollow(int followerId, int followeeId) {  
        if(!map.containsKey(followerId) || !map.containsKey(followeeId)){  
            return;  
        }  
        map.get(followerId).unfollow(followeeId);  
    }  
}
```

**Explanation**
1. **`Twitter` Class:**
    
    - **`timeStamp`**: A static integer used to assign a unique timestamp to each tweet, ensuring the order of tweets.
    - **`map`**: A `HashMap` that maps each `userId` to a `User` object.
2. **`Tweet` Class:**
    
    - **`id`**: The tweet ID.
    - **`time`**: The timestamp when the tweet was created.
    - **`next`**: A pointer to the next tweet in the user's tweet list.
3. **`User` Class:**
    
    - **`id`**: The user ID.
    - **`follows`**: A `HashSet` of user IDs that this user follows (including themselves).
    - **`tweetHead`**: A pointer to the most recent tweet this user posted.

**Methods:**

1. **`postTweet(int userId, int tweetId)`**:
    
    - Posts a tweet with `tweetId` for the user with `userId`.
    - If the user doesn’t exist in the `map`, they are added.
    - The new tweet is added to the front of the user's tweet linked list.
2. **`getNewsFeed(int userId)`**:
    
    - Retrieves the 10 most recent tweets from the users that `userId` follows.
    - A priority queue (`pq`) is used to manage the tweets based on their timestamps.
    - The tweets are retrieved from the queue in decreasing order of their timestamps.
3. **`follow(int followerId, int followeeId)`**:
    
    - Makes the user with `followerId` follow the user with `followeeId`.
    - If either user does not exist in `map`, they are added.
4. **`unfollow(int followerId, int followeeId)`**:
    
    - Makes the user with `followerId` unfollow the user with `followeeId`.
    - Does nothing if the user tries to unfollow themselves or if either user doesn’t exist.