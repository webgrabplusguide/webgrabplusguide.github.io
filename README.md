## Welcome to my basic guide on how to use WebGrab+Plus

### Disclaimer
Before we begin please note I'm in no way affiliated with WebGrab+Plus or its team. I make no money etc from referrals and any questions, support or anything relating to the product should be directed through the offical WebGrab+Plus website. <br>
This guides assumes you are using Windows. Although Linux should be the same, the paths to directories will be different.

### Buy me a coffee
If this guide has helped you and you'd like to donate or buy me a coffee you can do so here
https://www.buymeacoffee.com/sparklesunshine

### Download & install WebGrab+Plus
Go to <a href="http://www.webgrabplus.com">http://www.webgrabplus.com</a> and download the latest version of WebGrab+Plus. Note that there maybe a beta version in the news and updates section on the main page which is newer than the current stable version. Read the notes to see any changes. <br>
Install the software and the siteini pack. If you choose not to download the siteini pack you can download it later or manually download it from the website. This is also the case if you wish to update the pack at a later date. The siteini pack contains all the providers you can grab your epg from. The default location of the pack should be C:\Users\YourUserName\AppData\Local\WebGrab+Plus\siteini.pack

You will also need Notepad++ to edit the files. Please download it from <a href="https://notepad-plus-plus.org/downloads">https://notepad-plus-plus.org/downloads</a>

### Register or Donate
Make sure you sign up and register for an account on WebGrab+Plus. This is free to do. <br>
You can also donate to WebGrab+Plus. €5 is the minimum and this will get you the donator badge for 1 year. Each multiple of €5 will gain you an extra year.
See the table below to see the benefits of being a donator.

```licence
                             default           donator_license        registered_user         
           channels/ini      20                250                    30                      
           channels total    20                250                    30                       
           siteinis          2                 15                     3                     
           decryption keys   without userkey   enabled                enabled             
           decryption mode   legacy (V2)       new (V3) & (V2)        legacy (V2)         
           index only        yes               no                     no                
           postprocess MDB   disabled          enabled                disabled           
           postprocess REX   disabled          enabled                enabled           
           debug             False             False                  False               
           show details *    ttd               full                   ttsd              
           update mode       force             all                    light               
           channel delay     4 secs            0 secs                 2 secs              
           index delay       4 secs            0 secs                 4 secs            
           show delay        2 secs            0 secs                 1 secs  
```           

In addition to the above you will also get the use of using encrypted siteinis. See the website forum for decrypt keys. <br>
Note some siteinis require an additional donation to get the decrypt key.

### Setting up a config file part 1
Once WebGrab+Plus is installed go to the following location on your PC C:\Users\YourUserName\AppData\Local\WebGrab+Plus <br>
Note that AppData is usually a hidden folder and you may not see it. Either enable hidden folders in folder options in the control pannel or just copy and paste the address. <br>
Alternatively if you type %appdata% in the address bar and then go up one directory you can then click on Local then WebGrab+Plus.

Open WebGrab++.config.xml in Notepad++ - We will first look at the top half of the config file

```Config1
<?xml version="1.0"?>
<settings>
  <!-- for detailed info about the settings see http://webgrabplus.com/documentation/configuration/webgrabconfigxml 
  and http://webgrabplus.com/sites/default/files/downloads/Misc/Documented_Configuration_Files.zip -->
  <filename>guide.xml</filename>
  <mode>
  </mode>
  <postprocess grab="y" run="n">rex</postprocess>
  <user-agent>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36 Edg/79.0.309.71</user-agent>
  <decryptkey site="sitename">12345</decryptkey>
  <license wg-username="YourUserName" registered-email="YourEmail@example.com" password="12345">To force a license update; replace this text with the letter f</license>
  <logging>on</logging>
  <retry time-out="15">4</retry>
  <timespan>7</timespan>
  <update>i</update>
 ```
 
Between the filename tags is the name of the file that will outputted with your epg. In this case guide.xml. You can change this to what ever you want the file name to be called. <br>
If you are using an encrypted siteini and you are a donator put the name of the siteini and then the decrypt key between the decryptkey site tags. <br>
Once you are registered with WebGrab+Plus place your username in the YourUserName section (with quotations) and your email used to sign up in the email section. <br>
The password is NOT the password you use to login to WebGrab+Plus! Once you are logged into WebGrab+Plus go to your profile page. Your password is at the bottom of your profile. <br>  This is the password that should be entered into the password section of your config file.

