# DIP

[![GoDoc Widget](https://godoc.org/github.com/030/dip?status.svg)](https://godoc.org/github.com/030/dip)
[![Go Report Card](https://goreportcard.com/badge/github.com/030/dip)](https://goreportcard.com/report/github.com/030/dip)
[![Build Status](https://travis-ci.org/030/dip.svg?branch=master)](https://travis-ci.org/030/dip)
[![DevOps SE Questions](https://img.shields.io/stackexchange/devops/t/dip.svg)](https://devops.stackexchange.com/questions/tagged/dip)
![Issues](https://img.shields.io/github/issues-raw/030/n3dr.svg)
![Pull requests](https://img.shields.io/github/issues-pr-raw/030/dip.svg)
![Total downloads](https://img.shields.io/github/downloads/030/dip/total.svg)
![License](https://img.shields.io/github/license/030/dip.svg)
![Repository Size](https://img.shields.io/github/repo-size/030/dip.svg)
![Contributors](https://img.shields.io/github/contributors/030/dip.svg)
![Commit activity](https://img.shields.io/github/commit-activity/m/030/dip.svg)
![Last commit](https://img.shields.io/github/last-commit/030/dip.svg)
![Release date](https://img.shields.io/github/release-date/030/dip.svg)
![Latest Production Release Version](https://img.shields.io/github/release/030/dip.svg)
[![codecov](https://codecov.io/gh/030/dip/branch/master/graph/badge.svg)](https://codecov.io/gh/030/dip)
[![GolangCI](https://golangci.com/badges/github.com/golangci/golangci-web.svg)](https://golangci.com/r/github.com/030/dip)
[![BCH compliance](https://bettercodehub.com/edge/badge/030/dip?branch=master)](https://bettercodehub.com/results/030/dip)
[![Chocolatey](https://img.shields.io/chocolatey/dt/dip)](https://chocolatey.org/packages/dip)

<a href="https://dip.releasesoftwaremoreoften.com"><img src="https://github.com/030/dip/raw/master/logo/logo.png" width="100"></a>

Docker Image Patrol (DIP) keeps docker images up-to-date.

## Usage

```bash
Usage of dip:
  -debug
        Whether debug mode should be enabled
  -image string
        The origin of the image, e.g. nginx:1.17.5-alpine
  -registry string
        To what destination the image should be transferred, e.g. quay.io/some-org
exit status 2
```

### Absent

Check whether a docker-image resides in a docker-registry:

```bash
dip -image nginx:1.17.5-alpine -registry quay.io/some-org/
```

An ```exit 0``` will be returned if the image is absent and an ```exit 1``` is
applicable if it already exists to prevent that the tag gets overwritten.

or by using regex:

```bash
go run main.go -image ubuntu -registry quay.io/some-org/ -latest "xenial-\d.*"
```

## latest

### alpine

```bash
go run main.go -image alpine -latest "(\d+\.){2}\d"
```

### nexus

```bash
go run main.go -image sonatype/nexus3 -latest "(\d+\.){2}\d"
```

### nginx

```bash
go run main.go -image nginx -latest ".*(\d+\.){2}\d-alpine$"
```

### sonarqube

```bash
go run main.go -image sonarqube -latest ".*-community$"
```

### traefik

```bash
go run main.go -image traefik -latest "^v(\d+\.){1,2}\d+$"
```

### ubuntu

```bash
go run main.go -image ubuntu -latest "^xenial.*" -semantic=false -debug=true
```

## preserve

It it possible to preserve images from dockerhub in a private registry:

```bash
go run main.go -image ubuntu -registry quay.io/some-org/ -latest "xenial-\d.*" -preserve
```

## date

Use ```-date``` to ensure that an image with security updates can be stored
without having to worry that a tag will be overwritten.

```bash
go run main.go -image sonarqube -latest ".*-community$" -preserve -registry quay.io/some-org/ -date
```
