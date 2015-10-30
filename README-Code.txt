解读工作已经有人做了
http://blog.csdn.net/column/details/flashcache.html

初始化：
module_init(flashcache_init);
module_exit(flashcache_exit);

入口：flashcache_map
用户态代码会经常去先看main函数，内核看module_init，同样看IO流时候也要找到入口。
flashcache作为一个dm_target，入口就是struct target_type 的map函数，对应的是flashcache_map函数.

flashcache是Target Driver。
[root@sandstone0002 ~]# dmsetup targets
multipath        v1.5.0
flashcache       v1.0.4
mirror           v1.12.0
striped          v1.5.6
linear           v1.1.0
error            v1.0.1

[root@sandstone0002 ~]# dmsetup status
vg_journal-lv_journal_0_0: 0 5586944 linear
VolGroup-lv_home: 0 421052416 linear
vg_journal-lv_journal_2_0: 0 5586944 linear
cachedev-2: 0 585937500 flashcache stats:
        reads(37847), writes(35892491)
        read hits(5152), read hit percent(13)
        write hits(313215) write hit percent(0)
        replacement(485), write replacement(16099)
        write invalidates(60426), read invalidates(12)
        pending enqueues(0), pending inval(0)
        no room(0)
        disk reads(32695), disk writes(32612135) ssd reads(5152) ssd writes(3602889)
        uncached reads(23415), uncached writes(32298928), uncached IO requeue(0)
        disk read errors(0), disk write errors(0) ssd read errors(0) ssd write errors(0)
        uncached sequential reads(2244), uncached sequential writes(31908952)
        pid_adds(0), pid_dels(0), pid_drops(0) pid_expiry(0)
        lru hot blocks(4881920), lru warm blocks(4881920)
        lru promotions(0), lru demotions(0)