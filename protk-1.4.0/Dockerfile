FROM debian:wheezy

MAINTAINER Simon Belluzzo <simon@belluzzo.id.au>

ENV PROTK_INSTALL_DIR /opt/protk_tools
ENV RUBY_DIR /opt/ruby

RUN apt-get update \
      && apt-get -y install --no-install-recommends \
	autoconf \
	automake \
        build-essential \
        bzip2 \
	curl \
	libbz2-dev \
	libc6-dev \
	libgd2-noxpm-dev \
	liblocal-lib-perl \
	libxml-parser-perl \
	libxml2 \
	libxml2-dev \
	libyaml-0-2 \
	lsb-release \
	openjdk-7-jre-headless \
	pkg-config \
	time \
	unzip \
	wget \
      && curl -SL https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz | tar -zx \
      && ruby-install-0.5.0/bin/ruby-install --cleanup --install-dir $RUBY_DIR ruby 2.1 -- --disable-install-rdoc \
      && rm -rf ruby-install-0.5.0 \
      && $RUBY_DIR/bin/gem install --no-document protk:1.4.0 \
      && $RUBY_DIR/bin/protk_setup.rb tpp \
      && $RUBY_DIR/bin/protk_setup.rb omssa \
      && $RUBY_DIR/bin/protk_setup.rb blast \
      && $RUBY_DIR/bin/protk_setup.rb msgfplus \
      && $RUBY_DIR/bin/protk_setup.rb pwiz \
      && $RUBY_DIR/bin/protk_setup.rb clean \
      && chmod -R a+x $PROTK_INSTALL_DIR/Logs \
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