If you later become a donator you will need to run a force update of your license. As stated above in the config example replace the line between > and the license close tag with the letter f. Then run WebGrab+Plus to update the license.

Retry time out means if there is an issue connecting to the site it will wait 15 seconds before trying again. If it still fails it will wait 30 seconds and so on in multiples of 15 seconds 4 times. In other words the 4th time it will wait 1 min before trying again. If it still fails after that then that channel grab will fail and it will move on to the next channel.

Timespan sets the number of days to grab the EPG data for. It will grab one day more than the number specified. E.G. 0 will grab 1 day. 7 will grab 8 days.

Update will set the type of grabbing WebGrab+Plus will do. <br>
The main two being: <br>
f - Force update. All data will be grabbed again. <br>
i - Incremental update. Only changes will be grabbed. E.G changes in schedule from the last grab and any additional days needing to be grabbed since the last run. Anything the same that has already been grabbed will be left unchanged so is much faster than then 1st time you grab data or running a force grab.

### Setting up a config file part 2
Now we move onto the bottom half of the config file.

```channels
		<channel update="i" site="tvguide.co.uk" site_id="66" xmltv_id="BBC News">BBC News</channel>
</settings>
```

In the above example we have told WebGrab+Plus we want to grab the data for BBC News. But where do we get these details from? <br>
All the details you need are in the siteini pack. Here you will find providers seperated in folders by country. Note that some of these files maybe old and no longer work. You will have to try them to find what works best for you. <br>
File names with E in them are encrypted and need a decrypt key for use.

In the above example I used the siteini tvguide.co.uk <br>
This can be found in the UK folder. So open that up and locate tvguide.co.uk.channels.xml and open it in Notepad++ <br>
Here you will see a list of channels this provider can grab. Copy and paste the channels you want to grab in to your config file. <br>
Now we have to change the name of the channel to match that of your playlist. Since some providers don't tag channels in their playlist with an epg tag or you may not even have direct access to the playlist the easiest way to link the channel to your playlist is just to use the channel name that is displayed in your playlist. <br>
So after xmltv_id=" make sure the name of the channel matches what is displayed in your playlist exactly. Also change the name after the > to match. <br>
So if your playlist displays the channel name as UK BBC News your line would now be:

```channels2
		<channel update="i" site="tvguide.co.uk" site_id="66" xmltv_id="UK BBC News">UK BBC News</channel>
        </settings>
```

Keep adding channels above the </settings> tag until you have all the channels you need. Refer to the license table for any limitations to the numbers you can grab and from how manny different siteinis.


### Run WebGrab+Plus
It's also a good idea to run WebGrab+Plus when you add a new siteini just to test it works correctly. All you need to do is double click Run and WebGrab+Plus will start. <br>
Any errors will output and can be viewed in WebGrab++.log.txt <br>
You can view your current license in WGLicense.log.txt <br>
Once done your EPG will be outputted as guide.xml or what ever you have called it in your config.


Move on to how to create more advanced configs for local channels and channel logos or skip to how to host the EPG file.


### How to create or update a channel list xml
#### Old way for older unencrypted Siteini
If the siteini is old and unencrypted it may use the old way of creating a channel list. 

In this example we will use canalsat.fr.ini in the France folder. <br>
Open canalsat.fr.ini with Notepad++ and find the following section:

```provider
**      #####  CHANNEL FILE CREATION (only to create the xxx-channel.xml file)
**   
** @auto_xml_channel_start
*url_index {url|https://secure-webtv-static.canal-plus.com/metadata/cpfra/all/v2.2/globalchannels.json}
*index_site_channel.scrub {multi|{"id":|"name":"|",|"type"}
*index_site_id.scrub {multi|{"id":||,"|"type"}
*scope.range {(channellist)|end}
*index_site_id.modify {cleanup(removeduplicates=equal,100 link="index_site_channel")}
*end_scope
** @auto_xml_channel_end
```

