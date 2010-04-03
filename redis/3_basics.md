!SLIDE burger

# basics

!SLIDE bullets incremental

# history

* REmote DIctionary Server
* started in 2009
* @antirez
* vmware
* under very heavy development

!SLIDE bullets incremental

# installing

* `git clone git://github.com/antirez/redis`
* `make`
* `redis-server`
* `redis-cli`
* POSIX only

!SLIDE bullets

# drivers

* ruby
* python
* java
* php
* node.js
* ...

!SLIDE bullets

# memory

* keys, values
* keys must stay in memory
* values can be swapped
* really stable

!SLIDE bullets

# speed

* ANSI C
* 110,000 SETs/second
* 81,000 GETs/second
* pipelining

!SLIDE bullets incremental

# misc

* atomic operations
* background saving
* master/slave replication
* sharding
* virtual memory
