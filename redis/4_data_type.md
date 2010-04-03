!SLIDE burger

# data types

!SLIDE bullets

# keys

* like memcached
* simple data
* expiration
* renaming
* multiple get/set

!SLIDE redis code

    > set fries done
    OK
    > get fries
    done
    > del fries
    1

    > set fries done
    OK
    > expire 60
    1
    > get fries
    nil

!SLIDE bullets

# counters

* incr
* incrby
* decr
* decrby
* completely atomic

!SLIDE code

    > incr burgers
    1
    > incrby burgers 42
    43
    > decr burgers
    42

!SLIDE bullets

# lists

* push/pop
* length
* random access
* ranges
* blocking pop

!SLIDE code

    > rpush order burger
    1
    > rpush order hotdog
    2
    > rpush order fries
    3
    > lrange order 0 -1
    1. burger
    2. hotdog
    3. fries
    > lpop order
    burger
    > rpop order
    fries
    > lindex order 0
    hotdog

!SLIDE bullets

# sets

* unique elements
* basic functionality from lists
* intersect
* union
* difference

!SLIDE code

    > sadd meat bacon
    1
    > sadd meat turkey
    1
    > sadd toppings bacon
    1
    > sadd toppings bacon
    0
    > sinter meat toppings
    1. bacon
    > sdiff meat toppings
    1. turkey

!SLIDE bullets

# sorted sets (zset)

* {key => float}
* atomic increments
* ranges by score or rank
* union/intersect

!SLIDE code

    > zadd menu 4.99 burger
    1
    > zadd menu 2.99 shake
    1
    > zadd menu 1.99 fries
    1
    > zrank menu fries
    0
    > zscore menu fries
    1.99
    > zrange menu 0 -1
    1. fries
    2. shake
    3. burger
    > zrangebyscore menu 2 5
    1. shake
    2. burger
    > zremrangebyscore menu 2 5
    2

!SLIDE bullets

# hashes

* {key => value}
* atomic increments like zset
* set, get, del, exists, len
* get all keys, values, or both

!SLIDE code

    > hset orders nick burger
    1
    > hset orders john fries
    1
    > hget orders nick
    burger
    > hvals orders
    1. burger
    2. fries
    > hgetall orders
    1. nick
    2. burger
    3. john
    4. fries

!SLIDE bullets

# misc

* type
* sort
* monitor
* multi/exec
* flushdb/all
* randomkey