Remove the 1st * from every line starting ** @auto_xml_channel_start so it will now look like this:

```provider2
**      #####  CHANNEL FILE CREATION (only to create the xxx-channel.xml file)
**   
* @auto_xml_channel_start
url_index {url|https://secure-webtv-static.canal-plus.com/metadata/cpfra/all/v2.2/globalchannels.json}
index_site_channel.scrub {multi|{"id":|"name":"|",|"type"}
index_site_id.scrub {multi|{"id":||,"|"type"}
scope.range {(channellist)|end}
index_site_id.modify {cleanup(removeduplicates=equal,100 link="index_site_channel")}
end_scope
* @auto_xml_channel_end
```

In your config file place this line (You can rename your current config file WebGrab++.configbackup.xml and then copy it and name it WebGrab++.config.xml and delete all the current channels you have configured - WebGrab+Plus will just run the config file named WebGrab++.config.xml)

```dummy
	<channel update="i" site="canalsat.fr" site_id="dummy" xmltv_id="dummy">dummy</channel>
```

Run WebGrab+Plus <br>
The file canalsat.fr.channels.xml will be outputted containing all the channel data for you to grab from that provider. <br>
Move canalsat.fr.channels.xml to siteini.user for safe keeping. <br>
Go back to canalsat.fr.ini and put the * back from all the lines you removed it from. <br>
You are now ready to grab channels from your created channel list.


#### Create channel list for most Siteini (encrypted or unencrypted) 
For this example we will use programy-tv.cz.ini in the Czech Republic folder. (note this is an encrypted siteini) 

Open up your config file

Change the "i" in the update part to a "c" 

It will now look like this. 

```updatechannel
<update>c</update>
```

Add the follow line in the channel section

```dummy2
	<channel update="i" site="programy-tv.cz" site_id="dummy" xmltv_id="dummy">dummy</channel>
```

Run WebGrab+Plus <br>
The file programy-tv.cz.channels.xml will be outputted containing all the channel data for you to grab from that provider. <br>
Move programy-tv.cz.channels.xml to siteini.user for safe keeping. <br>
Go back to your config file and change the "c" in the update section back to an "i"<br>
You are now ready to grab channels from your created channel list.

#### New way to create channel list for new encrypted Siteini
This method is available in builds starting from V3.1.7.1 of WebGrabPlus 

#### TVguide.com example - Start here
In this example we will be using tvguide.com which is found in the international folder.

This siteini only allows you to grab channels from one provider/zip code. We will cover if you need to grab channel data from multiple providers/zip codes using this siteini later in this guide.

#### Create channel list (Excluding USA)
Copy and rename your main config file to something else for safe keeping as we need a config file with no channels in it in order to create the channel list. <br>
Open your config file WebGrab++.config.xml

Change the "i" in the update section to "c1" as shown below

```c1
<update>c1</update>
```

This siteini can grab channels from multiple countries so we need to create a country list to choose from. Note if you only want USA skip this part and go straight to the USA section of this example.

Add the following line to the channel section

```country
<channel update="i" site="tvguide.com" site_id="" xmltv_id="dummy">dummy</channel>
```

Run WebGrabPlus <br>
This will output a file called tvguide.com.channels.c1.xml which will contain a list of available countries you can use with this siteini.

Open tvguide.com.channels.c1.xml with notepad++ <br>
Copy the line for the country you want into your config file (delete the previous line we copied in first). In this example we will use Argentina.

```argentinna
<channel update="i" site="tvguide.com" site_id="ARG" xmltv_id="Argentina">Argentina</channel>
```

Change "c1" in your update parameter to "c2"
```c2
<update>c2</update>
```

Run WebGrabPlus <br>
This will output a file called tvguide.com.channels.c2.xml containng all the providers available for Argentina this siteini can grab.

Select the provider you want and copy it into your config file (again delete the previous country line we copied there first). In this example we will use DirecTV Argentina Argentina.

```directvargentina
<channel update="i" site="tvguide.com" site_id="9133006468" xmltv_id="DirecTV Argentina Argentina">DirecTV Argentina Argentina</channel>
```

Change "c2" in your update parameter to "c4"
```c4
<update>c4</update>
```

