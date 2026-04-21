# ssv6x5x_compiled_for_6.18.23-current-rockchip

here is the module driver files only for the 6.18.23-current-rockchip kernel. It works for the rk3228a cpu, but it might work for other CPUs that can run the rk32xx-box armbian as well...

Clone the Repo then:

# 1. Install Firmware and Driver
sudo cp ./ssv6x5x-wifi.cfg /lib/firmware/

sudo cp ./ssv6x5x-sw.bin /lib/firmware/

sudo cp ./ssv6x5x.ko /lib/modules/$(uname -r)/kernel/drivers/net/wireless/

sudo depmod -a

# 2. Force Firmware Path and Reload
echo 'options ssv6x5x stacfgpath="/lib/firmware/ssv6x5x-wifi.cfg" cfgfirmwarepath="/lib/firmware/ssv6x5x-sw.bin"' | sudo tee /etc/modprobe.d/ssv6x5x.conf

sudo rmmod ssv6051 2>/dev/null

sudo rmmod ssv6x5x 2>/dev/null

sudo modprobe ssv6x5x

# 3. Make it permanent
cat <<EOF > /etc/modprobe.d/armbian_ssv6x5x.conf
blacklist ssv6051
ssv6x5x
EOF

# 4. Reboot

# 5. Coonnect using nmtui or nmcli…

More info on: https://forum.armbian.com/topic/57960-sv6256p-wifi-now-working-on-linux-6x-armbian-tested
