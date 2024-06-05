FROM cloudsuite/base-os:ubuntu

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r memcache && useradd -r -g memcache memcache

ENV DEBIAN_FRONTEND noninteractive

RUN buildDeps='curl gcc libc6-dev make git ca-certificates' \	
	&& set -x \
	&& apt-get update && apt-get install -y $buildDeps libevent-dev vim --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& git clone https://github.com/shinsakukataoka/memcached-loadtester.git /usr/src/memcached \
	&& cd /usr/src/memcached/memcached_client \
	&& make -j $(nproc) \
	&& chown -R memcache:memcache /usr/src/memcached \
	&& apt-get purge -y --auto-remove $buildDeps

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

USER memcache
CMD ["/bin/bash"]