Run WebGrabPlus <br>
This will output a file called tvguide.com.channels.c4.xml containing all the channels for that provider you can then copy into your config file. <br>

Change "c4" back to "i" as you update parameter <br>
Copy all the channels you want to grab into your config file and edit the names as required. <br>
Run WebGrabPlus to start grabbing the channels.

#### To create a channel list for USA 
Copy and rename your main config file to something else for safe keeping as we need a config file with no channels in it in order to create the channel list. <br>
Open your config file WebGrab++.config.xml

Copy the following line into your config file replacing xxxx with the zip code you want to get providers for.

```zipcode
<channel update="i" site="tvguide.com" site_id="xxxx" xmltv_id="dummy">dummy</channel>
```

In this example we will use 10001 for New York.

```zipcode
<channel update="i" site="tvguide.com" site_id="10001" xmltv_id="dummy">dummy</channel>
```

Change the update parameter to "c3" as shown below.

```c3
<update>c3</update>
```

Run WebGrabPlus <br>
This will output a file called tvguide.com.channels.c3.xml containing all the providers for that zip code.

Open tvguide.com.channels.c3.xml and copy the provider you want to use into your config file (delete the zip code line we copied in previously first). <br>
In this example we will use Dish Network New York.

```dish
<channel update="i" site="tvguide.com" site_id="9100008443" xmltv_id="Dish Network New York">Dish Network New York</channel>
```

Change the update parameter from "c3" to "c4" as shown below.

```c4again
<update>c4</update>
```

Run WebGrabPlus <br>
This will output a file called tvguide.com.channels.c4.xml containing all the channels for that provider.

Change your update parameter from "c4" back to "i" <br>
Copy all the channels you want to grab into your config file and edit the names as required. <br>
Run WebGrabPlus to start grabbing the channels.

#### If you need to grab channels from more than one country/provider/zip code
This siteini can only grab channels from the same country, provider or zip code<br>
In order to grab from a different country/provider/zip code, copy and rename tvguide.com.ini eg copy and rename it tvguide1.com.ini

Repeat everything above in order to create your channel list but where you see site="tvguide.com" it will now be site="tvguide1.com"

You will need a different named siteini for every different country/provider/zip code you want to use with the tvguide siteini. Note each differently named siteini will count towards your siteini limit on your licence.

### Channel Logos
Some siteinis will grab channels automatically but others don't or you want to replace the logos with your own. There are several ways this can be done:

You can do it manually. Open your EPG xml file and find the channel you want to add a logo to in the channel list like in the example below:

```logo1
  <channel id="BBC One">
    <display-name lang="en">BBC One</display-name>
    <icon src="https://LocaionOfImage.png" />
    <url>http://www.siteiniprovider.com</url>
  </channel>
  ```
  
Either add the line that begins <icon src or ammend to point to the location of your image. <br>
Note if you run WebGrab+Plus again anything you change in your xml file will be removed. If you are going to do it this way copy all your channel info to another file so you can copy it back but remember if you add or ammend channels in your config make sure you add or ammend them in to your copied file.


The best way though is to set the siteini to automatically insert your channel logos when it grabs the EPG. <br>
Depending on the coding of the siteini depends on how you can do this.

For example tvguide.co.uk.ini <br>
For this to work you need a direct link to the logo image and it must be named the same as the site_id value. However if the site_id value has special characters once WebGrabPlus has finished use notepad++ to find and replace them with nothing effectively removing them. <br>
E.G. If the site_id ends up being 123##456 remove the ## from your finished epg xml & name the png 123456.png <br>
Open tvguide.co.uk.ini in Notepad++ <br>
Find the following lines:

```
index_variable_element.modify {set|'config_site_id'}
index_urlchannellogo.modify {addstart|https://url.com/'index_variable_element'.png}
```

Change https://url.com/ to the first part of the url where your image is located

```namelogo
		<channel update="i" site="tvguide.co.uk" site_id="66" xmltv_id="BBC News">BBC News</channel></channel>
```

If you wanted to add the logo to the above example your logo must be named 66.png - the same as the site_id value. <br>
You must have a direct link to the logo so it will add 66.png to the end part of the url set in the siteini so it will become https://url.com/66.png <br>
File storage sites normally don't give you a direct link and instead give you a shared link which will not work here. The best place to put the logo is in a folder on github and use the raw link address. This way you can get a direct link.

