===============================================================================

SUMMARY:

Suhosin is an advanced protection system for PHP installations. It was designed
to protect servers and users from known and unknown flaws in PHP applications
and the PHP core. Suhosin extension is binary compatible to normal PHP
installation, which means it is compatible to 3rd party binary extension like
ZendOptimizer.

Further information can be obtained from the official website:
http://www.hardened-php.net/suhosin/

If you wish to obtain the source code of the latest official Suhosin extension
you should look at https://github.com/stefanesser/suhosin

===============================================================================

DESCRIPTION:

This github repository aims to be an unofficial source for compatibility
patches for the Suhosin PHP extension.

Those patches are produced by community with the sole purpose of keeping the
project compatible with latest PHP versions and fix any bugs found.

If you've found any bug in the Suhosin extension after you apply one of our
patches, you should try to reproduce the bug in an unpatched instalation and,
if unable to reproduce, please don't bother the official project with the issue
and just report the bug to this unofficial project.

===============================================================================

REQUIREMENTS:

* Linux, Windows or any other platform where PHP is supported.
* PHP 5.1 or a newer version.

(PHP 5.1 is supported by using the patch meant for PHP 5.2)
(If you are using PHP 5.5, only PHP 5.5.4 or higher is supported)

===============================================================================

INSTRUCTIONS:

After downloading the source code of the Suhosin extension you can apply the
patch that matches your PHP version in order to make the Suhosin extension
compatible with your current PHP version.

Then you can install it via adequate install procedure for your platform.

(I will fill this section later with further details if required.)

===============================================================================

LICENSE:

/*
  +----------------------------------------------------------------------+
  | Suhosin Version 1                                                    |
  +----------------------------------------------------------------------+
  | Copyright (c) 2006-2007 The Hardened-PHP Project                     |
  | Copyright (c) 2007-2014 SektionEins GmbH                             |
  +----------------------------------------------------------------------+
  | This source file is subject to version 3.01 of the PHP license,      |
  | that is bundled with this package in the file LICENSE, and is        |
  | available through the world-wide-web at the following url:           |
  | http://www.php.net/license/3_01.txt                                  |
  | If you did not receive a copy of the PHP license and are unable to   |
  | obtain it through the world-wide-web, please send a note to          |
  | license@php.net so we can mail you a copy immediately.               |
  +----------------------------------------------------------------------+
  | Author: Stefan Esser <sesser@sektioneins.de>                         |
  +----------------------------------------------------------------------+
*/