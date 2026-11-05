<div align="center">

<img src="assets/aceos.png" width="155" alt="AceOS Logo">

# AceOS

**A minimal operating system. Your system, your decisions.**

`x86-64` · `C` · `OS Development` · `Terminal First`

**One System. Our Decisions.**

---

</div>

## Overview

AceOS is an experimental, general-purpose operating system project built around a simple idea:

**An operating system should provide the foundation. The user should decide what comes next.**

Instead of shipping a fully configured desktop environment, dozens of applications, and unnecessary background services, AceOS aims to provide a minimal, functional system that users can configure according to their own needs.

Our default environment is a terminal.

From there, users can configure networking, install packages, manage services, enable a desktop environment, and customize their system using AceOS's own management tools.

We want to make system administration understandable without sacrificing the flexibility and control expected from a low-level operating system.

AceOS is primarily designed for ordinary x86-64 desktop and laptop computers.

Our initial development may use the Linux kernel as a foundation while we develop our own userspace, initialization system, and configuration tools. Our long-term objective is to develop an independent kernel.

**AceOS is currently in early development and is not intended for production use.**

## Project status

**Development stage: Pre-alpha**

Our first major objective is to build a minimal, bootable x86-64 system that reaches a working terminal and provides the foundation for further configuration.

| Component | Status |
|---|---|
| System architecture | Planning and design |
| x86-64 support | Initial target |
| UEFI boot | Planned |
| Linux-based development foundation | Planned |
| AceIt init system | Planned |
| Terminal-first userspace | Planned |
| Configuration system | Design phase |
| Package manager | Planned |
| User management | Planned |
| Networking | Planned |
| Optional desktop environment | Future |
| Independent kernel | Long-term |

These statuses represent current development goals, not verified completed functionality.

---

## Downloads & testing

### Development builds

**No public AceOS builds are available yet.**

AceOS is still in early development. We have not published an official ISO, disk image, or installable release.

Once the first bootable builds are ready, this section will provide downloads and instructions for testing them.

| Build | Architecture | Format | Availability |
|---|---|---|---|
| AceOS Development Preview | x86-64 | ISO / disk image (TBD) | Not available |
| AceOS Testing | x86-64 | TBD | Not available |
| AceOS Stable | x86-64 | TBD | Not available |

### Planned testing options

We intend to support testing AceOS in virtual machines before recommending installation on physical hardware.

Our initial testing targets include:

- QEMU
- Other compatible x86-64 virtual machines
- Selected physical desktop and laptop computers

Future downloadable builds will include, where applicable:

- Version and build information
- Supported architectures
- Image checksums
- Boot and installation instructions
- Known issues
- Testing and bug-reporting instructions

**Important:** Early AceOS builds should only be used in disposable virtual machines or on dedicated test hardware. They are not intended to replace an existing daily-driver operating system.

We will update this section when the first verified test image is available.

---

## Philosophy

AceOS is built around a few principles that guide both development and the user experience.

### 1. Minimal by default

AceOS should install only what is necessary to provide a functional operating system.

No mandatory graphical interface. No unnecessary applications. No desktop environment selected on behalf of the user.

Our intended default installation provides:

- A bootable operating system
- A working terminal and shell
- Essential system utilities
- AceIt and required base services
- Basic user and permission management
- AceOS configuration tools
- The foundation for installing additional software

Everything else should be optional wherever practical.

**We provide the foundation. You build your environment.**

### 2. Terminal first, desktop optional

The terminal is the primary interface of AceOS.

It should be possible to configure and operate the system without installing a graphical environment.

Users who prefer a desktop can install and enable one later.

Users who prefer a terminal-only machine should never be required to install graphical components.

We intend to support both approaches without turning either into a separate operating system.

### 3. User control

We believe the user should decide how their system behaves.

AceOS should avoid enabling unnecessary services or installing software without an explicit reason.

Users should be able to configure:

- System identity and hostname
- Networking
- Installed packages
- Enabled services
- User accounts
- Desktop environments
- System behavior and preferences

Our management tools should make these operations accessible while keeping advanced configuration available.

### 4. Declarative configuration, simple commands

We want to combine a central configuration file with straightforward terminal commands.

A user should not need to manually edit several unrelated files just to perform a common configuration task.

For example:

```sh
aceos setr network:true
aceos preview
aceos apply
```

