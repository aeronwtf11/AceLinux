<div align="center">

<img src="assets/acelinux.png" width="155" alt="AceLinux Logo">

# AceLinux

**A minimal Linux distribution. Built around your decisions.**

`Linux` · `x86-64` · `Terminal First` · `System Control`

**Start minimal. Build your system.**

---

</div>

## Overview

AceLinux is an independent, general-purpose Linux distribution focused on simplicity, user control, and a minimal starting environment.

Our goal is to create a Linux distribution that provides the essential foundations of an operating system without deciding how the user should configure their computer.

No mandatory desktop environment, no unnecessary preinstalled applications, and no excessive background services.

**AceLinux starts with a terminal. Everything else is up to the user.**

Users should be able to install the software they need, configure their system, manage services, and optionally enable a graphical environment through our own system-management tools.

Unlike AceOS, AceLinux is intended to remain based on the Linux kernel. We want to develop our own userspace components and system-management experience while retaining the compatibility and hardware support provided by Linux.

AceLinux is designed primarily for x86-64 desktop computers and laptops.

The project is currently in early development.

## Project status

**Development stage: Planning / Pre-alpha**

We are defining the system architecture and initial development milestones.

| Component | Status |
|---|---|
| Linux kernel integration | Planned |
| x86-64 support | Initial target |
| UEFI boot | Planned |
| Terminal-based environment | Planned |
| Base userspace | Planned |
| AceIt integration | Proposed |
| System configuration engine | Design phase |
| Binary package manager | Planned |
| Network management | Planned |
| User management | Planned |
| System generations and rollback | Design phase |
| Optional desktop environments | Planned |
| Graphical installer | Not planned for initial release |

These are development goals. They should not be interpreted as completed or tested functionality.

---

## Downloads & testing

### Development builds

**There are currently no public AceLinux downloads.**

We have not released an installable ISO, disk image, or official development preview.

Our first builds will focus on booting a minimal x86-64 system in a virtual machine.

| Release | Architecture | Availability |
|---|---|---|
| AceLinux Development Preview | x86-64 | Not available |
| AceLinux Alpha | x86-64 | Not available |
| AceLinux Beta | x86-64 | Not available |
| AceLinux Stable | x86-64 | Not available |

Once test images are available, we intend to provide:

- Downloadable bootable images
- Version information and changelogs
- SHA-256 checksums
- Installation instructions
- Known issues
- Verified hardware compatibility
- Testing and bug-reporting guidelines

### Testing platforms

Our initial testing environment will prioritize:

- QEMU/KVM
- x86-64 virtual machines
- Selected physical desktop and laptop computers

Experimental builds should be tested in disposable virtual machines or on dedicated hardware rather than installed over an existing operating system.

We will not publish a build as verified until it has passed the relevant boot and functionality tests.

---

## Philosophy

AceLinux follows a straightforward philosophy: **the operating system should provide a foundation, not dictate the user's environment.**

### 1. Minimal by default

A default AceLinux installation should contain only the components necessary for a usable system.

This includes:

- The Linux kernel
- A bootloader
- An initialization system
- Essential system services
- A shell and basic Unix utilities
- User and permission management
- AceLinux configuration tools
- Package-management functionality

We do not intend to ship a desktop environment, web browser, office suite, or other optional applications by default.

Users can install those components when they need them.

### 2. Terminal first

The terminal is the default user interface.

AceLinux should remain fully usable without a graphical environment.

System administration, package management, configuration, and service management should all be accessible from the command line.

A graphical interface should be an optional addition, not a requirement.

### 3. User control

The user should decide which services run, which packages are installed, and how their system behaves.

AceLinux should avoid making unnecessary assumptions about the user's preferred workflow.

A machine configured as a development workstation should not require the same software as a server or a minimal terminal environment.

### 4. Simple configuration

We want to provide a straightforward configuration experience without sacrificing low-level control.

Common operations should be handled through understandable commands rather than requiring users to manually edit numerous unrelated system files.

The system should remain transparent, with configuration stored in readable files and changes visible before they are applied.

### 5. Privacy by default

AceLinux is intended to operate without telemetry, advertising, or user tracking.

Only essential system services should run by default.

Optional network-dependent services should be configurable by the user.

### 6. Reliability and recovery

We aim to make configuration changes predictable and recoverable.

Our goals include validation before applying settings, explicit upgrades, version tracking, and recovery mechanisms.

Saved system generations should not be automatically deleted without an explicit retention policy chosen by the user.

### 7. One coherent system

AceLinux should feel like one operating system rather than a disconnected collection of tools.

