# Package details
export OS ?= $(shell uname -s | tr '[:upper:]' '[:lower:'])
export DISTR ?= $(shell grep ^ID= /etc/os-release 2>/dev/null | cut -d= -f2 | tr '[:upper:]' '[:lower:'])

ifeq ($(OS),darwin)
	OS=macos
endif

ifeq ($(DISTR),alpine)
	OS=alpine
endif

export VENDOR ?= codefresh-io
export REPO_NAME ?= cli
export NAME ?= codefresh
export APK_BUILD_TEMPLATE ?= APKBUILD.github-binary
export DOWNLOAD_URL ?= $(REPO_URL)/releases/download/v$(VERSION)/codefresh-v$(VERSION)-$(OS)-x64.tar.gz
export APKBUILD_DEPENDS += ca-certificates

## Required for testing on build
export CFCONFIG ?= ./src/.cfconfig

export EXE = codefresh

include ../../tasks/Makefile.package
include ../../tasks/Makefile.apk

install:
	$(call download_tarball)

test:
	$(EXE) version