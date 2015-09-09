CMAKE_MINIMUM_REQUIRED(VERSION 3.2)
SET(CMAKE_CXX_COMPILER "clang++") 
SET(PROJECT_NAME PGBOUNCER)
PROJECT(${PROJECT_NAME}) 
SET(PG_SRC 
    src/admin.c 
    src/client.c 
    src/dnslookup.c 
    src/hba.c 
    src/janitor.c 
    src/loader.c 
    src/main.c 
    src/objects.c 
    src/pktbuf.c 
    src/pooler.c 
    src/proto.c 
    src/sbuf.c 
    src/server.c 
    src/stats.c 
    src/system.c 
    src/takeover.c 
    src/util.c 
    src/varcache.c
)
SET(PG_LIB_SRC
    lib/usual/crypto/chacha.c
    lib/usual/crypto/csrandom.c
    lib/usual/crypto/digest.c
    lib/usual/crypto/entropy.c
    lib/usual/crypto/hmac.c
    lib/usual/crypto/keccak.c
    lib/usual/crypto/keccak_prng.c
    lib/usual/crypto/md5.c
    lib/usual/crypto/sha1.c
    lib/usual/crypto/sha256.c
    lib/usual/crypto/sha3.c
    lib/usual/crypto/sha512.c
    lib/usual/hashing/crc32.c
    lib/usual/hashing/lookup3.c
    lib/usual/hashing/memhash.c
    lib/usual/hashing/siphash.c
    lib/usual/hashing/spooky.c
    lib/usual/hashing/xxhash.c
    lib/usual/tls/tls.c
    lib/usual/tls/tls_cert.c
    lib/usual/tls/tls_client.c
    lib/usual/tls/tls_compat.c
    lib/usual/tls/tls_config.c
    lib/usual/tls/tls_server.c
    lib/usual/tls/tls_util.c
    lib/usual/tls/tls_verify.c
    lib/usual/aatree.c
    lib/usual/base.c
    lib/usual/cbtree.c
    lib/usual/cfparser.c
    lib/usual/cxalloc.c
    lib/usual/cxextra.c
    lib/usual/daemon.c
    lib/usual/dlfcn.c
    lib/usual/err.c
    lib/usual/event.c
    lib/usual/fileutil.c
    lib/usual/fnmatch.c
    lib/usual/getopt.c
    lib/usual/heap.c
    lib/usual/json.c
    lib/usual/list.c
    lib/usual/logging.c
    lib/usual/mbuf.c
    lib/usual/mdict.c
    lib/usual/mempool.c
    lib/usual/netdb.c
    lib/usual/pgsocket.c
    lib/usual/pgutil.c
    lib/usual/psrandom.c
    lib/usual/pthread.c
    lib/usual/regex.c
    lib/usual/safeio.c
    lib/usual/signal.c
    lib/usual/slab.c
    lib/usual/socket.c
    lib/usual/socket_ntop.c 
    lib/usual/socket_pton.c
    lib/usual/string.c
    lib/usual/strpool.c
    lib/usual/talloc.c
    lib/usual/time.c
    lib/usual/utf8.c
    lib/usual/wchar.c
)
SET(SRC_LIST ${PG_LIB_SRC} ${PG_SRC}) 
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include ${CMAKE_SOURCE_DIR}/lib) 
SET(CMAKE_CXX_FLAGS "
    -std=c++11 -stdlib=libc++ -Werror -Weverything 
    -Wno-deprecated-declarations 
    -Wno-disabled-macro-expansion 
    -Wno-float-equal 
    -Wno-c++98-compat 
    -Wno-c++98-compat-pedantic 
    -Wno-global-constructors 
    -Wno-exit-time-destructors 
    -Wno-missing-prototypes 
    -Wno-padded 
    -Wno-old-style-cast")
SET(CMAKE_EXE_LINKER_FLAGS "-lc++ -lc++abi -lpq -levent -lcrypto -lssl") 
SET(CMAKE_BUILD_TYPE Debug) 
#SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
ADD_EXECUTABLE(main ${SRC_LIST})
INSTALL(FILES ${CMAKE_SOURCE_DIR}/etc/pgbouncer.ini DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(FILES ${CMAKE_SOURCE_DIR}/etc/userlist.txt DESTINATION ${CMAKE_INSTALL_PREFIX})
INSTALL(PROGRAMS ${CMAKE_BINARY_DIR}/main DESTINATION ${CMAKE_INSTALL_PREFIX} RENAME pgbouncer-x2)
