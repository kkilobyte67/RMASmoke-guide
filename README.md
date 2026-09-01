# RMASmoke-guide
# a guide on how to disable wp (write protection) with using only software, which is AKA: RMASmoke, so without messing with hardware

> [!WARNING]
> I am NOT responsible for risks or bricks that happen to Your device

> [!NOTE]
> RMASmoke does NOT WORK on Ti50 security chips, only on older Cr50 ones, and also you HAVE TO be on chromeOS version 122 or lower, for RMASMoke to work and disable WP, (Write Protection), and one more thing, RMASmoke cannot work while Enrolled!!!

First, Powerwash, using, `esc+⟳+⏻ ` (`esc+refresh+power`) then `ctrl + d`

and then once finished powerwashing, while on this screen:

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSdl6xZ9Lq8ies6-vpGnBxfCjKU1F05KpiVeozPgzlWTw&amp;s=10" alt="Basic &amp; direct keyboard connection needed to re-enable OS verification : r/chromeos"/>

press: `ctrl + d`

then log in and everything and stuff like that, and then download [RMASmoke](https://github.com/FWNavy/RMASmoke), by pressing the green code button and then download zip, like this:

<img width="780" height="382" alt="Screenshot 2026-09-01 11 28 24 AM" src="https://github.com/user-attachments/assets/f50161a3-5471-487a-9be0-28dbd16c6b2b" />

> [!NOTE]
> then in crosh, paste this command to boot into RMASmoke

```
#!/bin/bash
CHROOT_PATH=/mnt/stateful_partition/rmasmoke_root
tpm_manager_client destroy_space --index=0x80000A
crossystem clear_tpm_owner_request=1
crossystem clear_tpm_owner_request=1 #grunt weirdness
initctl stop trunksd
initctl stop tpm_managerd
initctl status tpm2-simulator # Chk the pid of tpm2 
mount --bind /dev $CHROOT_PATH/dev
mount --bind /proc $CHROOT_PATH/proc
mount --bind /var $CHROOT_PATH/var
chroot $CHROOT_PATH rmasmoke "$@"
umount $CHROOT_PATH/dev
umount $CHROOT_PATH/proc
umount $CHROOT_PATH/var
initctl start trunksd
initctl start tpm_managerd
initctl status tpm2-simulator #Check if the tpm2 simulator has crashed
```

# And Hooray!!! Now WP (AKA: Write Protection) is Disabled!

