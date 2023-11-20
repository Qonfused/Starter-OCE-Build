<h1 align="center">Starter OCE-Build Template</h1>
<br>
<p align="center">
  A template <b>Hackintosh</b> project built on top of the <a href="https://github.com/acidanthera/OpenCorePkg">OpenCore</a> bootloader and <a href="https://github.com/Qonfused/OCE-Build">OCE-Build</a> build manager.
</p>

<div align="center">

  <a href="/LICENSE">![License](https://img.shields.io/badge/⚖_License-BSD_3_Clause-lightblue?labelColor=3f4551)</a>
  <a href="/docs/CHANGELOG.md">![SemVer](https://img.shields.io/badge/SemVer-v0.0.0-important?logo=SemVer&labelColor=3f4551)</a>
  <a href="https://github.com/acidanthera/OpenCorePkg/releases">![OpenCore](https://img.shields.io/badge/dynamic/yaml?label=OpenCore&logo=Osano&logoColor=0298e1&labelColor=3f4451&prefix=v&query=OpenCorePkg.version&url=https%3A%2F%2Fraw.githubusercontent.com%2FQonfused%2FStarter-OCE-Build%2Fmain%2Fsrc%2Fbuild.lock)</a>
  <a href="https://github.com/Qonfused/Starter-OCE-Build/actions/workflows/oce-build.yml">![OCE Build](https://github.com/Qonfused/Starter-OCE-Build/actions/workflows/oce-build.yml/badge.svg?branch=main)</a>

</div>

> [!NOTE]
> This template is for an archived version of OCE-Build pre-dating its v1.0.0 rewrite. An archived version of the project is available [here](https://github.com/Qonfused/OCE-Build/tree/v0-frozen).

## ⚡Quick Links

- [Getting Started](#-getting-started)
  - [1. Clone this repository using git](#1-clone-this-repository-using-git)
  - [2. Build this repository using OCE-Build](#2-build-this-repository-using-oce-build)
  - [3. Using this project with macOS](#3-using-this-project-with-macos)
- [License](#%EF%B8%8F-license)

## ✨ Getting Started
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Qonfused/Starter-OCE-Build)

### 1. Clone this repository using Git

To clone this repository locally with submodules, run the below commands:
```sh
git clone --recurse-submodules https://github.com/Qonfused/Starter-OCE-Build
cd Starter-OCE-Build
```

If you've cloned this project without resolving submodules, you'll need to initialize them:
```sh
git submodule init
git submodule update
```

> **Note**: Optionally, you can add git aliases to always resolve submodules:
> ```sh
> git config --global alias.clone-all 'clone --recurse-submodules'
> git config --global alias.pull-all 'pull --recurse-submodules'
> ```

### 2. Build this repository using OCE-Build
> **Note** **OCE-Build** must be run in a Linux or macOS environment.
> 
> For Windows users, refer to [aka.ms/wslinstall](aka.ms/wslinstall) and [aka.ms/wsl2](aka.ms/wsl2) for instructions on installing wsl and upgrading to the wsl2 kernel (recommended).
> - You can install a Linux distribution directly from the Microsoft Store (e.g. [Ubuntu 20.04.5 LTS](https://apps.microsoft.com/store/detail/ubuntu-20045-lts/9MTTCL66CPXJ)).
> - Alternatively, you can [setup devcontainers](https://code.visualstudio.com/docs/devcontainers/containers#_installation) with Docker and VSCode to run a containerized Linux environment on top of wsl. The [devcontainer](/.devcontainer/devcontainer.json) for this project will setup and build the project automatically upon container creation.
>
> For Linux users (or wsl), ensure you have the following commands available:
> - **cURL**
>   - Check with `curl --version`
>   - Install with `sudo apt install curl`
> - **bsdtar**
>   - Check with `bsdtar --version`
>   - Install with `sudo apt install libarchive-tools`
> - **iasl**
>   - Check with `iasl -v`
>   - Install with `sudo apt install acpica-tools`

To build your project's EFI, run the below command at the root of the project:
```sh
# Run oce-build pipeline
bash scripts/build.sh
```

You can run a validation script to check the EFI build output with:
```sh
# Verify build output
bash scripts/lib/oce-build/scripts/validate-efi.sh -c src/config.yml
```

### 3. Using this project with macOS
> **Note** To enable **iServices** functionality, please refer to the notice in
> the build-generated **.serialdata** file under the **src/** directory for instructions on validating your
> serial number. This is automatically generated each time you run a new build using the build script as long as no existing **.serialdata** file exists. Remember that you can re-generate this data by running `bash scripts/lib/oce-build/scripts/patch-serial.sh -c src/config.yml` or by removing **.serialdata** and re-running the build script.
>
> You can optionally instead download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) follow the [iServices guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-gensmbios) to generate new SMBIOS data for your machine to be applied before running the build script. You'll then need to store your SMBIOS data in a new **.serialdata** file:
> ```yaml
> MLB:                String | "M0000000000000001"
> ROM:                Data   | <112233445566>
> SystemProductName:  String | "iMac19,1"
> SystemSerialNumber: String | "W00000000001"
> SystemUUID:         String | "00000000-0000-0000-0000-000000000000"
> ```

## ⚖️ License
[BSD 3-Clause License](/LICENSE).
