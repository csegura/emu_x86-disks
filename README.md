# emu_x86-disks: free disk images for emu_x86

Disk images that are ready to use with [emu_x86](https://github.com/csegura/emu_x86), an IBM PC/XT and 386 PC emulator for the
browser and Linux. Every image here is free software that may be shared: [FreeDOS](https://www.freedos.org/) 1.4.

**[Boot FreeDOS in your browser](https://emux86.romheat.net/?machine=386&hdd=https://blog.romheat.net/emu_x86-disks/freedos-hd.img.gz)**

| Image | Size | Machine | What it is |
| --- | --- | --- | --- |
| `freedos-hd.img` | 64 MB | 386 PC | A hard disk with FreeDOS 1.4 installed (base system). It boots to `C:\>` with the mouse driver (CTMOUSE) and the CD-ROM driver (UDVD2 and SHSUCDX: the CD is D:) loaded. The kernel needs a 386 or better. |
| `freedos-hd.img.gz` | 8 MB | 386 PC | The same disk, compressed with gzip. The emulator page loads it by address and unpacks it in the browser: this is the file of the online demo (GitHub Pages compresses a plain image on the way, and its ranges then count compressed bytes). |
| `freedos-boot.img` | 1.44 MB | XT and 386 | The FreeDOS 1.4 boot and install floppy, unchanged from the FreeDOS Floppy Edition. The other install floppies are in that edition. |

## How to use them

- **In the browser:** open the emulator page, choose **386**, and in the Mount menu of **C:** use **From URL...** with
  `https://blog.romheat.net/emu_x86-disks/freedos-hd.img.gz`, or load the downloaded file with **Load file**.
- **With `make serve`:** put `freedos-hd.img` in `disks/hd/` and `freedos-boot.img` in `disks/floppy/` of your emu_x86 folder.
- **On Linux:** `build/host/emu_386 --window -b src/bios/seabios.bin -v src/bios/vgabios.bin -d freedos-hd.img`.

The files are raw disk images (a partition table and a FAT16 volume), so other emulators and `mtools` read them too. Check a download
with `sha256sum -c SHA256SUMS`.

## How they were made

`freedos-hd.img` was made by the FreeDOS installer itself, on the emulated 386 PC: `tools/make_freedos.sh` of emu_x86 downloads the
FreeDOS 1.4 Floppy Edition (and checks its SHA-256), boots the install floppy with an empty 64 MB disk, and lets `emuctl` answer the
installer's questions and change the floppies. Run it again to get the same system:

```
tools/make_freedos.sh /tmp/freedos-work freedos-hd.img
```

## Licences

FreeDOS is free software. See [LICENSES.md](LICENSES.md) for the licences and for where to get the source code.
