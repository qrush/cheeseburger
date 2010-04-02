!SLIDE burger

# use cases

!SLIDE full-page center

![](boggle.jpg)

# boggle

!SLIDE bullets

# boggle

* game id, score = counter
* guesses, dictionary = set
* words for a game = list

!SLIDE ruby

    @@@ ruby
    def load
      $redis.del "dict"
      dict = File.read("/usr/share/dict/words")
      dict.split.each do |word|
        if word =~ /^[a-z]{3,8}$/
          $redis.sadd "dict", word.upcase
        end
      end
    end

    def word?(word)
      $redis.sismember("dict", word)
    end

!SLIDE full-page center

![](queue.jpg)

# queues

!SLIDE bullets incremental

# queues

* atomic pops = multiple workers
* resque
* `BLPOP key`
* `RPOPLPUSH srckey dstkey`
* pub/sub protocol

!SLIDE full-page center

![](hockey.jpg)
# analytics

!SLIDE bullets incremental

# analytics: gem downloads

* ideal with speed and `INCR`/`INCRBY`
* historical data vs current data
* total counts = counters
* daily per version = zset (`ZINCRBY`)
* historical data = hash (`HINCRBY`)

!SLIDE ruby

# on a gem download

    @@@ ruby
    $redis.incr "downloads"
    $redis.incr "downloads:rubygem:rails"

    key = "downloads:version:rails-2.3.5"
    $redis.incr key
    $redis.zincrby "downloads:today", 1, key

!SLIDE ruby

# daily rollover

    @@@ ruby
    date = "2010-04-02"
    $redis.rename "dls:today", "dls:yesterday"

    dls = Hash[*$redis.zrange("dls:yesterday",
                              0, -1,
                              "withscores")]

    dls.each do |key, score|
      ver = versions[key]
      $redis.hincrby ver, date, score
      $redis.hincrby ver.rubygem, date, score
    end
