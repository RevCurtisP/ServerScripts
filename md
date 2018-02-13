#!/bin/bash

DIRUSR=$USER
while getopts ":u:" opt; do
  case $opt in
    u) DIRUSR=$OPTARG
      ;;
    : )      echo "Invalid option: $OPTARG requires an argument" 1>&2
      ;;
    *) echo "Invalid option: -$OPTARG" >&2
      ;;
esac
done
shift $((OPTIND-1))
DIRSPC=$1
DIRGRP=`id -g -n $DIRUSER`

sudo mkdir -p "$DIRSPC"
sudo chown $DIRUSR "$DIRSPC"
sudo chgrp $DIRGRP "$DIRSPC"
sudo chmod 750 "$DIRSPC"

