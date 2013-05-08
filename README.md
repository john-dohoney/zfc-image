zfc-image
=========

How to use Image Captcha with ZFCUser

Assumption:  You have copied zfcuser into your ZF2 project and are not happy with the figlet captcha.  There are a lot of free
commercial fonts, like www.fontsquirrel.com as one example.  You should also take a peek at the documentation located
at http://framework.zend.com/manual/2.1/en/modules/zend.captcha.adapters.html#zend-captcha-image .  This will give you
an idea of the options for the captcha constructor (remove the "set" or "get").

1. Be sure to copy your zfcuser.global.php to you /config/autoload directory
2. Find a nice font, download it
3. Create 2 folders under your /public directory, /public/font and /public/captcha, in your ZF2 project
4. Make sure you adjust permissions (typically www-data user) to be able to write to /public/captcha directory on your server
5. Import the image file, in my case, Base5.ttf (I renamed this to remove spaces) from your download directory into your ZF2 project
6. Now edit your zfcuser.global.php
7. Next enable captcha by setting: 'use_registration_form_captcha' => true,
8. Next I commented out:
<pre>
         'form_captcha_options' => array(
                'class'   => 'figlet',
                'options' => array(
                        'wordLen'    => 5,
                        'expiration' => 300,
                        'timeout'    => 300,
                ),
        ),
</pre>

Replaced it with:
<pre>
'form_captcha_options' => array(
        'class'   => 'image',
        'options' => array(
                'wordLen'    => 5,
                'expiration' => 300,
                'timeout'    => 300,
                'font' => '/usr/local/zend/apache2/htdocs/foo/public/font/Base5.ttf',
                'imgDir' => '/usr/local/zend/apache2/htdocs/foo/public/captcha/',
                'imgUrl' => 'http://foo.local:10088/captcha/',
                'DotNoiseLevel' => '80',
                'LineNoiseLevel' => '3',
        ),
),
</pre>
9. You will have to adjust the directories to your environment.  Also, experiment with Noise Level settings, these values worked
pretty good for me.
10. I did not make any code changes to the Module.php or the Module config.  This is only used on the registration page.

I personally like the image CAPTCHA to the RECAPTCHA, and the ZF Commons team did a great job with the module.

This is it.

Good Luck
John
