- Drivers
- Riders

Each driver or rider stays in a shell. A shell is a collection of Pair(lat,long).
Shell is small in size.
# Drivers
- Driver send shell location through websocket in every 4s. 
- shell location saved in a database shard. shard are place in a ring.

# Riders
- Riders send shell location through websocket only when they want ride.

## Demand & Supply Service
- Let say we have shell from 1,12 and have 4 shards on ring.
- [1,2,3] is managed by s1. Similary [4,5,6] - s2. [7,8,9] - s3. [10,11,12] - s4
- Assume Rider is in 5th Shell and sends a demand or booking request. So request will come to s2.
- s2 will figure out what are the shells surrounding the shell 5. Let say 7, 9, 2
- so s2 will send the request to 5,7,9,2 to find the cabs. Sort the cabs which has less ETA for pickup.
- After sorting the cabs s2 sends request to each cab one by one and if match occurs then user gets notified.

