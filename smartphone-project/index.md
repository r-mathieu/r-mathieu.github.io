# Reuse my "old" smartphone


### A little story...

In March 2020, I needed a new phone and I didn't want to spend a lot of money on a phone so I took one of the best "old" phone in 2017 I bought a refurbished phone, the [Google Pixel 2 XL](https://www.gsmarena.com/google_pixel_2_xl-8720.php) for 200€ (Launch price was 950-1050€, what a decrease) and also I try to spend as little time as possible on it to spend more time on gami... coding and some passions. 

And for me, it (still) is a great phone even for an "old" phone, it's still fast, it takes pretty good photos, the quality of the screen is great and I loved the design... Even if I don't spend a lot of time on it, what a joke.

In November 2021, still in love with this phone, I decided to make it look a bit like new. New battery, new USB-C entry port, apply a new thermal paste and even a new earpiece speaker dust mesh !

{{< image src="/images/personal-project/fix-phone.png">}}

After a looooong shipping of nearly 1 month (USA -> France), I finally received everything. Helped with some tutorials and tools, let's do it.

However...

![Alt text](/images/personal-project/oh-no.png "I didn't break the screen, I'm nearly sure this is the result of too much heat.")

At this point, I didn't want to spend much more money (which was already 150€ and 50% just for taxes and shipping) and a new screen costs 180€... without taxes and shipping... oh dear. So I decided to buy a new phone and with the knowledge of "if it's too hot, you can buy a new phone" if I want to redo the experience.

In 2022, I decided to bring all the old phones, computers, etc... my parents and my neighbours had to a recycle center. And I looked at my Pixel 2 XL and had an idea.

### A New Hope

**So, can I replace my Raspberry Pi 3 with my Pixel 2 XL ? It means just running [Syncthing](https://syncthing.net/) and [Emby](https://emby.media/) ?**

- [Syncthing](https://syncthing.net/), absolutely no problem, it'll use the internal storage of the phone (~54GB).

- Emby, I'll plug my HDD and found an [USB hub ](https://www.amazon.fr/gp/product/B092HG1BJY) *(Well, **I don't recommend this one**, it's really noisy when it's "charing" and because the ONLY USB3.0 doesn't work with the HDD or a USB key but no problem with a keyboard or a mouse, PER-FECT)*


{{< image src="/images/personal-project/usb-hub-charing.jpg">}}

But I had little problem, **FAT32 is only supported for external storage** and I'll will absolutely not shrink *The Lord of the Rings: The Return of the King - Extended version* in 3 parts but mostly because I'm pretty sure Emby will not support it.

But after some long research, I finally found a mod.

[External sdcard rw permission enabler plus extras ](https://forum.xda-developers.com/t/external-sdcard-rw-permission-enabler-plus-extras-module.4078731/)

And this is what I installed on my phone.

- **[Ressurection Remix 8.5.8](https://resurrectionremix.com/)** (Android 10) (Couldn't find [LineageOS 17.1](https://lineageos.org/**))
- **[Magisk](https://github.com/topjohnwu/Magisk)**
- **[External sdcard rw permission enabler plus extras ](https://forum.xda-developers.com/t/external-sdcard-rw-permission-enabler-plus-extras-module.4078731/)**
- **[Syncthing](https://syncthing.net/)**
- **[Emby Server for Android](https://emby.media/server-android.html)**

And also **[ACCA (Advanced Charging Controller App)](https://github.com/MatteCarra/AccA)** and **[MagiskSSH](https://github.com/Magisk-Modules-Repo/ssh)** but it's only for me.

### The Result

However, this mod is "unpredictable". I wasn't able to use it with Android 11 but I had no problem with Android 10 but on Android 10, after I installed it, I can't access to the "Developer Options" to enable the "ADB WiFi Debugging". It's not a big lost and maybe I can still enable it with the SSH connection or with a terminal on the phone.

And the main cons now, it's Android, instead of just searching a software to install like the previous OS, [DietPi](https://dietpi.com), I need to search "Is there an Android version of this software ?". Or search a way to easily deploy a software.

But the result is still great, Syncthing is much faster to sync my folders and files between my new phone, my computer and my laptop than on my Raspberry Pi 3, Emby is much quicker too. And  for the power consumption, it's the same in idle state and with the HDD connected, 2.2-2.5 Watt but I didn't try while watching a movie.

Also, to preserve the new battery, I set the maximum charging at 66% with ACCA and also enable the Idle Mode so once the battery is charged at it's limit, the charging switch to powering only the phone itself so the battery will slowly decrease by itself (losts ~2% in 2 weeks) before starting recharging when it reach 20%.

{{< image src="/images/personal-project/smartphone-project.png">}}

![Alt text](/images/personal-project/smartphone-support.png "I also retrieve a little support to hold the phone and the USB Hub and attach the HDD below.")
