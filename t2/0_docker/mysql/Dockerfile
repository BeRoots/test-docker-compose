# syntax=docker/dockerfile:1

##
# MySQL Debian 10 (buster) amd64 Created By Sebastien Deschamps FROM mysql:5.6
##
FROM mysql@sha256:0cec2428f4827e0581893af9b8d9fbfa84c3dbf2add6aabc645efa7f773bc00f
LABEL maintainer="Sebastien Deschamps <sdx007.com@gmail.com>" description="MySQL Server on Debian 10 (buster) amd64" version="1.0"

##
# DEFAULT SHELL
##
SHELL ["/bin/sh", "-c"],


##
# OVERRIDABLE ARGS VARIABLES (A good security practice is to not log the build command in your bash history)
##
ARG ROOT_PASSWD="rootUndefined@1+1=2!"
ARG USER_LOGIN="dev"
ARG USER_GROUP="dev"
ARG USER_UID="1000"
ARG USER_GID="1000"
ARG USER_PASSWD="userUndefined@1+1=2"
ARG USER_NAME="developer"
ARG USER_ROOM=""
ARG USER_WPHONE=""
ARG USER_HPHONE=""
ARG USER_OTHER="No more informations about ${USER_NAME}"
ARG SYS_TZ="Europe/Paris"


##
# NOT OVERRIDABLE ARGS VARIABLES
##
ARG DEBIAN_FRONTEND="noninteractive"


##
# ENVIRONMENT VARIABLES
##
# Default to supporting utf-8
ENV HISTSIZE=1000
ENV HISTFILESIZE=1000
ENV TZ=${SYS_TZ}
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8


##
# 1) Root Stage:
#
# INFOS: This is the Container Administrator Stage. This stage is implemented by the maintainer only and provide a full devtool stack
#        for PHP oriented project.
#
# /!\ IMPORTANT: DON'T CHANGE ANYTHING ON THIS STAGE. CONTACT THE MAINTAIRNER FOR ANY CHANGES REQUEST.
#
#    - Set Root BASH History Log
#    - Change root password (overridable by the user through the docker-compose build used on install-env.* scripts)
#    - Create user/group dev that match 1000:1000 by default (overridable by the user through the docker-compose build used on install-env.* scripts)
#    - Change dev user password (overridable by the user through the docker-compose build used on install-env.* scripts)
#    - Set system clock from UTC hardware clock (overridable by the user through the docker-compose build used on install-env.* scripts)
#    - Add APT sources for MySQL
#    - Install MySQL Server
#    - Securize MySQL Installation
#    - Clean APT
##
RUN set -eux && \
echo "\e[36m====================\n\n[MYSQL CONTAINER BUILD STAGE] Add/Set users\n\n====================\e[0m" && \
echo "root:${ROOT_PASSWD}" | chpasswd root && \
addgroup --gid ${USER_GID} ${USER_LOGIN} && \
adduser ${USER_LOGIN} --uid ${USER_UID} --gid ${USER_GID} --gecos "${USER_NAME},${USER_ROOM},${USER_WPHONE},${USER_HPHONE},${USER_OTHER}" --disabled-login && \
echo "${USER_LOGIN}:${USER_PASSWD}" | chpasswd ${USER_LOGIN} && \
echo "\e[36m====================\n\n[MYSQL CONTAINER BUILD STAGE] Set TIMEZONE: ${SYS_TZ}\n\n====================\e[0m" && \
[ $(which timedatectl) ] && timedatectl set-timezone ${SYS_TZ} || rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/${SYS_TZ} /etc/localtime
