# PHP-SIGNED

## Abstract

This is a proposal for PHP extension to disable running unapproved PHP code, uploaded using security holes or by any other means.

## Components

1. Master key is saved in php.ini (hidden in phpinfo)
2. Signatures are saved in a file that lives in web or app root folder, 1 line per file/signature
3. Easy tool to (re)generate signatures file for current folder with subfolders (current trusted state).
4. (optional) Allow stripping whitespace from php files for the convenience of upload NL/LF and IDE space/tab reformatting, without need to regenerate signatures. (can be problematic for files with `__halt_compiler();`)

## Example

### php.ini 

    extension = phpsigned.so

    [PHP-Signed]

    phpsigned.enable = 1
    phpsigned.block_not_signed = 1
    phpsigned.master_key = kUCCS3vk4wVzC6IEqYK9nMGcLhfIqUi5
    phpsigned.strip_whitespace = 0

### /var/www/html/.php-signed

    index.php QGCWxkXjV3JmwW4huTQs8XS7FGjXhIAy
    app/code/example.php  ly1EU3UzT8657S8PFoaqO49NBUL6iKpR
    var/config/db.php TUNH3oqjPg1X2B2DssFoz4Cbto8bLiM4

### Signature generation tool

Ideally an option in php executable, like this:

    $ php --generate-signatures [-o .phpsigned] [-d /var/www/html]