
RPM_BUILD_ROOT := $(HOME)/rpmbuild
ver ?= 3.0

other_source_v3.0 := \
  ftdetect-proto.vim \
  protobuf-init.el \
  protobuf-2.5.0-emacs-24.4.patch \
  protobuf-2.5.0-fedora-gtest.patch \
  protobuf-3.0.2-easymock.patch

other_source_v3.2 := \
  ftdetect-proto.vim \
  protobuf-init.el

dep_pkgs_build_v3.0 := automake
#dep_pkgs_build_v3.0 += emacs emacs-el
dep_pkgs_build_v3.0 += gmock-devel gtest-devel
dep_pkgs_build_v3.0 += python python-devel python-setuptools python-google-apputils
#dep_pkgs_build_v3.0 += maven maven-local maven-plugin-bundle maven-antrun-plugin easymock2

dep_pkgs_build_v3.2 := autoconf automake
dep_pkgs_build_v3.2 += emacs emacs-el
dep_pkgs_build_v3.2 += gcc-c++ libtool pkgconfig zlib-devel
dep_pkgs_build_v3.2 += python python-devel python-setuptools python-google-apputils python-six
dep_pkgs_build_v3.2 += maven maven-local maven-plugin-bundle maven-antrun-plugin easymock2

# gtest: patch failed to patch v3.0.2, disable it.
# easymock: version does not satisfy requirement of v3.0.2, disable it.
# TODO: migrate easymock from v2.2 to v2.5 in protobuf v3.0.2 source?
build_args_v3.0 := --with python --without java --without gtest --without emacs
build_args_v3.2 := --with python --without python3 --without java

other_source := $(other_source_v$(ver))
dep_pkgs := $(dep_pkgs_build_v$(ver))
build_args := $(build_args_v$(ver))

.PHONY: all build

all: build

build: protobuf-$(ver).spec
	-@sudo yum --enablerepo=epel install -q -y $(dep_pkgs)
	@sudo rpm -V --nofiles $(dep_pkgs)
	@spectool -g -R $<
	@cp -f $(other_source) $(RPM_BUILD_ROOT)/SOURCES/
	@rpmbuild -bb $(build_args) $<
	@find $(RPM_BUILD_ROOT)/RPMS -name "*protobuf*-$(ver)*.rpm" -exec ls -ld {} \;
