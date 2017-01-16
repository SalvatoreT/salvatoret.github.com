---
layout: post
title: Customizing Your Mac Input Source Icon
published: true
category: hack
tags: [input source, hack, flag]
image: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/lights-1282268_1920.jpg
---
## Motivation
[Pair programming](http://en.wikipedia.org/wiki/Pair_programming) is pretty common around [Square](http://corner.squareup.com/), and I've had the fortunate experience of pairing with my manager, [Xavier](http://xaviershay.com/). Now, if (you have a Mac and) you've ever had to type in a different language, you know that there is a flag in the top right corner that signifies the layout.
![Qwerty](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/qwerty.png)
The U.S. traditional Qwerty layout that we all know and love.

![Dvorak](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/dvorak.png)
A layout for people who want to try new things.

![Pinyin](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/pinyin.png)
The layout I had to use for the one semester I took Chinese.

![Colemak](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/colemak.png)
The layout that I never heard of before Square and a layout that pretty much only Xavier uses.

This brings us back to pair programming. Xavier is very proficient with his keyboard layout and added it to the configurations. When I first the little 'CO' in the top corner, I joked that it stood for 'communist', and from then on, it was referred to as Xavier's communist layout. To drive the point home, I changed the display from this...
![](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/colemak_full.png)
... to this ...
![](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/communist_full.png)

## How to make a custom layout

### Step 1: Make an icon.
Select an image for your layout, and visit [iConvert](http://iconverticons.com/online/). I tried their software with no luck, but you might have a better outcome. Browse to your image and hit convert. Once it does its magic, click the "Download .icns" button.
![Download icns](/assets/article_images/2013-07-28-customizing-mac-input-source-icon/download_icns.png)

### Step 2: Make the keyboard layout
Download the Unicode Keyboard Layout Editor, [Ukelele](http://scripts.sil.org/ukelele) (version 2.2.4 worked for me), and open it. Once you have it open, make sure your keyboard layout is the one you want to replicate.

![Ukelele's icon is a ukulele]

If it isn't you can change it by navigating to  > **System Preferences** > **Language & Text** > **Input Sources** and checking the box for the layout you want. Then, click the layout icon in the top right corner of your screen and select the one you want.

![check language]

In Ukelele, select **File** > **New From Current Input Source** which should open a new keyboard window with your current keyboard layout. 

Then, set your icon file by going to **Keyboard** > **Attach Icon File...** and layout name by going to **Keyboard** > **Set Keyboard Name...**.

Finally save your layout by going to **File** > **Save As Bundle...**.

![save as bundle]

### Step 3: Use the layout
To install the layout, take your newly minted .bundle file and store it in your Library/Keyboard Layouts folder. If you can't find this folder, go to **Applications** > **Utilities** > **Terminal** and paste this line in:

```open ~/Library/Keyboard\ Layouts/```

![open image library]

Once you have your bundle in the layout folder, restart your computer, and your new layout will be listed under  > **System Preferences** > **Language & Text** > **Input Sources**. Check your custom keyboard, select it from the top corner.

![select layout]

### Step 4 (optional): Share
When you share your layout bundle, make sure to upload it to Dropbox or Skydrive and send the link to the bundle. I tried emailing the bundle and Gmail striped-out some important piece that prevented it from working.

Here is the [Communist Colmak][] and [Jedi Dvorak][] that I made for Xavier and this blog post respectively.

[Ukelele's icon is a ukulele]: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/Ukelele_512x512x32.png
[check language]: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/check_language.png
[save as bundle]: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/save_as_bundle.png
[open image library]: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/open_image_library.png
[select layout]: /assets/article_images/2013-07-28-customizing-mac-input-source-icon/select_layout.png
[Communist Colmak]: /files/posts/custom_keyboard_layout/Communist.bundle.zip
[Jedi Dvorak]: /files/posts/custom_keyboard_layout/Jedi.bundle.zip

