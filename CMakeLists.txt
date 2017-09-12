cmake_minimum_required(VERSION 3.7)

project(redis VERSION 3.2)

get_filename_component(REDIS_ROOT "${CMAKE_CURRENT_SOURCE_DIR}" ABSOLUTE)

add_executable(redis
        src/adlist.c
        src/adlist.h
        src/ae.c
        src/ae.h
        src/anet.c
        src/anet.h
        src/aof.c
        src/asciilogo.h
        src/bio.c
        src/bio.h
        src/bitops.c
        src/blocked.c
        src/cluster.c
        src/cluster.h
        src/config.c
        src/config.h
        src/crc16.c
        src/crc64.c
        src/crc64.h
        src/db.c
        src/debug.c
        src/dict.c
        src/dict.h
        src/endianconv.c
        src/endianconv.h
        src/fmacros.h
        src/geo.c
        src/geo.h
        src/help.h
        src/hyperloglog.c
        src/intset.c
        src/intset.h
        src/latency.c
        src/latency.h
        src/lzf.h
        src/lzfP.h
        src/lzf_c.c
        src/lzf_d.c
        src/memtest.c
        src/multi.c
        src/networking.c
        src/notify.c
        src/object.c
        src/pqsort.c
        src/pqsort.h
        src/pubsub.c
        src/quicklist.c
        src/quicklist.h
        src/rand.c
        src/rand.h
        src/rdb.c
        src/rdb.h
        src/redis-check-rdb.c
        src/redisassert.h
        src/release.c
        src/release.h
        src/replication.c
        src/rio.c
        src/rio.h
        src/scripting.c
        src/sds.c
        src/sds.h
        src/sdsalloc.h
        src/sentinel.c
        src/server.c
        src/server.h
        src/setproctitle.c
        src/sha1.c
        src/sha1.h
        src/slowlog.c
        src/slowlog.h
        src/solarisfixes.h
        src/sort.c
        src/sparkline.c
        src/sparkline.h
        src/syncio.c
        src/t_hash.c
        src/t_list.c
        src/t_set.c
        src/t_string.c
        src/t_zset.c
        src/testhelp.h
        src/util.c
        src/util.h
        src/version.h
        src/ziplist.c
        src/ziplist.h
        src/zipmap.c
        src/zipmap.h
        src/zmalloc.c
        src/zmalloc.h
        )

set_property(TARGET redis PROPERTY C_STANDARD 99)



target_include_directories(redis
        PRIVATE ${REDIS_ROOT}/deps/hiredis
        PRIVATE ${REDIS_ROOT}/deps/linenoise
        PRIVATE ${REDIS_ROOT}/deps/lua/src
        PRIVATE ${REDIS_ROOT}/deps/geohash-int
        )
add_library(luaa STATIC IMPORTED)
set_property(TARGET luaa APPEND PROPERTY IMPORTED_CONFIGURATIONS NOCONFIG)
set_target_properties(luaa PROPERTIES IMPORTED_LOCATION_NOCONFIG "${REDIS_ROOT}/deps/lua/src/liblua.a")

target_link_libraries(redis
        PRIVATE m
        PRIVATE luaa
        PRIVATE pthread
        PRIVATE dl
        PRIVATE ${REDIS_ROOT}/deps/linenoise/linenoise.o
        PRIVATE ${REDIS_ROOT}/deps/hiredis/libhiredis.a
        PRIVATE ${REDIS_ROOT}/deps/geohash-int/geohash.o
        PRIVATE ${REDIS_ROOT}/deps/geohash-int/geohash_helper.o
        )

