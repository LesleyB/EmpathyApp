EmpathyApp
==========

Empathy App is a Wordpress plugin and is integrated into websites with the help of Wordpress shortcodes



#### Technology stack

* LAMP
* Wordpress

Also relies on these wp plugins:

* Neat skype status v2 (PRO) [link](http://neat-wordpress-plugins.mission.lt/neat-skype-status/)
* Posts 2 posts (p2p) [link](https://wordpress.org/plugins/posts-to-posts/)



#### User roles and naming standards

Internal name | Wordpress role | Username restrictions
------------- | -------------- | ---------------------
Empathizer    | contributor    | empathizer_{first-name}, is both wp username and also an existing skype name
Caller        | subscriber     | is both username and also an existing skype name
Administrator | administrator  | any valid wp login name



#### Remote sites

##### Demo

[link](http://kuanyin.ihavearrived.org/)

You may want to create an empathizer (contributor) account and a caller (subscriber) account so that you can test the "empathizer email" page and send emails

##### Dev





#### Website overview

The website using EmpathyApp needs to have five pages with different shortcodes. php code (and js, html) is inserted through shortcodes (we cannot load pages directly because of how Wordpress is built)

A graphical overview in two parts: [before call](https://cloud.githubusercontent.com/assets/10245688/5697024/e43f9c26-99e4-11e4-9060-9edaf79a66dd.jpg), [after call](https://cloud.githubusercontent.com/assets/10245688/5697023/e3815e96-99e4-11e4-94db-98df20afe3a4.jpg)


##### 1. Front page

* [Example](http://kuanyin.ihavearrived.org)
* Shortcode: [skype skypenames="skypename1, skypename2, ..."] Example: [skype skypenames="echo123, tord_dellsen, infinitytaal"]
* Plugin dependencies: Neat skype status v2 (pro) *please note that "pro" version is required*
* How it works: Clicking the icon will call one of the people in the list of skype names
* Used by: Caller


##### 2. Page with form for sending email with donation link

* Empathizer perspective: Form for filling in the user name of caller from just finished call and the length of the call, after submitting the form an email will be sent to the caller
* Dev perspective: The actual sending of the email is done on the next page below
* [Example](http://kuanyin.ihavearrived.org/email_form/)
* Shortcode: [ea_email_form]
* How it works: While logged in as an empathizer (currently using the administrator role), entering a user name for a caller (currently using the subscriber role) and number of minutes for preceding call and pressing button will send an email to the caller with a link to the donation form
* Used by: Empathizer
* File: pages/email-form_sc.php


##### 3. Page with confirmation that email has been sent

* Empathizer perspective: Verification that the email has been sent to the caller
* Dev perspective: Sends email and also stores call record in the database
* [Example](http://kuanyin.ihavearrived.org/email_sent/)
* Shortcode: [ea_email_sent]
* Used by: Empathizer
* File: pages/email-sent_sc.php


##### 4. Page with donation form

* Caller perspective: Arrives at this page after clicking link received in an email (see previous step)
* [Example](http://kuanyin.ihavearrived.org/donation_form/)
* Shortcode: [ea_donation_form]
* For testing use 4242 4242 4242 4242 as the credit card number and anything for the other fields. We are using a test key so you can test all you want without any real money being transfered. To verify that the transfer was made you need access to the Empathy App stripe account but we also print the result and the amount transfered on the "thank you" page
* Used by: Caller
* File: pages/donation_form_sc.php


##### 5. Page with thank you and confirmation that email has been received

* Dev perspective: Makes the actual charge of the credit card
* [Example](http://kuanyin.ihavearrived.org/donation_sent/)
* Shortcode: [ea_donation_sent]
* Plugin dependencies: p2p wp plugin
* Used by: Caller
* File: pages/donation_sent_sc.php
