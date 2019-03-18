cmake_minimum_required(VERSION 3.13)

project(spiped)

find_package(Threads)
find_package(OpenSSL)

add_executable(
        spiped
        spiped/dispatch.c
        spiped/main.c

        proto/proto_conn.c
        proto/proto_crypt.c
        proto/proto_handshake.c
        proto/proto_pipe.c
        libcperciva/alg/sha256.c
        libcperciva/alg/sha256_shani.c
        libcperciva/datastruct/elasticarray.c
        libcperciva/datastruct/ptrheap.c
        libcperciva/datastruct/timerqueue.c
        lib/dnsthread/dnsthread.c
        lib/util/graceful_shutdown.c
        libcperciva/util/asprintf.c
        libcperciva/util/daemonize.c
        libcperciva/util/entropy.c
        libcperciva/util/getopt.c
        libcperciva/util/insecure_memzero.c
        libcperciva/util/monoclock.c
        libcperciva/util/noeintr.c
        libcperciva/util/setuidgid.c
        libcperciva/util/sock.c
        libcperciva/util/sock_util.c
        libcperciva/util/warnp.c
        libcperciva/cpusupport/cpusupport_x86_aesni.c
        libcperciva/cpusupport/cpusupport_x86_rdrand.c
        libcperciva/cpusupport/cpusupport_x86_shani.c
        libcperciva/cpusupport/cpusupport_x86_ssse3.c
        libcperciva/events/events_immediate.c
        libcperciva/events/events_network.c
        libcperciva/events/events_network_selectstats.c
        libcperciva/events/events_timer.c
        libcperciva/events/events.c
        libcperciva/network/network_accept.c
        libcperciva/network/network_connect.c
        libcperciva/network/network_read.c
        libcperciva/network/network_write.c
        libcperciva/crypto/crypto_aes.c
        libcperciva/crypto/crypto_aes_aesni.c
        libcperciva/crypto/crypto_aesctr.c
        libcperciva/crypto/crypto_dh.c
        libcperciva/crypto/crypto_dh_group14.c
        libcperciva/crypto/crypto_entropy.c
        libcperciva/crypto/crypto_entropy_rdrand.c
        libcperciva/crypto/crypto_verify_bytes.c
)

add_executable(
        spipe
        spipe/pushbits.c
        spipe/main.c

# <Makefile cut -d' ' -f1-2 | fgrep '.o: ../' | cut -d' ' -f 2- | cut -d/ -f 2-
        proto/proto_conn.c
        proto/proto_crypt.c
        proto/proto_handshake.c
        proto/proto_pipe.c
        libcperciva/alg/sha256.c
        libcperciva/alg/sha256_shani.c
        libcperciva/datastruct/elasticarray.c
        libcperciva/datastruct/ptrheap.c
        libcperciva/datastruct/timerqueue.c
        libcperciva/util/asprintf.c
        libcperciva/util/entropy.c
        libcperciva/util/getopt.c
        libcperciva/util/insecure_memzero.c
        libcperciva/util/monoclock.c
        libcperciva/util/noeintr.c
        libcperciva/util/sock.c
        libcperciva/util/warnp.c
        libcperciva/cpusupport/cpusupport_x86_aesni.c
        libcperciva/cpusupport/cpusupport_x86_rdrand.c
        libcperciva/cpusupport/cpusupport_x86_shani.c
        libcperciva/cpusupport/cpusupport_x86_ssse3.c
        libcperciva/events/events_immediate.c
        libcperciva/events/events_network.c
        libcperciva/events/events_network_selectstats.c
        libcperciva/events/events_timer.c
        libcperciva/events/events.c
        libcperciva/network/network_connect.c
        libcperciva/network/network_read.c
        libcperciva/network/network_write.c
        libcperciva/crypto/crypto_aes.c
        libcperciva/crypto/crypto_aes_aesni.c
        libcperciva/crypto/crypto_aesctr.c
        libcperciva/crypto/crypto_dh.c
        libcperciva/crypto/crypto_dh_group14.c
        libcperciva/crypto/crypto_entropy.c
        libcperciva/crypto/crypto_entropy_rdrand.c
        libcperciva/crypto/crypto_verify_bytes.c
)

include_directories(
        lib/dnsthread
        lib/util
        libcperciva/alg
        libcperciva/crypto
        libcperciva/cpusupport
        libcperciva/datastruct
        libcperciva/events
        libcperciva/network
        libcperciva/util
        proto
)

target_link_libraries(
        spipe
        ${CMAKE_THREAD_LIBS_INIT}
        ${OPENSSL_CRYPTO_LIBRARY}
)

target_link_libraries(
        spiped
        ${CMAKE_THREAD_LIBS_INIT}
        ${OPENSSL_CRYPTO_LIBRARY}
)

set_property(TARGET spipe PROPERTY C_STANDARD 99)
set_property(TARGET spiped PROPERTY C_STANDARD 99)
