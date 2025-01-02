# Video app design case study

## Functional requirements (MVP)

- stream videos (MVP)
- browse videos (MVP)
- user account
- publish video : publisher _user (MVP)
- watch live video: publisher_user (MVP)

## Design goals

Perhaps having various microservices to run this system might be a good idea.This is because streaming could require a lot of resources.

Service 1: A microservice to manage users

Service 2: A microservice could be used to browse videos.

- Highly available
- Eventually consistent

Service 3: Another service could be used for streaming.

- Low buffering
- Highly available
- eventually consistent

## Estiamations

### Assumptions

- Population of india is 1 Billion
- Percentage of people with an account could be 50% of the population => 500 million
- The amount of movies and videos could be perhaps 10,000

### Calculate storage

- A user could be worth 200 MB
  - with 200 MB *500 million people
       = 200 MB * 5* 100 million
        = 100 TB
    this implies sharding as computers would be 4 TB.. sharding based on user_id

- Video meta data could be 200 MB
    with 10,000 videos , we could be seeing 2 000 000 MB = 2 TB
    if we use a server of 4 TB, no sharding is needed.

- A video could be 5 GB considering meta data for each segment  or chunk
  - This implies that we're looking at 5 GB * 10 000 videos
  - In the end we're looking at 50 TB worth of videos.
  - sharding based on video_id

### read-heavy /write heavy

- read heavy - lots of viewers
- not write heavy as not everyone will have access to publish videos

## API

Service 2:

getVideo(video_id)
publishVideo(video_title,video_description)

Service 1:

addUser(email,first_name,last_name)

Service 3:

requestVideoStream(video_id)
requestLiveVideoStream(video_id)
publishLiveVideoStream(video_id,Stream_id, segment_id)

## Implementation approaches

### microservices communication

foresee communication between the service2 and service3
choreography pattern would be good

### implementing service 3

#### for live streaming - by publisher

- There would be a publisher client allowing the publisher(user) to record live.
  - As the recording occurs, there would be services that will be responsible to chop the video into segments and  send requests to publish the segments along with  metadata.

#### for live/non-live streaming - by audience

- There would be an audience client making a request to an app server via a CDN to view the live video.
  - then , *Adaptive bitrate* streaming is done to  provide the best video resolution to send for the stream
  - the client continuously does requests to get the next chunk (applying *preemptive loading*)
