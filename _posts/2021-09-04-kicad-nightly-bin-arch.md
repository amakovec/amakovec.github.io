---
layout: post
title: Repackaging .debs for Arch Linux's AUR (kicad-nightly-bin)
---

For my personal projects, I use KiCAD for design capture.  KiCAD has had a 6.0 release in the works for a while, but as of this writing has not released yet.  The features of 6.0 are available on GitLab main branch and in the nightly builds that are officially provided for many platforms, not including Arch.  One of my older machines has a long-standing install of Arch that I don't have the heart to remove, and I wanted to get KiCAD nightly working on this machine without the need to build it every time it's updated.

## Use Case and Requirements

Here's what I was looking for in a KiCAD package:

* Runs on Arch
* Pre-built packages
* Fully automated nightly updates

Arch previously offered 3 packages for KiCAD:

* `kicad` (official repos): Stable binary.
* `kicad-git` (AUR): Latest from main branch (5.99) on GitLab.  Always up-to-date.  Requires building on the client machine.
* `kicad-nightly` (AUR): Tagged nightly commits from main branch on GitLab.  Automatically updated daily.  Requires building on the client machine.

Unfortunately, none of these packages quite met my requirements, so I set out on making my own.

## First Implementation - VPS Build Server

The first idea I had for an implementation was putting a build server up in the cloud that would automatically run a build, upload it to object storage, and generate a new PKGBUILD automatically.  I drafted a high-level process for the build script and started writing an implementation in Python to run on a Linode VPS.  Partway through, I started getting bogged down with some of the drawbacks of this solution:

* **Cost:**  Linode instance (\$1.86/mo) + Linode object storage (\$5/mo) = \$6.86/mo -> \$82.32/yr
* **Complexity:** Heroku launches a Linode instance -> Linode updates Arch instance -> Linode builds -> Linode pushes package to object storage -> Linode pushes PKGBUILD to AUR repo -- too many parts!

## Final Implementation - Client-Side .deb extract -> Arch package

Halfway through the implementation of the VPS build server implementation, I ran across [`debtap`](https://github.com/helixarch/debtap), a package that converts .deb packages into Arch Linux packages.  I checked the [top packages on the AUR](https://aur.archlinux.org/packages/?SB=p&SO=d) to see if any utilized this package - none did, but I ran across a few that did similar things manually, including `spotify`, `google-chrome`, and `teams`.  I tried writing a PKGBUILD for KiCAD nightly using the Launchpad .deb builds.  I tried it out manually on a Manjaro VM and got it working, with the following caveats:

* `kicad` (stable Arch package) had to be installed as a dependency
* `glew-2.1` had to be installed as a dependency to resolve an error in opening pcbnew
* `wxWidgets` encounters an warning: "Mismatch between the program and library build versions detected"
    * non-fatal error - closing the dialog box allows the user to ignore
    * Rebuilding and reinstalling `wxgtk3` and `wxgtk-common` via their PKGBUILD fixes this issue, but is not required.

Most importantly, _it worked_, and it addressed both of my concerns with the VPS solution.

### High-Level Process

A Heroku worker process is launched every 10 mins using Heroku Scheduler, which does the following:

1. Gets the latest `kicad-nightly-bin` version from the AUR via the REST API
2. Gets the latest `kicad-nightly` version from Launchpad via `launchpadlib`
3. Compare the Launchpad and AUR version - if the version on Launchpad is not newer than the AUR package, stop the worker.  Else, continue.
4. Get the URL of the latest `kicad-nightly` .deb from Launchpad via `launchpadlib`.
5. Download the latest `kicad-nightly` .deb from Launchpad to the Heroku worker, and calculate the sha256sum of the .deb
6. Clone the AUR git repo using `dulwich`
7. Use `jinja2` to populate PKGBUILD_template
8. Stage, commit, and push changes to the AUR git repo

## Closing Thoughts

This project was a good exercise for me in choosing solutions that are maintainable over solutions that are complex, at the cost of sacrificing some performance.  Overall, the .deb extract solution ended up being a pretty maintainable, low-complexity (and free!) solution, which made its dependency drawbacks acceptable.  

If you want to see the source, you can access it on GitHub: [amakovec/kicad-nightly-bin-arch](https://github.com/amakovec/kicad-nightly-bin-arch).  If you want to install the package via the AUR on your own machine, you can find the PKGBUILD on the AUR: [`kicad-nightly-bin`](https://aur.archlinux.org/packages/kicad-nightly-bin/)
