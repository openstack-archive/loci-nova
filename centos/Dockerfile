ARG FROM=centos:7
FROM ${FROM}

ENV PATH=/var/lib/openstack/bin:$PATH
ENV PROJECT=nova
ARG WHEELS=openstackloci/requirements:centos
ARG PROJECT_REPO=https://git.openstack.org/openstack/${PROJECT}
ARG PROJECT_REF=master
ARG SCRIPTS_REPO=https://github.com/openstack/loci
ARG SCRIPTS_REF=master
ARG OVERRIDE=override
ARG DISTRO

ADD $OVERRIDE /

RUN set -x \
    && yum upgrade -y \
    && yum install -y git \
        iproute \
        libpython2.7 \
        libvirt0 \
        libxml2 \
        openvswitch \
    && git init /tmp/common/ \
    && git --git-dir /tmp/common/.git fetch --depth 1 $SCRIPTS_REPO $SCRIPTS_REF \
    && git --work-tree /tmp/common --git-dir /tmp/common/.git checkout FETCH_HEAD \
    && /tmp/common/scripts/install.sh libvirt-python
