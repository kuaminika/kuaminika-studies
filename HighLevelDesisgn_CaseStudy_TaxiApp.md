# taxi like app

## Functional requirements (MVP)

- as a user, there is a need to see all the active cab drivers near by to book a ride
- as a user I'd like to see the movements of my chosen driver on a map to confirm progression

## non functional requirements (design goals)

- realtime movement of chosen driver
- highly available
- eventually consistent
- low latency over consistency

## Estimations

### assumptions

    - there's 20 drivers max shown on the map 
    - there's 100 million registered drivers on the system

### storage calculaition

- we will use a quadtree to store locations in our system
  - with geometric progression we know that if we were to locate 100 million drivers in a node in our quad tree, we would need 100 million *(4/3) nodes
  - a node can be 88 bytes as it can consist of:
    - 16 bytes longitude1
    - 16 bytes latitude1
    - 16 bytes longitude2
    - 16 bytes latitude2
    - 4 bytes node_id
    - 4 bytes pointer to parent
    - 4 bytes poinrter to part 1
    - 4 bytes poinrter to part 2
    - 4 bytes poinrter to part 3
    - 4 bytes poinrter to part 4
  - 88 bytes * 100 million (4/3) = 8800MB*4/3*1/20
  - we divide by 20 as well considering that we put 20 cars on leaf nodes
  - all together it gives 586 MB
  - with 100 million possible places as well, we can think of 32 bytes per place. so thats 3.2 billion bytes which is 3.2 GB
  - so, with a server being 4 TB . i dont see a need for sharding

### read-heavy/ write heavy

- read heavy yes because it constantly needs to seek driver locations
- write heavy yes beacuse drivers have to constantly publish their location

## API

updateLocation(driver_id, x,y, quadTree_grid_id);
getDriversNearMe(usrr_id, x,y)

## implementation dscussions

- implementind updateLocation(driver_id, x,y, quadTree_grid_id) is expensive as it can imply splitting the grid or compromising it.
- hence the reason why it is preferred to be eventually consistent.

- we can also consider splitting the grid when we are over the grid threshod by a few a certain amount
- we can also consider splitting the ndoe at an interval of a few hours if needed.

- we can also keep the location in the cache as perhaps its not truly necessary to keep the realtime location.
