
RPM_BUILD_ROOT := $(HOME)/rpmbuild
dep_pkgs := python-dateutil python2-gflags pytz python-mox

.PHONY: all build

all: build

build: python-google-apputils.spec
	-@sudo yum --enablerepo=epel install -y $(dep_pkgs)
	@sudo rpm -V --nofiles $(dep_pkgs)
	@spectool -g -R $<
	@rpmbuild -bb $<
	@find $(RPM_BUILD_ROOT)/RPMS -name "`basename $< .spec`*.rpm" -exec ls -ld {} \;
