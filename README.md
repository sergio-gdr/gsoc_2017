# GSoC 2017 Final Report

## Introduction
[QEMU](https://qemu.org/) is "*a generic and open-source machine emulator and virtualizer*". As an emulator, it provides full-system emulation, that is, it allows execution of an unmodified operating system on any of the architectures it supports. In the virtualization area, it provides support for using various in-kernel accelerators or hypervisors, in order to achieve near-native performance in its full-system emulation. The most prominent of these is the use of kvm under Linux.

Hypervisor.framework, or HVF, is macOS's native hypervisor or in-kernel accelerator. It is a recently added framework (available since Mac OS X 10.10 Yosemite) that includes an userspace-facing API that allows for taking advantage of virtualization facilities outside kernel mode.

The aim of my 2017 GSoC project is to add support in QEMU for using HVF so that full-system emulation can benefit from the performance gain when executing code for the x86_64 architecture.

## Project Execution
Various possible strategies were evaluated. The best plan that my mentor and I could draw was look for available implementations of Virtual Machine Managers using HVF. Fortunately, we found that Google maintains one such VMM, and best, it is based on an earlier version of QEMU (Ver. 2.8). We decided to take this implementation and integrate it with upstream QEMU, while also implementing a number of missing features. A significant amount of code refactoring was necessary before patches could be sent upstream, including adjusting the whole code base to QEMU's particular coding style.

Initially some code related to the emulation of the xsave/xrstr instructions had to be pulled out of KVM into a new file; these new helper functions are now shared by KVM and HVF.

## Repository Overview
This repository contains the directories for the various patchsets that have been sent upstream.
