---
title: "OVH & Docker - Failed to register layer: devmapper"
date: 2017-02-06T15:12:23+01:00
comments: true
categories: [docker, devops]
---
I've been using OVH's dedicated server range recently. When ever I tried to use docker with the Ubuntu latest LTS I ended up with an error `failed to register layer: devmapper:`. The solution is rather simple, OVH dedicated servers use rather old and unsupported kernel versions.
The solution is upgrade linux kernel.
<!--more-->

Step 1. Install the latest kernel, tools, and extra stuff.

`apt-get install linux-image-4.8.0-34-generic linux-tools-4.8.0-34-generic linux-image-extra-4.8.0-34-generic `

Step 2. Move the old kernel out of the /boot directory.
`mv bzImage-3.14.32-xxxx-grs-ipv6-64 /root/`

Step 3. Run grub update so it boots into the new kernel.
`update-grub`

Step 4. Reboot so it uses the new kernel.
`reboot`
