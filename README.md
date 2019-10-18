
# PHPinstaller for VestaCP

The script for the compilation of the source code of multiple versions of php in separate directories. For Debian/Ubuntu.

### Installation

Clone the repository into any directory on your server

```bash
git clone https://github.com/IvanMiroshin/PHPinstaller.git
```

### Usage

```bash
bash phpinstaller
```

**What the script does:**

At startup, it asks what php versions you want to build (the version needs to be entered completely. For example, 7.1.2, 
not 7.1. You can enter several versions with a space), whether to create a symlink on the php-cgi binary in `/usr/bin` 
for quick access.

At the first start, it asks whether to add dependencies. If you refuse to install dependencies, then you need to 
install them yourself. Otherwise, you will get errors during assembly. Subsequent launches skip this step. You need to 
understand that the script is trying to put all the possible dependencies, but different distributions may use different 
packages or when using custom compilation flags, you may need to install something.

Parses http://php.net/downloads.php for the presence of a bz2 archive with the source code of the php version specified 
by the user. If it finds, downloads and unpacks the sources in `/opt/php/src`.

You can also put archives with sources in `/opt/php/src/bzips`, then the script will not download them.

Sets default configurations.
You can use your own configurations: `/opt/php/options`. If the script finds this file, then it uses it to configure. 
The script replaces version in the configuration file with the current build version. This is done so that the script 
automatically creates its own directory for each version. If you build for example version `5.3.29` and `prefix = /opt/php/php-version` 
is specified in your configuration file, then this is equal to `prefix = /opt/php/php-5.3.29`. When building multiple 
versions at the same time, you need to use this so that you do not collect all versions into one directory.

If necessary, creates a symlink and template for the VestaCP. If it creates templates for the VestaCP, it checks if the
cgi module is enabled in Apache. If the module is enabled, turns it on.

**Author and source:**

Peter Anikin <br>
https://anikin.pw/all/menedzher-versiy-php/

