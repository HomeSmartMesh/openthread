# openthread
integration of openthread and wrapper scripts

# dependencies not mentioned in the install link

  sudo apt-get install libtool
  sudo apt-get install autotools-dev
  sudo apt-get install autoconf

  sudo apt-get update
  sudo apt-get install m4

## Step 1
pi@manar:~/openthread $ socat -d -d pty,raw,echo=0 pty,raw,echo=0
===> log take first pts number for  step 2: and second for step 3:
2018/11/28 16:13:39 socat[979] N PTY is /dev/pts/1
2018/11/28 16:13:39 socat[979] N PTY is /dev/pts/2
2018/11/28 16:13:39 socat[979] N starting data transfer loop with FDs [5,5] and [7,7]


## Step 2
~/openthread/output/armv7l-unknown-linux-gnueabihf/bin/ot-ncp-ftd 1 > /dev/pts/1 < /dev/pts/1

## Step 3
docker run --sysctl "net.ipv6.conf.all.disable_ipv6=0 \
        net.ipv4.conf.all.forwarding=1 net.ipv6.conf.all.forwarding=1" \
        -p 8080:80 --dns=127.0.0.1 -it --volume \
        /dev/pts/2:/dev/ttyUSB0 --privileged openthread/otbr