Our configuration engine, package manager, service management, and system utilities should work together through consistent interfaces.

---

## Default user experience

AceLinux is intended to boot into a terminal after installation and initial account setup.

An example of the planned experience:

```text
AceLinux
----------------------------------------

acelinux login: user
Password:

Welcome to AceLinux.

System:       AceLinux
Kernel:       Linux
Environment:  Terminal
Desktop:      Not enabled

user@acelinux ~ $
```

This is an interface concept, not output from an existing build.

From here, the user should be able to configure their installation.

For example:

```sh
acelinux status

acelinux setr hostname:my-pc
acelinux setr network:true

acelinux install git vim

acelinux preview
acelinux apply
```

These commands describe the planned interface and are not yet implemented.

The important part is that users begin with a minimal system and decide what to add afterward.

---

## System architecture

AceLinux is designed around the existing Linux kernel and a minimal userspace.

```text
                       AceLinux
                          |
                   UEFI / Bootloader
                          |
                     Linux Kernel
                          |
                    Init System
                          |
                 Essential Services
                          |
                     Base Userspace
                          |
                    Terminal / Shell
                          |
                 AceLinux System Layer
                 /        |         \
          Configuration Packages   Services
                 \        |         /
                  System Management
                          |
                Optional Components
                 /        |        \
             Network    Desktop    Tools
                          |
                   User Environment
```

The terminal and base userspace form the default environment.

Additional components are enabled according to the user's configuration.

### Linux kernel

AceLinux uses the Linux kernel.

We are not attempting to replace Linux with our own kernel in this project.

The kernel provides process scheduling, memory management, filesystem support, networking, and hardware interfaces.

Our development focus will instead be on creating the userspace, configuration system, package-management tools, initialization environment, and distribution infrastructure around it.

### Initialization and services

We intend to investigate using **AceIt**, our custom initialization system originally designed for AceOS.

AceIt integration is currently a proposed direction, not a finished compatibility feature.

Its intended responsibilities include:

- Starting required system services
- Managing service dependencies
- Tracking running services
- Reporting startup failures
- Starting and stopping configured services
- Supporting controlled shutdown and reboot

AceLinux should start only the services necessary for the base system and those explicitly enabled by the user.

The final init architecture will be documented once development begins.

### Base userspace

The initial userspace is planned to provide familiar Unix tools and a usable shell.

Our intended starting components include:

| Component | Initial direction |
|---|---|
| Shell | Bash |
| Standard utilities | GNU Coreutils |
| C library | glibc |
| Filesystem | ext4 |
| Recovery utilities | BusyBox |
| Init system | AceIt integration under consideration |
| Configuration | Custom rule-based engine |
| Package manager | Custom binary package manager |

Component selections may change during development.

Our goal is compatibility with existing Linux software wherever practical, not unnecessary rewrites of established low-level utilities.

---

## System configuration

AceLinux is intended to provide a central rule-based configuration interface.

A proposed configuration file is:

```text
/etc/ace/config.sys
```

Example:

```ini
[system]
hostname:acelinux
network:false
bluetooth:false
desktop:false

[services]
ssh:false

[packages]
pkg.git:true
pkg.vim:true
```

### Command-line interface

Our planned interface includes:

```sh
acelinux --help
acelinux status

acelinux setr hostname:workstation
acelinux setr network:true
acelinux setr bluetooth:false

acelinux preview
acelinux apply
```

### How configuration should work

1. Read the existing configuration.
2. Validate requested rules and values.
3. Determine which settings need to change.
4. Show a preview of the changes.
5. Apply the configuration through the appropriate system components.
6. Record the resulting state and report failures.

AceLinux should communicate with the selected init system for service-related configuration.

The system should reject invalid or unsupported changes rather than silently ignore them.

### Relationship to AceNix

