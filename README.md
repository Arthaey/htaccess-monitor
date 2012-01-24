# What is htaccess-monitor?

One way that hackers can mess with your website is to modify your .htaccess
files without your knowledge. If you keep your .htaccess files under version
control\*, then this script can show you any local modifications to the files.

_\* Only Subversion is currently supported by this script. I know, I know. I'll
add Git support if someone asks. ;)_


# Example

## Local modifications present

    $ htaccess-monitor
    
    The following .htaccess files have been modified:
    
      - /home/arthaey/www/path/to/.htaccess
    
        Index: /home/arthaey/www/arthaey.com/trunk/.htaccess
        ===================================================================
        --- /home/arthaey/www/path/to/.htaccess   (revision 1929)
        +++ /home/arthaey/www/path/to/.htaccess   (working copy)
        @@ -1 +1,4 @@
        +
        +# local change you forgot to commit, or malicious hack?
        +Redirect 301 / http://evil.example.com

## Remove local modifications

    $ svn revert /home/arthaey/www/path/to/.htaccess

or

    $ svn commit /home/arthaey/www/path/to/.htaccess -m "totally safe change"

# No more local modifications

    $ htaccess-monitor
    
    The following .htaccess files have been modified:
      [none]

# Usage

_Tested in Ruby 1.8.7._

## Run manually

The script takes no options. Just run it from anywhere. It only requires that
`$HOME` is set.

## Via cron

Use cron to run htaccess-monitor every night. For example, run `crontab -e` and
include something like the following in your crontab file:

    MAILTO='youremail@example.com'
    0 0 * * * /path/to/htaccess-monitor


# TODO

 - only output "no modifications" if --verbose
 - support subdirectory other than ~/www