The intended behavior is to validate the requested configuration, show what will change, and apply it through the appropriate system components.

This is a planned interface, not an implemented feature.

### 5. One coherent system

AceOS should be developed as a coherent operating system.

Our init system, configuration engine, package manager, and system utilities should work together rather than behave like unrelated tools.

Components should remain modular and maintainable, but their interfaces should be consistent.

### 6. Privacy by default

AceOS is intended to operate without telemetry, tracking, or unnecessary network communication.

Network-dependent functionality should be explicitly configured by the user whenever practical.

### 7. Reliability and recovery

Configuration changes should be validated before application.

We aim to provide clear error messages, backups, and recovery mechanisms for supported system changes.

Updates and rollback operations should be explicit. We do not intend to remove saved generations automatically.

---

## Default user experience

Our intended first-boot experience is straightforward.

After installation and initial account setup, AceOS boots into a terminal.

An illustrative future session might look like this:

```text
AceOS
----------------------------------------

ace-pc login: aaron
Password:

Welcome to AceOS.

System:      AceOS
Interface:   Terminal
Desktop:     Not enabled
Network:     Not configured

aaron@ace-pc ~ $
```

This is a **design example**, not a screenshot or output from a working build.

From the terminal, the user would configure the system according to their preferences.

For example:

```sh
aceos status

aceos setr hostname:ace-pc
aceos setr network:true

aceos install git vim

aceos preview
aceos apply
```

Users who want a graphical environment could enable one later through supported packages and system rules.

Those who do not want one can continue using AceOS entirely from the terminal.

---

## System architecture

AceOS is planned around a minimal base system and optional components.

```text
                       AceOS
                         |
                    UEFI / Boot
                         |
                       Kernel
                         |
                       AceIt
                    Init System
                         |
                 Essential Services
                         |
                    Base Userspace
                         |
                 Terminal / Shell
                         |
                 AceOS Management
                 /       |       \
           Rules      Packages   Services
                 \       |       /
                  System State
                         |
                Optional Components
                  /           \
              Networking     Desktop
                (user configured)
```

The terminal and base userspace form the primary environment.

Additional components are installed or activated according to the user's configuration.

### Kernel

The kernel provides process execution, memory management, scheduling, hardware interfaces, and other fundamental operating-system functionality.

During early development, we may use the Linux kernel to establish a functional userspace and test our system-management architecture.

Our long-term goal is an independently developed kernel.

We intend to design AceOS-specific userspace interfaces with future portability in mind, without promising immediate compatibility with an unfinished kernel.

### AceIt — our init system

**AceIt is our custom initialization and service-management system.**

AceIt is intended to initialize essential operating-system components and manage system services after the kernel starts.

Planned responsibilities include:

- System initialization
- Service startup and shutdown
- Service dependency handling
- Service state tracking
- Startup diagnostics
- Controlled restarts
- Orderly system shutdown and reboot

Our intended command interface includes:

```sh
aceit status
aceit list

aceit start networking
aceit stop networking
aceit restart networking

aceit enable networking
aceit disable networking
```

AceIt should only start services that the base system requires or that the user explicitly enables.

We want AceIt to be lightweight, understandable, and suitable for a minimal terminal-based operating system.

The interface above is planned and has not yet been implemented.

### Userspace

The initial userspace will provide the tools necessary to interact with and configure AceOS.

We intend to include only essential utilities initially.

Planned components include:

- Bash
- GNU Coreutils
- Basic filesystem utilities
- User and permission tools
- System information and diagnostics
- AceOS command-line tools
- Essential service-management utilities

BusyBox may be used in boot or recovery environments.

Additional user-facing software will be installed through the package manager when that functionality becomes available.

---

## Configuration system

AceOS is designed around a central rule-based configuration system.

Our proposed configuration file:

```text
/etc/ace/config.sys
```

Example:

```ini
[system]
hostname:ace-pc
network:false
bluetooth:false
desktop:false

[services]
ssh:false

[packages]
pkg.git:true
pkg.vim:true
```

This example represents a minimal system with no graphical environment and no optional networking services enabled.

We intend to support a consistent CLI:

```sh
aceos status
aceos get hostname

aceos setr hostname:ace-pc
aceos setr network:true

aceos preview
aceos apply
```

### Configuration workflow

