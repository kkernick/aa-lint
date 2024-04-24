## AA-Lint

Lint AppArmor Profiles

**WARNING! `aa-lint` can make errors. Make backups of your profiles!**

## Installation

On Arch-Based Distributions, download the PKGBUILD and run `makepkg -si`

For others, ensure that `python` `python-termcolor` are installed, and `chmod +x` the script. 

## Usage

`aa-lint` doesn't touch the system AppArmor directory at `/etc/apparmor.d`, it instead uses a copy which you'll need to create at `$XDG_DATA_HOME/apparmor.d`. Simply copy pasting and setting appropriate permissions will suffice. 

`aa-lint` runs without user interaction, and performs numerous linting stages on the profiles:

1. Replaces hard-coded paths, such as `/home/*/` into defined AppArmor variables, like `@{HOME}`
2. Combines rules pointing to the same file. For example, `/usr/bin/bash r` and `/usr/bin/bash ix`, will be combined into a single rule `/usr/bin/bash rix`
3. Find invalid profiles. If a profile permits execution of another binary using the `Px` or `Cx` modifiers, but that binary is not found to have its own profile or child profile, AppArmor will silently deny these executions. `aa-lint` will warn the user, so that they can either change the permission or add the profile.
4. Remove redundant rules. If a rule is contained within another rule (Such as `/** r`  and `/usr/bin/bash r`), which can either be from the current profile or any included abstractions, it will be removed.