# Suhosin

Suhosin (pronounced 'su-ho-shin') is an advanced protection system for PHP installations. It was designed to protect servers and users from known and unknown flaws in PHP applications and the PHP core.

## About this fork

This repository is an unofficial community-maintained fork of the Suhosin PHP extension. It carries compatibility changes and bug fixes in its source tree. No separate compatibility patch needs to be applied before building this checkout.

Report problems specific to this fork in the [issue tracker](https://github.com/NewEraCracker/suhosin/issues). Where practical, check whether the same problem occurs in the corresponding upstream version. If it occurs only in this fork, report it here rather than to the upstream project. Include the revision, PHP version, platform, and steps needed to reproduce the problem.

## Security Advisory

**CVE-2026-109618** and **CVE-2026-109619** identify two critical remote code execution vulnerabilities in **PHP**. Upload processing and session upload-progress handling are among the relevant attack paths, but they do not fully describe both vulnerabilities.

**Suhosin does not completely mitigate these vulnerabilities**.

To reduce the attack surface regarding `php_rfc1867_callback` in `ufilter.c`, this project has implemented the following mitigation:

- The `SUHOSIN_FORWARD_RFC1867_CALLBACK` directive has been set to `0`. This disables external callback forwarding while preserving Suhosin's internal multipart filters and cleanup mechanisms.

To remediate the problem, the following companion solution is recommended:

- **[php_uploadprogress_guard](https://github.com/HOSTED-POWER/php_uploadprogress_guard)** - a hardened extension that provides additional protection for upload-progress tracking and reduces exposure to related attack vectors.

## Compatibility and version

The source currently identifies itself as **Suhosin 0.9.39dev2** in [php_suhosin.h](php_suhosin.h). This is a development version; obtaining `master` does not establish release readiness.

The repository's [Travis configuration](.travis.yml) lists PHP **5.4, 5.5, and 5.6** on Linux. This records the configured test targets, not a claim that current builds or tests have passed. The [changelog](Changelog) records removal of support for PHP versions earlier than 5.4.

## Requirements
Suhosin works on Linux, Windows, or any other platform where PHP is supported.

- **PHP**: PHP 5.4 or newer is required.
  - For PHP 5.5 specifically, Suhosin requires PHP 5.5.4 or higher.

- **PHP 7 or later is not supported.** The historical wording "newer version" does not imply unrestricted compatibility with any future PHP versions.

- **Platforms**: The original README stated that Suhosin works on Linux, Windows, or any other platform supported by PHP. Both Unix and Windows build configuration files are present, but a current platform support matrix has not been verified.

- **Binary Compatibility**: The original README claimed that the extension is binary-compatible with normal PHP installations and third-party binary extensions (e.g., ZendOptimizer). This historical compatibility claim has not been verified for this revision or for specific third-party extension versions.

## Building and installing on Linux

### Step 0: Obtain the source

Get the source from this repository's `master` branch:

```sh
git clone --branch master --single-branch https://github.com/NewEraCracker/suhosin.git
cd suhosin
```

This replaces the old `suhosin-0.9.37.1.tar.gz` download and unpacking instructions. The compatibility changes are already integrated; there is no separate patching step.

### Step 1: Compile

Set `PHP_PREFIX` to the installation prefix of the PHP version you intend to build against, such as `/usr` or `/usr/local`. Use that installation's `phpize` and `php-config`:

```sh
export PHP_PREFIX="/usr"
"$PHP_PREFIX/bin/phpize"
./configure \
  --enable-suhosin=shared \
  --with-php-config="$PHP_PREFIX/bin/php-config"
```

To avoid potential runtime defects caused by stale build artifacts (e.g., partial builds mixing old and new header layouts), it is highly recommended to use a fresh source tree and clean the build directory before compiling:

```sh
make clean
make
```

This addresses potential issues where partial builds may retain old initializer/INI handlers against updated headers. A fresh build ensures all components are rebuilt consistently.

The extension's configure options are defined in [config.m4](config.m4). These instructions describe the existing Unix build procedure. Windows has a separate [build configuration](config.w32); a current Windows toolchain and installation procedure are not documented here because they have not been verified.

### Step 2: Install

```sh
make install
```

Run this with permission to write to the target PHP installation's extension directory.

### Step 3: Configure

Suhosin loads as a PHP extension. Use the supplied [suhosin.ini](suhosin.ini) as the configuration template and review its settings for your installation.

- If the target PHP installation scans an additional configuration directory, copy `suhosin.ini` there. `/etc/php.d` is one possible location; use it only if that PHP installation actually scans it.
- Otherwise, add the relevant settings to the target installation's `php.ini`. The original README used `/etc/php.ini` as an example; the actual path depends on the installation.

For the shared Unix build above, enable the following line, which is commented out in the supplied template:

```ini
extension=suhosin.so
```

Use the configuration for the PHP instance serving your application. A command-line PHP installation may use different configuration files from the web server's PHP installation.

## Historical project references

The original README points to the following upstream resources. They are retained for reference; their current availability and maintenance status have not been verified:

- [Original Suhosin website](http://www.hardened-php.net/suhosin/)
- [Original upstream source reference](https://github.com/sektioneins/suhosin)

For this fork, obtain the source using the `master` instructions above.

## License and credits

Suhosin is distributed under the **PHP License, version 3.01**, included in [LICENSE](LICENSE). The license is also referenced by the original README at [php.net/license/3_01.txt](http://www.php.net/license/3_01.txt).

For code covered by that license, its section 5 permits recipients to continue to use the code under version 3.01 or choose a subsequent version published by the PHP Group, including version 4. This statement does not change the terms of files carrying separate license notices.

The PHP License, version 4, is the Modified BSD License (SPDX-License-Identifier: BSD-3-Clause). These are alternative terms; a recipient may choose either one.

```
Copyright © The PHP Group and Contributors.
Copyright © Zend Technologies Ltd., a subsidiary company of Perforce Software, Inc.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

The original README credits:

- Copyright © 2006-2007 The Hardened-PHP Project
- Copyright © 2007-2015 SektionEins GmbH
- Author: Stefan Esser <sesser@sektioneins.de>

For third-party components incorporated into this fork, please refer to the [THIRD-PARTY-NOTICES](THIRD-PARTY-NOTICES) file.

See [CREDITS](CREDITS) for additional project credits. If the bundled license is missing and the online copy is unavailable, the original license notice directs requests to <license@php.net>.
