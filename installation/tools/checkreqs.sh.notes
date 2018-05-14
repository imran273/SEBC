#!/bin/bash

# MAIN
if [[ $# -eq 0 ]]; then
  echo "Usage: ${0} <user> <csv of ip_addresses or hostnames> <output_file_name>"
  exit 1
fi

USER="${1}"
if [[ -z $USER ]]; then
  echo 'Requires user login'
  exit 1
fi

HOSTS="${2}"
if [[ -z $HOSTS ]]; then
  echo 'Requires CSV of ip addresses or hostnames'
  exit 1
fi

OUTFILE="${3}"
if [[ -z $OUTFILE ]]; then
  echo 'Requires output filename'
  exit 1
fi

function header() {
  echo $1 >> $OUTFILE
}

function cmd() {
  echo "//--- ${1}" >> $OUTFILE
  OFS=$IFS
  IFS=,; for host in $HOSTS; do 
    ssh -t $USER@$host "hostname -f; sudo ${1}" >> $OUTFILE
  done
  IFS=$OFS
  echo "" >> $OUTFILE
}

# create a 10G file for use in testing which 
# can be used for subsequent tests
function test10gig() {
  echo "//--- CREATING 10G /tmp/test_io_10gig" >> $OUTFILE
  OFS=$IFS
  IFS=,; for host in $HOSTS; do 
    if [ -f /usr/bin/fallocate ]; then
      ssh -t $USER@$host "fallocate -l 10G /tmp/test_io_10gig"
    else
    # fallocate is not always available
      dd if=/dev/zero of=/tmp/test_io_10gig bs=16M count=64
    fi
  done
  IFS=$OFS
  echo "" >> $OUTFILE
}

# Customize with commands and headers

header '### OS INFO'
cmd 'uname -a'
cmd 'cat /etc/redhat-release' 

header '### NETWORK'
cmd 'dmesg | egrep NIC'
cmd 'egrep HOSTNAME /etc/sysconfig/network'
cmd 'cat /etc/sysconfig/network-scripts/ifcfg-eth* | egrep "^DEVICE|BOOTPROTO|ONBOOT|NETMASK|NETWORK|IPADDR|PEERDNS"'

header '### DISK INFO'
cmd 'lsblk'
cmd 'egrep "^/dev/*" /proc/mounts'
cmd 'df -h'

header '### CPU INFO'
cmd 'nproc'
cmd 'egrep "^model name\s+:" /proc/cpuinfo'

header '### MEM INFO'
cmd 'egrep "^MemTotal|SwapTotal|HugePages_Total" /proc/meminfo'

header '### SELINUX CHECK'
cmd 'egrep "^SELINUX" /etc/sysconfig/selinux'

header '### SSHD SERVICE'
cmd 'chkconfig --list sshd'

header '### USER LIMITS'
cmd 'egrep "^[^# ].+" /etc/security/limits.conf'

header '### NTP SERVICE' 
cmd 'service ntpd status'
cmd 'chkconfig --list ntpd'
cmd 'date'
cmd 'ntpq -p'

header '## FIREWALL SERVICE'
cmd 'service iptables status'
cmd 'chkconfig --list iptables'
cmd 'service ip6tables status'
cmd 'chkconfig --list ip6tables'

header '### NSSWITCH & HOST.CONF'
cmd 'egrep "^hosts:" /etc/nsswitch.conf'  
cmd 'cat /etc/host.conf'
cmd 'getent hosts' 

header '### DNS CACHE'
cmd 'service nscd status'
cmd 'chkconfig --list ncsd'

header '### SWAPPINESS'
cmd 'cat /proc/sys/vm/swappiness'

header '### IPV4 TCP'
cmd 'sysctl -a | egrep "net.ipv4.tcp_"'

