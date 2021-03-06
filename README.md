Laravel 5 VKontakte library
-------------------------
Library for working with API social network VKontakte

Installation
-------------
Add the following packages to your `composer.json`
```
"repositories": [
	{
      "url": "git@github.com:smskin/vkservice.git",
      "type": "git"
    }
]
...
"require": {
   "smskin/vkservice": "dev-master"
}
```
Next, run `composer update`

Next, add the following service providers to your `config/app.php`
```
'providers' => [
	...
	'SMSkin\VKService\ServiceProviders\VKServiceProvider'
]
```
Next, run `php artisan vendor:publish`
This creates a config file `app/config/vksettings.php`

Configuration
-------------

 - accessToken
	1. To work, you must create Standalone application VKontakte at http://vk.com/editapp?act=create. After creating you get Application ID.
	2. It is necessary to go to the address for access_token (appears in the address bar).
	Access_token needs to work with a closed part of Api VK.
	http://oauth.vk.com/authorize?client_id=[ApplicationID]&scope=wall,offline&redirect_uri=http://oauth.vk.com/blank.html&response_type=token
	3.  Copy access_token from the address bar.
 - userId - Social network user ID
 - groupId - Social network group ID
 - exportMessage - Export recording, if the user has configured the appropriate option.
 - exportServices - An array of social networks in which to export the recording. When the function is activated exportMessage
    
Working with the wall
-------------
An example of sending a message on the wall
```
$post = new WallPost();
$post->setMessageText('Test message');
$post->setAttachUrl('http://vk.com');
$post->setToGroup(true); //Send a message on the wall of the group
$post->save();
```
Example of editing posts
```
$post = new WallEdit();
$post->setMessageId(1);
$post->setMessageText('New message text');
$post->setAttachUrl('http://google.com');
$post->setToGroup(true);
$post->save();
```