+++
title = "Install Packettracer in Archlinux"
date = 2025-03-05
+++
1. Go to https://www.netacad.com/about-networking-academy/packet-tracer/ and create a account or login if you have an existing Network Academy Account.
![image](/images/install-packettracer-1.png)
2. After login search for Cisco Packet Tracer in the search bar and click on learning collection one.
![image](/images/install-packettracer-2.png)
3. Scroll down and click on Getting Started with Cisco Packet Tracer.
![image](/images/install-packettracer-3.png)
4. Now click on Get Started With Self-Paced, new page will load.
![image](/images/install-packettracer-4.png)
5. Scroll down and click on the link to download
![image](/images/install-packettracer-5.png)
	![[Pasted image 20250212210454.png]]
6. Scroll down and click on the link to download the ubuntu version.
![image](/images/install-packettracer-6.png)
7. Then install packettracer from AUR(Arch User Repository) using any AUR helper, I use yay.
```bash
yay -S packettracer
```

8. It will give you error to put the download file in build directory. Now move to your download directory or where you downloaded the installer file and rename that file to `CiscoPacketTracer822_amd64_signed.deb`.

```bash
mv ~/Downloads
mv Packet_Tracer822_amd64_signed.deb CiscoPacketTracer822_amd64_signed.deb
```
1. Now copy this file to the build directory of AUR package, which is located at `~/.cache/yay/packettracer`.
```bash
cp CiscoPacketTracer822_amd64_signed.deb ~/.cache/yay/packettracer
```
1. Now move to build directory and build the package.
```bash
mv ~/.cache/yay/packettracer
makepkg -si
```

1. Now the Cisco Packet Tracer should be installed.
2. Now open the app it will prompt you for login and then you can use it.
![image](/images/install-packettracer-7.png)
