CodeIgniter-Postmark
=========================

I spent a bit of time making this library resemble the internal CodeIgniter libraries a little more.

Installation
------------

1.  Copy system/application/config/postmark.php to your application/config folder
2.  Copy system/application/libraries/Postmark.php to your application/libraries folder

Usage
------

### Config
	
There are six options that you can set in the config file (application/config/postmark.php)
Only api-key is required, which you get from your server instance on postmarkapp.com

The other five are optional. You can set a default 'From Name' and 'From Address'. This are setup in your postmarkapp.com sender signatures.

Setting 'validation' to TRUE will require that the to and from email addresses are, indeed, valid emails. A request will not be sent to 
postmarkapp.com if either of these are not a valid email address, saving bandwitdh.

Setting 'strip_html' to TRUE will simply remove all HTML tags from the non-HTML message that gets sent to your recipient. Some wild and crazy
formatting things will happen if you set this to TRUE, but the email will send, and not fail.

Setting 'develop' to TRUE will use the generic POSTMARK_API_TEST token to make sure that your configuration is correct. And email will _*not*_
be sent.

You can also pass an array of config options to the initialize(); function. 
	
	$config['api_key'] = '1234';
	$config['from_address'] = '1f@gogle.com';
	$config['from_name'] = 'Jarrod HJena3';
	
	$config['validation'] = TRUE;
	$config['strip_html'] = TRUE;
	$config['develop'] = FALSE;
	
	$this->postmark->initialize($config);

### Sending

    $this->load->library('postmark');
	// option, you can set these in config/postmark.php
    $this->postmark->from('from@example.com', 'From Name');

    $this->postmark->to('to@example.com', 'To Name');
    
    $this->postmark->cc('cc@example.com', 'Cc Name');
    
	$this->postmark->reply_to('us@us.com', 'Reply To');

    // optional
    $this->postmark->tag('Some Tag');

    $this->postmark->subject('Example subject');
    $this->postmark->message_plain('Testing...');
    $this->postmark->message_html('<html><strong>Testing...</strong></html>');

	// add attachments (optional)
	$this->postmark->attach(PATH TO FILE);
	$this->postmark->attach(PATH TO OTHER FILE);
	
	// send the email
    $this->postmark->send();
	
If using this in a loop, calling $this->postmark->to('to'); again will *replace* the original recipient, and calling $this->postmark->clear(); will set all fields to null. 
Postmark has now added the ability to send to multiple recipients. This is done by passing a comma separated string to $this->postmark->to();

$this->postmark->to('ex1@g.com, ex3@g.com');

ChangeLog
---------
1.3 - Added support for ReplyTo
1.4 - Attachments

Extra
-----

If you'd like to request changes, report bug fixes, or contact
the developer of this library, email <zack@inrpce.com>
