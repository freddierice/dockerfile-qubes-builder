FROM fedora
MAINTAINER Freddie Rice

# initial upgrade
RUN dnf update -y

# dumb-init
RUN dnf install -y wget
RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 \
	&& chmod +x /usr/local/bin/dumb-init

# qubes requirements
RUN dnf install -y git createrepo rpm-build rpm-sign make python2-sh rpmdevtools rpm-sign dialog perl-open gpg hostname which sudo PyYAML libyaml

# add non-root user
RUN useradd -G wheel -p "" user

# make working directory
RUN mkdir -p /build \
	&& chown user:user /build \
	&& mkdir -p /shared \
	&& chown user:user /shared

USER user
ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]
CMD ["bash", "-c", "if [ ! -d qubes-builder ]; then git clone https://github.com/QubesOS/qubes-builder.git ; fi && bash"]
