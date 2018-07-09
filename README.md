# Reden snap

Snap package for the `kyd-cli`, `kyd-tx`, `kydd`, and `kyd-qt` binaries for easy installation on Linux systems. Check the [KYD repostory](https://github.com/kydcoin/KYD) for more information about the KYD project.

It's currently only tested on Solus OS with X11, so please test on other desktop environments if you will.

<details>
  <summary>What is KYD?</summary>
  <p>KYD Core is a decentralized, peer-to-peer cryptocurrency with a primary focus on energy-efficiency and scalabilty. The KYD Network makes use of only Proof-of-Stake mining, in the form of masternodes and staking. This means that the KYD blockchain has a very low impact on the environment and ensures that scaling will be a smooth transition in future.

Furthermore, as result of offering multiple ways for users to mint new KYD coins, the network is a lot less centralized than some Proof-of-Work coins that have their hashrates dominated by one or two mining pools..</p>
</details>

<details>
  <summary>What is a snap?</summary>
  <p>Snaps are containerised software packages that are simple to create and install. They auto-update and are safe to run. And because they bundle their dependencies, they work on all major Linux systems without modification.</p>
</details>

<hr/>

> **DISCLAIMER**
>
> This repository is purely intended as an exercise in creating snap packages. Don't use this wallet to store crypto without a proper audit of both the snap and the upstream KYD repository. In other words: don't trust random code on the interwebs!

# Installing

On any snap enabled Linux system:

```
$ snap install kyd-thebeard --edge
$ kyd-thebeard.kyd-qt
```

You can now see all installed applications by running `snap info kyd-thebeard`.

Note: the final package should obviously be named `kyd` and not `kyd-thebeard` but I don't want to squat that name, I'll leave that up to the KYD team.

# Building

You normally don't need this part. This part explains building the snap, which you don't need as a user of the software.

The snap is build in a "cleanbuild" LXD container to make sure the build instructions are not polluted by random libraries installed on my system. It's slower (no caching) but makes sure you don't forget to include packages you might have on your system but are not available by default on an Ubuntu 16.04 system.

From the root directory of this repository run:

```bash
$ snapcraft cleanbuild
$ snap install kyd-thebeard_0.1_amd64.snap --dangerous
```

You can use `snapcraft cleanbuild --debug` to be dropped in the container's shell if the build fails.

# Known issues

- Starting kyd-qt throws an AppArmor warning related to dbus. This is [fixed](https://github.com/snapcore/snapd/pull/5189) in `snapd` so should resolved itself in a future `snapd` release.

# License

This repository is licensed under the [MIT license](LICENSE). The KYD application icon is a cropped copy of the [splash.png](https://github.com/kydcoin/KYD/blob/master/splash.png) image from the [KYD project](https://github.com/kydcoin/KYD) and also MIT licensed.
The repository is based on the prelimary work that has been done by [cimm](https://github.com/cimm/). He figured out all the hard parts of the snap code to make it work.