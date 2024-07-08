# Nix on Snapdragon Elite X Hyper V

A NixOS derivate that generates a bootable iso for Snapdragon X Elite's Hyper V.  

No existing linux .iso I am aware of work properly on Hyper V.  A standard NixOS image may boot, but runs very slowly, taking hours to boot the kernel.

I noticed WSL2, which runs on Hyper V is quite fast.  So I created an image with the Microsoft WSL 2 Kernel.  I tried using Microsoft's kernel config, as well as letting Nix generate the config.  Both work.

## Generating

I generated the image in an Arm64 VM running on my M2 Pro Apple Silicon, using qemu (via UTM) to run NixOS.  I avoided cross compiling by doing this, however cross compiling will probably work.

I am using Nix packages 24.05.  If using the Microsfot config, all the BPF and BTF config options need to be disabled to avoid build error.

Download the .nix iso file into a folder.
Run

Note, the install boots a working terminal.  The system installed by the graphical installer doesn't seem to work, I am not sure why.

```
nix-shell -p nixos-generators --run "nixos-generate --format iso --configuration ./iso_wsl.nix -o result"
```


