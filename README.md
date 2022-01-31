# install-debian-zfs-sysvinit

Buggy. Do not use unless you're feeling adventurous and like supporting
your own systems.

Install Debian on ZFS, with sysvinit, optionally encrypted. You can
optionally use legacy mountpoints and manage mounts with fstab, and that's
Just Fine.

Parts of this have doubtless bitrotted - I don't use native encryption
much, for instance. Worked last time I tried it.

This used to support Devuan and Ubuntu installs as well, and can trivially
support those with some minor modifications. I'm going to do a Void version
at some point.

Needs more documentation. Probably loaded with bugs. Works for me most of
the time.

*** This will destroy your disk. By design. Don't use it. ***

Note that pre-existing MD-RAID metadata will often resurrect itself
spontaneously, so in my actual usage, I often stop between steps, mdadm
--stop --scan, and mdadm --zero-superblock the right places. Automating
this has been a merry chase so I've yanked that out for this initial
posting.

Note that this requires that you have a local APT repository with ZFS
packages. I follow this guide:

[Custom Packages](https://openzfs.github.io/openzfs-docs/Developer%20Resources/Custom%20Packages.html)

I use a metapackage that depends on the most recent two ZFS kmod packages
I've created and that conflicts with anything newer than a kernel for which
I've already built ZFS. Each kmod package is specific to a kernel, and
depends on the ZFS userland packages and the requisite kernel bits. I'll
publish examples sometime. It's possible you can use DKMS instead, but I
wouldn't want to.

Oh, FWIW, this is intended to run off from the Debian standard live media.
It's historically also run from Ubuntu live images. It can cross-install.

Note that my funny try/catch trick is generally useful and I need to use it
everywhere. Note also that I need to make this way more granular, with each
option having its own checkpoint. I lump some things together now that
should be distinct. But I want to get this out rather than just shoving the
version de jeur into pastebins every few months for years now.
