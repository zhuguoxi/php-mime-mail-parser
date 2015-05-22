# Requirements #

PHP Mime Mail Parser requires [MailParse](http://pecl.php.net/package/mailparse) extension and PHP5+.


## MailParse ##

The MailParse extension is can be downloaded from here:
http://pecl.php.net/package/mailparse

It also depends on [mbstring](http://www.php.net/mbstring). Mbstring is available in PHP but not enabled by default. see: http://www.php.net/manual/en/mbstring.installation.php

To install mailparse you'll need the php-devel package.

You can install this through your package manager.
Example:
```
sudo apt-get install php5-devel 
```
or
```
yum install php5-devel
```
etc.

This will give you the commands that allow compiling PHP PECL extensions.

Then follow the directions on installing a PHP PECL extension through the pecl command.

http://php.net/manual/en/install.pecl.phpize.php

Basically you want to download the latest version of mailparse:

eg:

```
wget http://pecl.php.net/get/mailparse-2.1.5.tgz
```

2.1.5 is the latest stable as of this writing. You'll need the latest version from:
http://pecl.php.net/package/mailparse

Extract the archive:
```
tar -xzvf mailparse-2.1.5.tgz
```

change to the directory you just decompressed:
```
cd mailparse-2.1.5
```

Then build and install it through:

```
phpize
./configure
make
make install
```

Here is a good guide on installing PHP PECL extensions:
http://mattiasgeniar.be/2008/09/14/how-to-compile-and-install-php-extensions-from-source/

# Installation #

Once you have enabled MailParse support in your PHP build, you can download the latest source for the MimeMailParser Class from: http://code.google.com/p/php-mime-mail-parser/source/browse/trunk/MimeMailParser.class.php

# Usage #

Once you have the MimeMailParser class, include it in your PHP file. The documentation is in PHPDoc syntax. The doc explains what each method does.

Example code:

```
<?php

require_once('MimeMailParser.class.php');

$path = 'path/to/mail.txt';
$Parser = new MimeMailParser();
$Parser->setPath($path);

$to = $Parser->getHeader('to');
$from = $Parser->getHeader('from');
$subject = $Parser->getHeader('subject');
$text = $Parser->getMessageBody('text');
$html = $Parser->getMessageBody('html');
$attachments = $Parser->getAttachments();

?>
```

Retrieving Attachments Example :

```
$save_dir = '/path/to/save/attachments/';
foreach($attachments as $attachment) {
  // get the attachment name
  $filename = $attachment->filename;
  // write the file to the directory you want to save it in
  if ($fp = fopen($save_dir.$filename, 'w')) {
    while($bytes = $attachment->read()) {
      fwrite($fp, $bytes);
    }
    fclose($fp);
  }
}

```