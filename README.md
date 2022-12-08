# Hardware setup and software installation

tested on Ubuntu 22.04 on RPi 4B (2018) with
- USB stick RTL-SDR.com (https://www.amazon.com/dp/B0129EBDS2)
- discone antenna (better use this: https://www.amazon.com/Flightaware-1090MHz-Aviation-Receiver-Software/dp/B09P19H1Q8)

# Software installation

make sure to be in your home directory
```
mkdir dump1090-master
cd dump1090-master
```

download https://github.com/flightaware/dump1090 here

```
sudo apt-get install build-essential fakeroot librtlsdr-dev pkg-config libncurses5-dev net-tools
make RTLSDR=yes
```

# dump1090 to start on reboot

edit [dump1090.sh](https://github.com/Sky360-Repository/ads-b/blob/main/dump1090.sh) and add your local geo coordinates and dump1090-master path
```
sudo cp dump1090.sh /etc/init.d
sudo chown root /etc/init.d
sudo chgrp root /etc/init.d
```

# starting dump1090 with webinterface

```
mkdir public_html/data
chmod 777 public_html/data
python3 -m http.server 8080 &
sudo /etc/init.d/dump1090.sh start
```

# starting dump1090 in terminal mode

```
sudo ./dump1090 --metric --lat <latitude in decimals> --lon <longitude in decimals> --interactive
```

# TODO

**ADS-B**

ROS2 node using dump1090 outputs and noelec hardware (hardware not needed for development)

- [x] thanks to Matti/Finland for testing the hardware with dump1090
