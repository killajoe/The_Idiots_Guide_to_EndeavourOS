***I'm a complete idiot - so here's my guide for you!***

It has been asked a lot, and fairly frequently recently it seems, *especially* by new Endeavour/new to Linux users.  It was recently asked that I post how I update - so here it is.

*"How do I maintain / update / upgrade my system?!?  Help!!"*

This is *my* maintenance plan.  I have been using the same install for almost 2 years now without any major issue.  I'm VERY aware there's more than one way to do this.  And most importantly -

**Many of these can be done through the welcome center app** - They do very much the same thing, you just need to click on it.  But since this is a *terminal centric distro with a target audience of intermediate users* - we're doing this in terminal.  Completely new users who have found themselves here for whatever reason (and possibly overwhelmed) will find this even more beneficial.

**1. The Golden Rule**
Rule # 1 to keeping a system up and running and **NOT** having problems - 
*DON'T BREAK YOUR OWN COMPUTER.* Most problems are user generated.

**2. (a) Keep updated** 
- maintenance schedule - as frequently as you would like.  From several times a day to at least once every other week (in my opinion)

`yay`

That's it.  

**2. (b)  Sorting pacnew/pacsave files - when prompted by terminal**
- maintenance schedule - whenever you are notified by `yay` that you have a pacnew or pacsave file that needs tending to.  This schedule varies upon frequency of receiving them
- you will ALWAYS be notified during the update process if they are created.
- The longer you wait to tend to them, the more difficult life can become for you.
- There is a great tool in the EOS-welcome app for this that combines pacdiff and meld
- I also use the program meld from terminal for this
- *note for Arch users who may be reading this - you will need meld from the repos if you don't already have it to complete this step*

`DIFFPROG=meld pacdiff`

- remove/overwrite/merge as necessary - for more information please see the arch wiki:
- https://wiki.archlinux.org/title/Pacman/Pacnew_and_Pacsave


**3. (a) Update Mirrors - Arch** 
- maintenance schedule - approximately once every 1-2 months
- this will save the fastest 25 mirrors, will show you in terminal (verbose flag) and only call on those with https protocol - please append accordingly to your needs
- this gets saved to /etc/pacman.d/mirrorlist

I usually copy and paste this from my current mirrorlist file as it will show up on top and then I don't have to type it out every time.

`reflector --protocol https --verbose --latest 25 --sort rate --save /etc/pacman.d/mirrorlist`

**Always after updating your mirrorlist - refresh your entire system**

`yay -Syyu`

**3. (b) Update Mirrors - Endeavour (optional)**
- maintenance schedule - 1-6months
- there is not a huge amount of them, so it's up to you if it's worth it to do it more or less frequently.
- this will be saved in /etc/pacman.d/endeavouros-mirrorlist

`eos-rankmirrors --verbose`
**Always after updating your mirrorlist - refresh your entire system**

`yay -Syyu`


**4. Clean Journal**
- maintenance schedule - approximately once every 1-2 months
- more info: https://wiki.archlinux.org/title/Systemd/Journal
- this will keep 1 months (4 weeks) worth of journal entries you can still see in case you have errors

`journalctl --vacuum-time=4weeks`


**5. Clean Cache**
- maintenance schedule - approximately once every 1-2 months
- this will clean your cache of all packages
- they can be found in `/var/cache/pacman/pkg`
- paccache keeps 3 versions by default - please see the Arch Wiki if you would like other options here: https://wiki.archlinux.org/title/Pacman#Cleaning_the_package_cache

`paccache -r`

I also do not carry a cache of uninstalled packages - I assume I uninstalled them for a reason.  If you would like to remove ALL uninstalled packages (as I do)

`paccache -ruk0`



**6.  Remove Orphans**
- maintenance schedule - approximately once every 1-2 months
- ALWAYS look over your list - make absolutely sure you want to remove all packages shown.  If you would like to keep any - make them explicity installed first before proceeding.  
- by issuing this command you understand the consequences, if you do not - read about orphans here: https://wiki.archlinux.org/title/Pacman/Tips_and_tricks#Removing_unused_packages_(orphans)

`pacman -Rns $(pacman -Qdtq)`


**7. Clearing Old Configuration Files**
- maintenance schedule - whenever you feel like doing it 1 month - 12 months
- there is nothing to run, you will need to manually do this step - see wiki for this step
- https://wiki.archlinux.org/title/System_maintenance#Old_configuration_files



**8.  DON'T BREAK YOUR OWN SYSTEM**
-
- It's so important I added it at the end again
- *most* people have problems due to their own doing.  The easiest way to continue having a trouble free system is by not creating problems.  

**Warning - I'm not responsible for any and all problems that may come from following this guide.  It's your computer to do as you please, good or bad.  You are sudo, you have the power and with that it's your own responsibility to maintain your computer as you wish.  If you do NOT understand what these do - do your own research first.  Good luck.**
----


This can be shared freely as anyone would see fit.

For further information and where I got the overwhelming majority of this guide - please see:

https://wiki.archlinux.org/title/System_maintenance

:beers:
Cheers - to a long and trouble free installation.  Keep on rollin'.

*edited to include pacnew/pacsave and eos-rankmirrors as well as page breaks between each step for clarity*


*edited again - what started out as my personal guide for how I update my own Arch/Endeavour systems has been embraced by the team and community more than I originally had intended or anticipated.  I have removed some bits to make the distinction that this is a guide for Endeavour specifically and to distinguish they are not the same, nor the same project.*

Written by the famous (infamous):
https://forum.endeavouros.com/u/fbodymechanic/summary

https://forum.endeavouros.com/t/a-complete-idiots-guide-to-endeavour-os-maintenance-update-upgrade/25184
