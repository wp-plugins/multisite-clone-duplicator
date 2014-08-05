=== MultiSite Clone Duplicator ===
Contributors: GLOBALIS media systems
Tags: duplicate, clone, copy, duplication, duplicator, factory, multisite, site, blog, network, wpmu, new blog
Requires at least: 3.5.0
Tested up to: 3.9.1
Stable tag: 0.2.0
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Clones an existing site into a new one in a multisite installation : copies all posts, settings and files

== Description ==

MultiSite Clone Duplicator adds a "Duplicate Site" functionality to your network installation.  

It allows you to clone any site of your network into a new one : all data, files, users and roles can be copied.  

It is useful when you want to create multiple sites from the same template : waste your time copying the same configuration again and again !  
  
Simple and user-friendly, this plugin extends WordPress core network's functionalities without polluting the dashboard.  

= Features: =
* Clones any site of your wordpress multisite installation
* Copies all posts and settings
* Generates log files (if option is checked)
* Copy all files from duplicated site (if option is checked)
* Keep users and roles from duplicated site (if option is checked)
* Configure which site is clonable (so you can define an unique "pattern" site)
* Fully hookable

== Installation ==

You can install MultiSite Clone Duplicator using the built in WordPress plugin installer. It’s easy, 2 seconds.

If you prefer download MultiSite Clone Duplicator manually :

1. Upload multisite-clone-duplicator/ to the `/wp-content/plugins/` directory
2. Activate the plugin through the 'Plugins' menu in WordPress
3. (Optional) Chmod 777 the logs/ directory of the plugin, if you want to activate logs
4. Go to My Sites > Network Admin > Duplication and enjoy !

In the future, you'll probably want to create a dedicated "template" blog to clone from.

== Frequently Asked Questions ==

= How does it work ? =
* It creates a new user if the email was not an existing email
* It creates a new blog with appropriate title and admin user
* It copies all tables from cloned site, but keep some options (like title, domain, etc) of the new blog
* It searches and replaces old site's URL and DOMAINS with the new ones
* It copies upload directory from the old site to the upload directory of the new one (if option is checked)
* It imports users and roles from the old site to the new one (if option is checked)

= Does it support subdirectory AND subdomain installations ? = 
Yes, it supports both !

= Can I clone the primary site ? = 
Yes you can, but you want to be careful : WordPress saves network tables and primary blog tables with the same prefix, and some of their data are mixed. It forces us to restrict primary blog cloning to copy only the default wp tables. If you want to change this (for example, include your plugin tables in the cloning), use mucd_default_primary_tables_to_copy filter. In the future, you want probably not to copy again and again the primary blog : use a "template" blog dedicated to clonage instead.

= Does it clone plugins settings ? = 
Yes it does !

= But some data are serialized ? =
It's not a problem ! Serialized data are understood by the plugin, recursively unserialized, replaced with appropriate values, and serialized again.

= After cloning, new site was created, but it goes on 404 page, why ? =
Check your host / server configuration : you probably cloned your site into a domain that is not available !

= Which languages are currently supported? = 
As of now, MultiSite Clone Duplicator is available in English and in French. If you wish to, you can translate the interface in your own language in the [standard WordPress way](http://codex.wordpress.org/Translating_WordPress)

= GLOBALIS what ? =
[Globalis media systems](http://www.globalis-ms.com/) is a web IT consulting company based in Paris, and a pioneer of the PHP and LAMP platform. Since 1997, we have been designing, making and maintaining Internet, intranet or mobile software. We have been working with open source CMS since 2000 and have regularly been using WordPress since 2007.

== Screenshots ==

1. **Basic features**
2. **Advanced features**
3. **Settings**
4. **Successfull duplication**
5. **Log warning**

== Changelog ==

= 0.2.0 =
* First public version released by Pierre Dargham
* Generates logs
* Primary site is clonable
* Auto-suggest for admin email
* Keep users and roles from duplicated site
* Translating
* Hookable

= 0.1.0 =
* Initial version released by Julien Oger
* Copies all the posts, settings and files from a site to a new one
* Cannot clone primary site

== Upgrade Notice ==

= 0.2.0 =
Get advanded features and log functionnality !

== Hooks ==
  
---------------------------------------
= Action : mucd_before_copy_files / mucd_after_copy_files =
Action before / after copying files  
**Args :**

  1. Int : from_site_id
  2. Int : to_site_id
  
---------------------------------------
= Action : mucd_before_copy_data / mucd_after_copy_data =
Action before / after copying data  
**Args :**

  1. Int : from_site_id
  2. Int : to_site_id
  
---------------------------------------
= Action : mucd_before_copy_users / mucd_after_copy_users =
Action before / after copying users  
**Args :**

  1. Int : from_site_id
  2. Int : to_site_id
  
---------------------------------------
= Filter : mucd_copy_blog_data_saved_options =
Filter options that should be preserved in the new blog (original values from created blog will not be erased by copy of old site's tables)  
**Args :**

  1. Array of string : option_name
  
---------------------------------------
= Filter : mucd_default_fields_to_update =
Filter fields to scan for an update after data copy  
**Args :**

  1. Array of ( 'table_name' => array('field_1', 'field_2' ...));
  
---------------------------------------
= Filter : mucd_default_primary_tables_to_copy =
Filter tables to duplicate when duplicated site is primary site  
**Args :**

  1. Array of string table_name
  
---------------------------------------
= Filter : mucd_copy_dirs =
Filter directories and files you want to copy  
**Args :**

  1. Array of string : dirs
  2. Int : from_site_id
  3. Int : to_site_id
  
---------------------------------------
= Filter : mucd_string_to_replace =
Filter which strings we want to replace during update  
**Args :**

  1. String : string_to_replace
  2. Int : from_site_id
  3. Int : to_site_id
  
---------------------------------------
  
== Thank’s ==

The original version of this plugin has been developed by [Julien OGER](https://github.com/julienOG) who keeps following the project carefully.  

Some code for search and replace in SQL serialised data were initialy taken from [Lionel Pointet Wordpress Migration tool](https://github.com/lpointet/wordpress_migration)