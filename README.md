# freebsd-kernel-ci-example

Example of using [imrcpan/freebsd-kernel-ci-tester](https://github.com/imrcpan/freebsd-kernel-ci-tester)
from another repository's CI.

The workflow [`freebsd-ci.yml`](.github/workflows/freebsd-ci.yml) can only be
started by hand (Actions tab, "Run workflow"; source repo and branch are
inputs). It

1. builds the FreeBSD kernel from source on the runner on top of the latest
   official prebuilt world of the same branch (`skip-world`, on by default;
   untick it to build the whole world too), installs it, reboots into it and
   exports the system as a one-day artifact,
2. then runs two parallel jobs on exactly that system:
   * `fastfetch`: installs and runs `fastfetch`
   * `cpu-sysctl`: runs `sysctl -a | grep cpu`

No cache is used; the built system is only handed over as an artifact.
A kernel-only build takes tens of minutes with KVM; with the world it takes
hours (job limit is 6 hours).
