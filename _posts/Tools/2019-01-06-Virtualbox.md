---
title: "Install Virtualbox on Mac"
Date: 2019-01-06
---

# Install Virtualbox
## Preparation

1. MacOS: Mojave 10.14

2. Virtualbox

   VirtualBox-5.2.20-125813-OSX

3. Ubuntu

   ubuntu-16.04.5-desktop-amd64

## An error occurred during installation

- Error Messgae

When I install Virtualbox on Mac, encontered this problem:



![Install_Virtualbox_failed](images/Virtualbox/Install_Virtualbox_failed.png)

I checked this problem on website:

[virtualbox-5-1-28-fails-to-install-on-macos-10-13-due-to-kext-security](https://apple.stackexchange.com/questions/301303/virtualbox-5-1-28-fails-to-install-on-macos-10-13-due-to-kext-security).

- Allow Installation

According to its instruction, Ifound this setting, and click "Allow":

![Allow_Installation_SecurityPrivacy](images/Virtualbox/Allow_Installation_SecurityPrivacy.png)

- Reinstall Virtualbox

  Succeed after reinstall the virutualbox

  ![Install_successfully](images/Virtualbox/Install_successfully.png)

# Virtualbox congigure

## Copy And Paste Between VirtualBox Host And Guest Machines

- Devices -> Drag and Drop -> Bidirectional

![copy_paste_host_vm](images/Virtualbox/copy_paste_host_vm.png)

- Devices -> Insert Guest Additions CD images, then install it

  If the the method mentioned above still cannot work, then try this method. However, I encountered this error:

  ![InsertGuestDisk](images/Virtualbox/InsertGuestDisk.png)

  Could not mount the media/drive '/Applications/VirtualBox.app/Contents/MacOS/VBoxGuestAdditions.iso' (VERR_PDM_MEDIA_LOCKED).

  When you click the Vmware host, you are asked to install something. After install it, reboot the linux machine. And then the copy and paste function can work properly. If not, try this method: (I did not try it)

  ```
  sudo apt-get install virtualbox-guest-utils
  ```

## Resizing a VirtualBox Disk Image (.vmdk) on a Mac

According to [Resizing a VirtualBox Disk Image (.vmdk) on a Mac](https://www.jeffgeerling.com/blogs/jeff-geerling/resizing-virtualbox-disk-image), there are two methods:

1. **Convert and resize the disk image**
    First,  shutdown your VM, then in Terminal or on the command line:

    ```bash
    # Resize the new .vdi image (30720 == 30 GB).
    vboxmanage modifyhd "virtualdisk.vdi" --resize 30720
    ```

    For example:

    ```bash
    $ vboxmanage modifyhd --resize 30720 Ubuntu164.vdi
    0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
    ```

2. Resize the disk image using gparted**

    1. [Download the gparted .iso](http://gparted.org/download.php)

    2. Mount the .iso as a CD/DVD drive in VirtualBox for your VM

    3. Start your VM, and on the boot screen, hit F12 to select the gparted iso image for boot

    4. Follow the instructions for gparted's startup, then in the GUI (or on the command line) [resize the partition](http://askubuntu.com/a/269072) on your new disk image so it uses all the unallocated free space).

        **Resize the Extended Partation**

        ![Partation_extend](images/Virtualbox/Partation_extend.png)

        **Create New Partation**

        ![Create_new_partation](images/Virtualbox/Create_new_partation.png)

        The default install paht of "apt-get install" cannot be changed. Therefore, It's needed to allocate large size space for "/home" partition.

        If not, you can try this method. But this is very **dangerous**. Refer [Increase the /home partition without losing the data](https://askubuntu.com/questions/29866/increase-the-home-partition-without-losing-the-data) for detail.

        ![extend_home_partation](images/Virtualbox/extend_home_partation.png)

        I tried this approach succesfully without lost the original data.
