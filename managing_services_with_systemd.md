

# Chapter 2. Managing Services with Systemd

Servislerin systemd üzerinden yönetilmesi nasıl olur ?

'''console
#! /bin/sh

### BEGIN INIT INFO
# Provides:		sshd
# Required-Start:	$remote_fs $syslog
# Required-Stop:	$remote_fs $syslog
# Default-Start:	2 3 4 5
# Default-Stop:
# Short-Description:	OpenBSD Secure Shell server
### END INIT INFO

set -e

# /etc/init.d/ssh: start and stop the OpenBSD "secure shell(tm)" daemon

test -x /usr/sbin/sshd || exit 0
( /usr/sbin/sshd -\? 2>&1 | grep -q OpenSSH ) 2>/dev/null || exit 0

umask 022

if test -f /etc/default/ssh; then
    . /etc/default/ssh
fi

. /lib/lsb/init-functions

'''