1. Read the current configuration.
2. Parse and validate the requested changes.
3. Identify affected system components.
4. Present a readable preview.
5. Apply supported changes.
6. Record the resulting system state.
7. Report errors and provide recovery information if necessary.

### Rule validation

The configuration system should reject:

- Unknown configuration rules
- Invalid values
- Conflicting settings
- Unsupported operations
- Changes that cannot be safely applied

We intend to reuse lessons learned from AceNix while developing an independent backend suited to AceOS.

The configuration system will communicate with AceIt for service-related operations.

---

## Package management

AceOS is planned to include its own binary package manager.

A minimal base installation should not require users to manually compile every application they want to use.

Our planned commands include:

```sh
aceos search firefox
aceos install firefox
aceos remove firefox
aceos update
```

Planned capabilities:

- Package search
- Package installation and removal
- Dependency resolution
- Package metadata
- Integrity verification
- Explicit upgrades
- Version tracking
- Recovery and rollback support

The package manager is not yet implemented.

During early development, we may use packages assembled by established build tools while developing the custom package-management system.

---

## Optional desktop environments

**AceOS does not install a desktop environment by default.**

Graphical environments are optional system components.

Our long-term goals include supporting existing desktop environments where technically feasible and developing our own AceOS desktop environment.

The intended workflow is:

1. Install the required graphical packages.
2. Select a desktop environment.
3. Enable the associated system services.
4. Preview the configuration.
5. Apply the changes.

The system should remain fully usable in terminal mode if the user does not enable a desktop.

We do not intend to make graphical components mandatory dependencies of the core operating system.

---

## Filesystem layout

Our initial design follows familiar Unix conventions while keeping AceOS-specific configuration and state separate.

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
│   └── bin/
└── var/
    ├── lib/
    │   └── ace/
    └── log/
```

The planned initial root filesystem is ext4.

The final filesystem layout will be documented as implementation progresses.

---

## Target platforms

AceOS is intended for general-purpose computers.

| Platform | Priority |
|---|---|
| x86-64 desktops | Primary |
| x86-64 laptops | Primary |
| UEFI systems | Initial boot target |
| QEMU virtual machines | Initial testing |
| Legacy BIOS | Possible future support |
| ARM64 computers | Possible future port |

Our first development and testing efforts focus on x86-64 virtual machines before expanding hardware compatibility.

Support for a specific device will be documented only after successful testing.

---

## Building AceOS

### Development environment

Our intended development toolchain includes:

| Tool | Purpose |
|---|---|
| GCC / Clang | Compilation |
| GNU Make | Build automation |
| Git | Version control |
| QEMU | System testing |
| GDB | Debugging |
| GNU Binutils | Low-level tools |
| Buildroot | Possible initial Linux system construction |

Development will primarily take place on Linux.

### Build workflow

```text
AceOS Source
     |
     v
Build Configuration
     |
     v
Compiler / Build Tools
     |
     v
Bootable Image
     |
     v
QEMU
     |
     v
Terminal Login
     |
     v
