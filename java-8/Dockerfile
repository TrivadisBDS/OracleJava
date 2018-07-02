# ----------------------------------------------------------------------
# Trivadis AG, Infrastructure Managed Services
# Saegereistrasse 29, 8152 Glattbrugg, Switzerland
# ----------------------------------------------------------------------
# Name.......: Dockerfile 
# Author.....: Stefan Oehrli (oes) stefan.oehrli@trivadis.com
# Editor.....: Stefan Oehrli
# Date.......: 2018.03.19
# Revision...: 1.0
# Purpose....: This Dockerfile is to build Oracle Java 1.8
# Notes......: This Dockerfile is based on Oracle's Dockerfile for 
#              Java 1.8.
#              Build this image : docker build -t oracle/serverjre:8 .
# Reference..: https://github.com/oracle/docker-images/tree/master/OracleJava
# License....: Licensed under the Universal Permissive License v 1.0 as 
#              shown at http://oss.oracle.com/licenses/upl.
# ----------------------------------------------------------------------
# Modified...:
# see git revision history for more information on changes/updates
# ----------------------------------------------------------------------

# Pull base image
# ----------------------------------------------------------------------
FROM oraclelinux:7-slim

# Maintainer
# ----------------------------------------------------------------------
LABEL maintainer="stefan.oehrli@trivadis.com"

# Arguments for Oracle Installation
ARG ORAREPO

# Environment variables required for this build (do NOT change)
# ----------------------------------------------------------------------
ENV DOWNLOAD="/tmp/download" \
    ORAREPO=${ORAREPO:-"docker.oradba.ch"} \
    JAVA_MOS_PKG="p27412890_180172_Linux-x86-64.zip" \
    JAVA_PKG=server-jre-8u*-linux-x64.tar.gz \
    JAVA_HOME="/usr/java/default" \
    JAVA_BASE="/usr/java"

# Install libaio gzip zip unzip tar for OUD stuff 
# ----------------------------------------------------------------------
RUN echo "%_install_langs   en" >/etc/rpm/macros.lang && \
    yum install -y libaio gzip zip unzip tar && \
    rm -rf /var/cache/yum && \
    mkdir -p ${DOWNLOAD} && \
    mkdir -p ${JAVA_BASE} && \
    cd ${DOWNLOAD} && \
    [ -s "${DOWNLOAD}/${JAVA_MOS_PKG}" ] || \
    curl -f http://${ORAREPO}/${JAVA_MOS_PKG} -o ${DOWNLOAD}/${JAVA_MOS_PKG} && \
    unzip ${DOWNLOAD}/${JAVA_MOS_PKG} && \
    tar -zxvf ${DOWNLOAD}/${JAVA_PKG} -C ${JAVA_BASE} && \
    rm -rf ${DOWNLOAD}

# Install Java respectively update alternatives for Java
# ----------------------------------------------------------------------
RUN export JAVA_DIR=$(ls -1 -d /usr/java/*) && \
    ln -s $JAVA_DIR /usr/java/latest && \
    ln -s $JAVA_DIR /usr/java/default && \
    alternatives --install /usr/bin/java java $JAVA_DIR/bin/java 20000 && \
    alternatives --install /usr/bin/javac javac $JAVA_DIR/bin/javac 20000 && \
    alternatives --install /usr/bin/jar jar $JAVA_DIR/bin/jar 20000

# --- EOF --------------------------------------------------------------