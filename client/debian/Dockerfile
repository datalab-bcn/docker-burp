FROM debian:buster AS builder

# We install dev dependencies
RUN apt-get update && apt-get install -y make pkg-config check g++ acl-dev xattr \
		librsync-dev libz-dev libssl-dev uthash-dev dh-autoreconf libncurses-dev

ADD https://netcologne.dl.sourceforge.net/project/burp/burp-2.2.18/burp-2.2.18.tar.bz2 /tmp/burp-2.2.18.tar.bz2

WORKDIR /tmp/
RUN tar xvf burp-2.2.18.tar.bz2

WORKDIR /tmp/burp-2.2.18

# We compile burp
# We remove dev dependencies to decrease image size (also cache and tmp)
RUN autoreconf -vif && \
  ./configure --prefix=/usr --sysconfdir=/etc/burp --localstatedir=/var && \
  make && make install


FROM debian:buster
COPY --from=builder /var/spool/burp /var/spool/burp
COPY --from=builder /usr/sbin/burp_ca /usr/sbin/burp_ca
COPY --from=builder /usr/sbin/burp /usr/sbin/burp
COPY --from=builder /usr/share/burp /usr/share/burp
WORKDIR /
RUN apt-get update && apt-get install -y librsync1 zlib1g libssl1.1 libncurses6 xattr \
    acl

CMD [ "burp", "-a","t" ]