Functional Testing
```

We will publish exact build commands and required dependencies once our first reproducible build configuration has been committed and verified.

At present, there is no official AceOS build available for download.

---

## Development roadmap

Our roadmap reflects the order in which we intend to develop the system.

It is not a release schedule.

### Phase 1 — Minimal bootable system

- [ ] Establish the x86-64 build environment.
- [ ] Configure initial UEFI boot support.
- [ ] Produce a bootable system image.
- [ ] Boot successfully in QEMU.
- [ ] Establish a minimal userspace.
- [ ] Reach an interactive terminal.
- [ ] Document the first successful boot.

**Goal:** A minimal system that boots directly to a functional terminal.

### Phase 2 — AceIt

- [ ] Define the AceIt architecture.
- [ ] Implement system initialization.
- [ ] Create service definitions.
- [ ] Implement service start and stop operations.
- [ ] Implement service dependency handling.
- [ ] Add service status reporting.
- [ ] Implement shutdown and reboot support.
- [ ] Test failure handling.

**Goal:** Our own init system manages the minimal system reliably.

### Phase 3 — Base userspace

- [ ] Establish the filesystem layout.
- [ ] Integrate the selected shell and utilities.
- [ ] Implement initial user management.
- [ ] Add system diagnostics.
- [ ] Develop basic AceOS commands.
- [ ] Improve terminal usability.

**Goal:** A usable terminal-first operating system.

### Phase 4 — Configuration management

- [ ] Finalize `config.sys`.
- [ ] Implement the rule parser.
- [ ] Add typed value validation.
- [ ] Implement `aceos setr`.
- [ ] Implement preview and apply.
- [ ] Integrate service settings with AceIt.
- [ ] Add backup and recovery support.

**Goal:** Users can configure AceOS through its own management interface.

### Phase 5 — Networking and package management

- [ ] Implement configurable Ethernet networking.
- [ ] Integrate networking services with AceIt.
- [ ] Design the binary package format.
- [ ] Implement package installation and removal.
- [ ] Add dependency management.
- [ ] Implement package updates.
- [ ] Investigate system rollback mechanisms.

**Goal:** Users can add software and networking functionality to their minimal installation.

### Phase 6 — Optional graphical environment

- [ ] Establish graphical session support.
- [ ] Support selected desktop components.
- [ ] Develop AceOS-specific graphical tools.
- [ ] Research our custom desktop environment.
- [ ] Improve hardware compatibility.

**Goal:** Users can optionally turn their terminal-based AceOS installation into a desktop system.

### Long-term — Independent kernel

- [x] Research kernel bootstrapping.
- [x] Establish a freestanding C development environment.
- [ ] Implement initial kernel entry and diagnostics.
- [ ] Research memory management.
- [ ] Implement process management and scheduling.
- [ ] Design system calls.
- [ ] Develop essential hardware interfaces.
- [ ] Investigate userspace compatibility.
- [ ] Bring up AceOS userspace on our own kernel.

The custom-kernel effort is a long-term research and development objective.

---

## Testing and verification

We distinguish between code that compiles, an image that boots, and features that work correctly.

| Test | Purpose |
|---|---|
| Unit tests | Verify individual components |
| Integration tests | Verify subsystem interaction |
| Boot tests | Verify system startup |
| AceIt tests | Verify service management |
| Terminal tests | Verify the base user environment |
| Configuration tests | Verify parsing and application |
| Recovery tests | Verify failure handling |
| Hardware tests | Verify real-device compatibility |

Our initial development images will be tested in virtual machines.

We will document real hardware results separately and will not claim compatibility with untested devices.

---

## Security and privacy

AceOS is intended to use privacy-conscious defaults.

Our planned principles include:

- No telemetry.
- No unnecessary background network activity.
- Minimal services enabled by default.
- Explicit permissions and privilege boundaries.
- Configuration validation before application.
- Integrity checks for packages and updates.
- Clear error reporting.
- Recovery mechanisms for supported operations.

A minimal installation is not automatically a secure installation. We will evaluate security properties as the system develops.

Pre-alpha builds should be treated as experimental software and should not be trusted with important data.

---

## Project structure

Our proposed repository organization:

```text
AceOS/
├── README.md
├── assets/
│   └── aceos.png
├── boot/
├── kernel/
├── init/
│   └── aceit/
├── userspace/
├── system/
│   ├── configuration/
│   ├── services/
│   └── packages/
├── build/
├── tests/
└── docs/
    ├── ARCHITECTURE.md
    ├── BUILDING.md
    ├── ACEIT.md
    ├── CONFIGURATION.md
    ├── ROADMAP.md
    └── TESTING.md
```

This is a proposed structure and may change as implementation progresses.

Generated build artifacts should remain separate from tracked source code and build configurations.

## Contributing

AceOS is a team-driven project focused on understanding and developing operating-system components.

We welcome technical feedback, testing, documentation contributions, and code reviews.

Our development priorities are:

- Clear and understandable code
- Minimal unnecessary dependencies
- Well-defined component interfaces
- Reproducible development
- Documented decisions
- Incremental testing

Major changes should be accompanied by an explanation of their purpose, affected components, and testing requirements.

## Related projects

**[AceNix](https://github.com/aeronwtf11/AceNix)** — Our NixOS management CLI, developed to simplify declarative system administration.

**AceLinux** — Our separate Linux distribution project.

AceOS is our longer-term operating-system engineering project, with AceIt, a minimal terminal-first environment, configurable components, and an eventual independently developed kernel.

## License

Licensing has not yet been finalized.

Until a license is added, no permission to modify or redistribute the source should be assumed.

---

<div align="center">

**AceOS**

*Minimal by default. Configured by you.*

**One System. Our Decisions.**

<sub>We provide the foundation. You decide what runs on it.</sub>

</div>
