# setup-kali-vm-in-UTM
Setting up a Kali VM with full disk encryption in UTM can be a bit of a hassle. Here is one way to do it.

## Prereqs
- Install UTM
- Under UTM settings/display, "do not save VM screenshots to disk"
- Download a Kali installer: https://www.kali.org/get-kali/#kali-installer-images

## Create VM and setup
- Create VM in UTM from the Kali ISO file 
- Under Summmary, check `Open VM Settings`
    - Add new Device: Serial
- Boot VM
    - Graphical install in the Terminal window, make sure to pick full disk encryption when the option is given. Continue to next bullet when the installation is completed, and it prompts you to `Continue to reboot`
- Shut down the VM (force stop)
- Enter the VM settings 
    - Remove the iso drive 
    - Change the display card emulation to `virtio-gpu-pci`

- Start the VM again. You will be prompted to give your disk encryption password in the Terminal window.
- Run inside Kali: 
    - Sudo `vim /etc/default/grub`
        - Modify `GRUB_CMDLINE_LINUX_DEFAULT` and `GRUB_CMDLINE_LINUX` to the following:
          
            `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash console=tty0"`
            `GRUB_CMDLINE_LINUX="console=tty0"`
          
    - Run `sudo update-grub`

- Shut down the VM (force stop)
- Remove the serial device in options

The setup from the host perspective is done.

## Setup the VM
- According to UTM docs, `sudo apt install spice-vdagent` is needed for a shared clipboard between the host and VM.
- ...