Our earlier project, [AceNix](https://github.com/aeronwtf11/AceNix), explores a similar user experience for NixOS.

We intend to carry over some of its design principles:

- Simple imperative commands
- Declarative configuration
- Readable previews
- Explicit application
- Error validation
- Recovery mechanisms

However, AceLinux will need its own backend because it is a separate Linux distribution, not a NixOS management layer.

The goal is to reuse good ideas where appropriate without introducing unnecessary dependencies on NixOS.

---

## Package management

AceLinux is planned to include a custom binary package manager.

Our goal is to make installing and maintaining software straightforward while retaining control over package sources and updates.

Proposed commands:

```sh
acelinux search firefox
acelinux install firefox
acelinux remove firefox
acelinux update
```

### Planned package-management features

- Binary package installation
- Package removal
- Dependency resolution
- Repository metadata
- Package integrity verification
- Explicit system upgrades
- Version tracking
- Transaction history
- Recovery from failed operations

We also intend to explore generation-based rollback for system changes.

The package format, repository layout, dependency solver, and update model are not yet finalized.

### Package philosophy

AceLinux should not automatically install large collections of applications the user did not request.

Dependencies necessary for selected software may still be installed automatically.

System upgrades should be explicit and understandable.

We intend to keep package metadata and system state inspectable.

---

## Networking

AceLinux should provide basic networking without requiring a graphical network manager.

Our initial goal is Ethernet connectivity using DHCP once networking has been enabled and configured.

Wi-Fi configuration will follow as hardware support and network tooling develop.

We intend to provide commands for inspecting and changing network settings while keeping advanced Linux networking interfaces accessible.

Optional network services should not be enabled without a clear reason.

---

## Desktop environments

**AceLinux does not ship with a desktop environment by default.**

Users who want a graphical environment should be able to add one later.

Our intended direction includes compatibility with existing Linux desktop environments such as:

- KDE Plasma
- GNOME
- Xfce
- Window managers and Wayland compositors

Support will depend on the required packaging, graphics stack, service integration, and hardware compatibility.

We also intend to explore our own desktop environment in the future.

A terminal-only installation will remain a supported configuration.

---

## Filesystem layout

AceLinux is intended to follow familiar Linux filesystem conventions.

Proposed layout:

```text
/
├── boot/
├── dev/
├── etc/
│   └── ace/
│       └── config.sys
├── home/
├── proc/
├── run/
├── sys/
├── usr/
│   ├── bin/
│   └── lib/
└── var/
    ├── lib/
    │   └── ace/
    └── log/
```

The initial root filesystem is expected to use ext4.

System-specific configuration and package-management state should be stored separately from user data.

The final layout will be documented as the implementation develops.

---

## Installation

AceLinux is intended to provide a terminal-oriented installation experience.

We want installation to be transparent and configurable rather than hide every operation behind a graphical installer.

The initial installer design is not finalized.

Our planned installation workflow includes:

1. Boot the AceLinux installation environment.
2. Identify the installation target.
3. Configure partitions and filesystems.
4. Install the minimal base system.
5. Configure the bootloader.
6. Create a user account and set credentials.
7. Reboot into the terminal environment.
8. Configure additional packages and services.

Installation tools must clearly identify destructive operations and require explicit confirmation before modifying disks.

We will publish verified installation instructions once a working installer exists.

---

## Building AceLinux

### Development environment

Our initial development environment will use Linux.

Planned tools include:

| Tool | Purpose |
|---|---|
| GCC / Clang | Compilation |
| GNU Make | Build automation |
| Git | Version control |
| QEMU | Virtual-machine testing |
| GDB | Debugging |
| GNU Binutils | Low-level build utilities |
| Linux kernel sources | Kernel integration |
| Image-building tools | Filesystem and bootable-image creation |

We may use established build tools for early prototypes while developing our own distribution-specific tooling.

The final build system has not yet been selected.

### Build workflow

```text
AceLinux Sources
        |
        v
Build Configuration
        |
        v
Kernel + Userspace + Utilities
        |
        v
Root Filesystem
        |
        v
Bootable System Image
        |
        v
QEMU / Test Hardware
        |
        v
Boot and Functionality Tests
```

Reproducible build commands will be documented after the first complete build configuration is committed.

There is currently no verified AceLinux image.

---

## Development roadmap

This roadmap describes our planned milestones. It is not a release schedule.

### Phase 1 — System foundation

- [ ] Establish a reproducible build environment.
- [ ] Select the initial Linux kernel baseline.
- [ ] Configure x86-64 and UEFI support.
- [ ] Build a minimal root filesystem.
- [ ] Generate a bootable system image.
- [ ] Boot successfully in QEMU.
- [ ] Reach an interactive terminal.

**Goal:** A bootable Linux system with a minimal command-line environment.

### Phase 2 — Initialization and userspace

- [ ] Finalize the init-system architecture.
- [ ] Investigate AceIt integration.
- [ ] Configure essential startup services.
- [ ] Integrate basic Unix utilities.
- [ ] Establish user and permission management.
- [ ] Add system information and diagnostics.
- [ ] Implement clean startup and shutdown behavior.

**Goal:** A reliable minimal userspace environment.

### Phase 3 — Configuration engine

- [ ] Finalize the configuration format.
- [ ] Implement rule parsing and validation.
- [ ] Develop the `acelinux` CLI.
- [ ] Implement configuration previews.
- [ ] Implement apply operations.
- [ ] Integrate service and networking configuration.
- [ ] Add recovery mechanisms.

**Goal:** A functional command-line system-management interface.

### Phase 4 — Package management

- [ ] Design the binary package format.
- [ ] Implement package metadata.
- [ ] Add installation and removal.
- [ ] Implement dependency resolution.
- [ ] Introduce repositories.
- [ ] Add integrity verification.
- [ ] Implement explicit upgrades.
- [ ] Investigate generation-based rollback.

**Goal:** Users can install and manage software independently.

### Phase 5 — Installation and hardware

- [ ] Develop an installation workflow.
- [ ] Test UEFI installations.
- [ ] Improve storage and filesystem support.
- [ ] Test networking.
- [ ] Improve laptop hardware compatibility.
- [ ] Document supported hardware.

**Goal:** AceLinux can be installed and used on selected real computers.

### Phase 6 — Optional desktop support

- [ ] Establish the graphical software stack.
- [ ] Package selected desktop environments.
- [ ] Integrate graphical sessions with the init system.
- [ ] Improve graphics and input support.
- [ ] Test desktop installation and removal.
- [ ] Investigate custom desktop components.

**Goal:** Users can choose between terminal-only and graphical installations.

### Long-term — Stable distribution

- [ ] Establish reliable package repositories.
- [ ] Improve installation and upgrade reliability.
- [ ] Expand hardware testing.
- [ ] Introduce release engineering and maintenance procedures.
- [ ] Maintain reproducible build configurations.
- [ ] Publish verified releases and security updates.

---

## Testing and verification

We want to distinguish between a system that builds, one that boots, and one that is reliable enough for everyday use.

| Test level | Purpose |
|---|---|
| Unit tests | Validate individual components |
| Integration tests | Validate communication between subsystems |
| Boot tests | Confirm successful startup |
| Configuration tests | Validate rule processing |
| Package tests | Verify installation, removal, and upgrades |
| Recovery tests | Verify failure handling |
| Installation tests | Validate installation workflows |
| Hardware tests | Verify compatibility on real devices |

Initial testing will prioritize QEMU and isolated virtual machines.

We will document known issues and avoid claiming compatibility with hardware that has not been tested.

---

## Security and privacy

AceLinux is intended to follow privacy-conscious and minimal-by-default principles.

Our goals include:

- No telemetry.
- No unnecessary tracking.
- Minimal enabled services.
- Explicit administrative operations.
- Verified package integrity.
- Clear configuration previews.
- Documented privilege boundaries.
- Recovery mechanisms for supported operations.
- Regular security maintenance when releases become available.

A minimal system is not automatically secure.

We will treat early builds as experimental and avoid claiming production-level security until appropriate testing has been completed.

---

## Project structure

A proposed repository layout:

```text
AceLinux/
├── README.md
├── assets/
│   └── acelinux.png
├── boot/
├── kernel/
├── init/
├── userspace/
├── system/
│   ├── configuration/
│   ├── services/
│   └── packages/
├── installer/
├── build/
├── tests/
└── docs/
    ├── ARCHITECTURE.md
    ├── BUILDING.md
    ├── INSTALLATION.md
    ├── CONFIGURATION.md
    ├── PACKAGES.md
    ├── ROADMAP.md
    └── TESTING.md
```

This is a proposed structure, not a claim that these directories or files already exist.

Generated images, temporary builds, and downloaded dependencies should be kept separate from tracked source files.

## Contributing

AceLinux is a team-driven project.

We welcome technical feedback, testing, documentation, code reviews, and contributions that help us improve the system.

We value:

- Understandable code
- Minimal unnecessary complexity
- Clear system interfaces
- Documented technical decisions
- Reproducible builds
- Meaningful tests
- Respect for the project's terminal-first philosophy

Major features should include documentation explaining their purpose, implementation, and impact on existing components.

## Related projects

**[AceNix](https://github.com/aeronwtf11/AceNix)** — Our NixOS management CLI, designed to make native NixOS administration easier.

**AceOS** — Our separate, long-term operating-system project focused on developing an independent kernel and its surrounding system.

**AceLinux** — Our Linux-kernel-based distribution, designed to become a minimal but usable general-purpose operating system.

AceLinux and AceOS may share architectural ideas and reusable utilities where appropriate, but they have different long-term goals.

## License

A license has not yet been finalized for AceLinux.

Until one is added, the repository should not be assumed to grant permission to modify or redistribute its source code.

---

<div align="center">

**AceLinux**

*Start minimal. Build your system.*

**One System. Your Decisions.**

<sub>The foundation is ours. The configuration is yours.</sub>

</div>
