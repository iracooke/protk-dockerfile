FROM debian:wheezy

MAINTAINER Simon Belluzzo <simon@belluzzo.id.au>

ENV PROTK_INSTALL_DIR /opt/protk_tools
ENV RUBY_DIR /opt/ruby

RUN apt-get update \
      && apt-get -y install --no-install-recommends \
	autoconf=2.69-1 \
	automake=1:1.11.6-1 \
        build-essential=11.5 \
        bzip2=1.0.6-4 \
	curl=7.26.0-1+wheezy13 \
	libbz2-dev=1.0.6-4 \
	libc6-dev=2.13-38+deb7u8 \
	libgd2-noxpm-dev \
	liblocal-lib-perl=1.008004-2 \
	libxml-parser-perl=2.41-1+b1 \
	libxml2 \
	libxml2-dev \
	libyaml-0-2=0.1.4-2+deb7u5 \
	lsb-release=4.1+Debian8+deb7u1 \
	openjdk-7-jre-headless \
	pkg-config=0.26-1 \
	time=1.7-24 \
	unzip=6.0-8+deb7u2 \
	wget=1.13.4-3+deb7u2 \
      && curl -SL https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz | tar -zx \
      && ruby-install-0.5.0/bin/ruby-install --cleanup --install-dir $RUBY_DIR ruby 2.1 -- --disable-install-rdoc \
      && rm -rf ruby-install-0.5.0 \
      && $RUBY_DIR/bin/gem install --no-document protk:1.4.3 \
      && $RUBY_DIR/bin/protk_setup.rb tpp \
      && $RUBY_DIR/bin/protk_setup.rb omssa \
      && $RUBY_DIR/bin/protk_setup.rb blast \
      && $RUBY_DIR/bin/protk_setup.rb msgfplus \
      && $RUBY_DIR/bin/protk_setup.rb pwiz \
      && $RUBY_DIR/bin/protk_setup.rb clean \
      && chmod -R a+w $PROTK_INSTALL_DIR/Logs \
      && apt-get -y purge --auto-remove \
	autoconf \
	automake \
	autotools-dev \
	binutils \
	build-essential \
	dpkg-dev \
	gcc \
	g++ \
	libbz2-dev \
	libc6-dev \
	libffi-dev \
	libreadline-dev \
	libtinfo-dev \
	libxml2-dev \
	libyaml-dev \
	linux-libc-dev \
	make \
	pkg-config

ENV PATH $RUBY_DIR/bin:$PROTK_INSTALL_DIR/tools/pwiz:$PATH
