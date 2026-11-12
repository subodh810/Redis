Q. "How can we refill/reload data in Redis after TTL expires?
>>Option 1: Cache-Aside Pattern (Most Common)
              
              Application
                    |
                    v
              Check Redis
                    |
                    |-- Found --> Return Data
                    |
                    |-- Not Found
                              |
                              v
                        Query Database
                              |
                              v
                        Save to Redis
                              |
                              v
                          Return Data

>>Option 2: Refresh Cache Before Expiry

>>When a Redis key expires due to TTL, the most common approach is the Cache-Aside pattern. The application first checks Redis. If the data is missing because the TTL has expired, it fetches the data from the database, returns it to the user, and stores it back in Redis with a new TTL. In Spring Boot, this can be implemented manually using RedisTemplate or automatically using @Cacheable. For proactive refreshing, scheduled jobs or Redis keyspace notifications can be used.
