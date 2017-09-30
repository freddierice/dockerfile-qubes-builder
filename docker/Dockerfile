FROM fedora
MAINTAINER Freddie Rice

# initial upgrade
RUN dnf update -y

# dumb-init
RUN dnf install -y wget
RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 \
	&& chmod +x /usr/local/bin/dumb-init

# qubes requirements
RUN dnf install -y git createrepo rpm-build rpm-sign make python2-sh rpmdevtools rpm-sign dialog perl-open gpg hostname which sudo PyYAML libyaml e2fsprogs policycoreutils

# add non-root user
RUN useradd -G wheel -p "" user

# make working directory
RUN mkdir -p /build \
	&& chown user:user /build \
	&& mkdir -p /shared \
	&& chown user:user /shared

# set the locale
RUN echo "export LANG=en_US.utf-8" > /opt/export_LANG.sh

# make loop devices
RUN /usr/bin/mknod /dev/loop0 -m0660 b 7 0 \
	&& /usr/bin/mknod /dev/loop1 -m0660 b 7 1 \
	&& /usr/bin/mknod /dev/loop2 -m0660 b 7 2 \
	&& /usr/bin/mknod /dev/loop3 -m0660 b 7 3 \
	&& /usr/bin/mknod /dev/loop4 -m0660 b 7 4

USER user
ENV BASH_ENV=/opt/export_LANG.sh \
	ENV=/opt/export_LANG.sh \
	PROMPT_COMMAND="source /opt/export_LANG.sh"
ENV LANG=en_US.utf-8

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]
CMD ["bash", "-c", "if [ ! -d qubes-builder ]; then git clone https://github.com/QubesOS/qubes-builder.git ; fi && bash"]
