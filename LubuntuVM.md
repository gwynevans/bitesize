# LubuntuVM Notes

Notes from setting up a Lubuntu 18.10 VM (Mar'19)

Not completely plain sailing, unfortunately...

1. Pretty near the end of the (1st) installation, there was a CertificateError reported, where the installer failed to validate a particular domain.  ("Boost.Python" error of some form.)  Anyway, workaround was to redo the installation without an internet connection from the VM.  Ths offline install did mean that the auto-partitioning wasn't available but was able to (after a bit of fiddling) reuse the partition created by the first attempt.

2. Installing `pwntools` suggests doing a `pip install --upgrade pip` before installing - DON'T DO THIS unless in a virtualenv, as after pip v10, this will break pip.  (Paraphrasing, fix is to pip uninstall, then apt --reinstall python-pip).

3. When installing Vmware Tools, just 'apt install open-vm-tools-desktop', not the one via the Vmware CD image).

4. Lubuntu keyboard config doesn't seem to work, but haven't yet investigated beyond trying the Settings GUI and finding the changes failing to take effect/persist.

Other than that, still continuing with it, as I just need a lightweight VM to run gdb/gef, etc.