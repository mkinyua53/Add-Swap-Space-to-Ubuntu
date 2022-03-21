# How to add swap space to Ubuntu
This is the code I run to add swap space to Ubuntu.

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon --show
sudo cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

```
Running this code will create a swap file of 2GB and then activate it.

## Explanation
Allocate 2GB of swap space on the system.
```bash
sudo fallocate -l 2G /swapfile
```
Of course you can use any size by replacing 2G with the size you want.

Change the permissions of the swap file to 600.
```bash
sudo chmod 600 /swapfile
```
Confirm that the file is created and the permissions are correct.
```bash
ls -lh /swapfile
```
Create the actual swap file.
```bash
sudo mkswap /swapfile
```
Activate the swap file.
```bash
sudo swapon /swapfile
```
Confirm that the swap file is active.
```bash
sudo swapon --show
```
We need to make sure the swapfile will survive a reboot. Take a backup of the fstab file.
```bash
sudo cp /etc/fstab /etc/fstab.bak
```
Add the swapfile to the fstab file.
```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

## Credits
 - [Brian Boucheron](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04)

Visit [this page](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04#step-6-tuning-your-swap-settings) for more performance tips after adding swap space.

## The Why
Sometimes, I noted that my EC2 instance would freeze while running [Composer](https://getcomposer.org/) related tasks. Adding swap space solved the problem.

Enjoy! ☕