### Change channel logos on encrypted siteinis or post grab
Now some siteinis are encrypted so you can't edit them. So how do we change the logos on these sites? The answer is to write a script that will change them. <br>
First you need to download Git for Windows from <a href="https://gitforwindows.org">https://gitforwindows.org</a>

Now you need to create a script so open a new document in NotePad++ and paste the following in to it:

```script1
#!/bin/sh
cd /c/users/YourUserName/appdata/local/WebGrab+Plus
sed -i 's#<icon src="https://WhatYouWantToChange.com/logo.png" />#<icon src="https://NewUrl.com/NewLogo.png" />#' guide.xml
```

Save it as logoscript.sh in C:\Users\YourUserName\AppData\Local\WebGrab+Plus <br>
Now we need to edit the script. <br>
Change the location path so it matches where the script is saved (For example change the YourUserName part to your Windows username) <br>
Open your EPG xml and find the channel icon line for the channel you want to change. <br>
Copy it and past it in to the script replacing what is between the first two # <br>
Now amend https://NewUrl.com/NewLogo.png to the url of where your logo is. <br>
Open Git Bash <br>
Type the following to run your script assuming both the script and EPG xml are in the directory C:\Users\YourUserName\AppData\Local\WebGrab+Plus

```terminal
cd /c/users/YourUserName/appdata/local/WebGrab+Plus
bash logoscript.sh
```

Everything will now be replaced in your EPG xml with what you have told the script to replace. <br>
The next time you run WebGrap+Plus your ammended url will be replaced with the original so you will need to run the script each time you grab data assuming the original url doesn't change.

### Add channel logo line via script post grab
If you pull the epg and it doesn't have a channel logo and you can't modify the sitini then you will not have a line to modify like in the example above but you can still add one in via a script. The process is the same as what is written above so read that first but the script will look like this.

```addlogo
#!/bin/sh
cd /c/users/YourUserName/appdata/local/WebGrab+Plus
sed -i '9a <icon src="https://NewUrl.com/NewLogo.png" />' guide.xml
```

The number represents the line you want to add the channel logo line after. If you wanted it after line 20 then change 9a to 20a. <br>
If you are adding multiple channel logos make sure you start with the largest line number first and work to the smallest. This is because if you do it the other way round the next line it will add will be wrong eg if you tell it to add a line after 1 and then after 4 then it will add the line after 1 so the logo line is position 2 and then everything that was under it is now on a line number 1 greater than what it was before. So make sure you work from the bottom up and you won't have this issue!

You can mix adding or amending lines in the same script.

### Compress Your EPG
It is a good idea to compress your EPG so the file size is smaller. You can do this using 7zip. You want to compress it using the gz file format so change the compression method in the drop down menu. 

### Hosting your EPG
So now you have grabbed everything you wanted and you have your guide.xml or what ever you have called it and it is now time to host it. I recommend two choices. <br>
With either see how to link shorten at the end.

The first is if you are not going to be sharing the EPG publically. If it is a private EPG host it on dropbox. It is not good to host it here if you intend to share it because if a large number of people access the link then dropbox may stop access to the link. <br>
Once you have uploaded the EPG to dropbox click on the option to share and create a link to the file. <br>
Copy and paste this in to a web address bar and change the last 0 in the address to a 1 - This will allow direct downloading without any prompts.

The second is if you are going to share the EPG publically. If you indend to share it publically then upload it to Github. Once you have done this click to get the raw link for the file. 

Now you have uploaded your EPG to either site it is a good idea to shorten the link because this will save you typing in a long url and causing typos. <br>
Go to <a href="http://bit.ly">http://bit.ly</a> <br>
Register and enter your EPG link in the create a short link option. You can give the link any name you want but the shorter and easier the better.

Enter this link as your EPG source and you are done!

Note when you update your EPG in dropbox just drag and drop the new EPG in to the dropbox window - Don't delete the file. This will update the file instead and keep your link so the short link will still work <br>
In Github you can delete the file and upload the new one. As long as it's in the same repository and folder with the same file name your short link will still work

