---
layout: post
title: Powers of Tau Ceremony
published: true
category: crypto
tags: [zcash, crypto]
image: /assets/article_images/2018-02-17-powers-of-tau/z-cash-radio-lab-the-ceremony.jpeg
---
I got to take part in a crypto ceremony that I heard about on Radiolab. It was surprisingly easy to participate.

# What is the Powers of Tau Ceremony?
I won't pretend to understand. The digital currency group, The Zcash Foundation, [posted an announcement](https://z.cash.foundation/blog/powers-of-tau/) late last year that explains it, but the main thing I got was this.

>The best part is that the Powers of Tau [...] can scale to hundreds (or even thousands) of participants. As the number of participants grows, it becomes implausible that all of them could be compromised.

Basically they were looking for a lot of people to do _something_.

# Why did I do it?
Early in 2017, my friends Corinne, Jeremy, and Lexi, and they told me about this cool Radiolab podcast episode called ["The Ceremony"](http://www.radiolab.org/story/ceremony/). It was a very intriguing story, but apart from looking up Zcash, I didn't think much of it.

Then, earlier this week, my co-worker Alok emailed out about the second iteration of "The Ceremony". He was participating, and he showed how easy it was: you download a file, run a script, and upload the result. If anyone wanted to participate they just needed to [email a group](https://lists.z.cash.foundation/mailman/listinfo/zapps-wg) and let the group know.

# How did I get involved?

I fired-off [a quick email](https://lists.z.cash.foundation/pipermail/zapps-wg/2018/000255.html).

>I'd like to help out. I'm available any day of the week except Thursdays.

Less than an hour later, I got an email from one of the organizers, Jason.

>Great. I do actually have a slot this Friday (16th) at the moment.  Would that work for you?  What time zone are you in?  We normally give each participant 24 hours from the point they receive the challenge file.  I will send you further instructions when it's your turn.

On Friday, I got an email with setup instructions and a link to the site where I downloaded the challenge and needed to upload the response.

![this is what secrecy looks like](/assets/article_images/2018-02-17-powers-of-tau/challenge-website.png)

Then I got started.

# Setting-up Hardware
I installed "Raspbian Strech with Desktop" [via torrent](/assets/article_images/2018-02-17-powers-of-tau/2017-11-29-raspbian-stretch.zip.torrent) (sha `64c4103316efe2a85fd2814f2af16313abac7d4ad68e3d95ae6709e2e894cc1b`) onto my Raspberry Pi 3.

    ~ $ openssl sha -sha256 ~/Downloads/2017-11-29-raspbian-stretch.zip
    SHA256(/Users/sal/Downloads/2017-11-29-raspbian-stretch.zip)= 64c4103316efe2a85fd2814f2af16313abac7d4ad68e3d95ae6709e2e894cc1b

![imaging the SD card with Etcher](/assets/article_images/2018-02-17-powers-of-tau/etcher.png)

Once I formatted the SD card, I enabled SSH'ing into my RPi.

    ~ $ cd /Volumes/boot/
    boot $ touch ssh

# Installing Software
I installed Rust onto the Raspberry Pi...

    pi@raspberrypi:~ $ curl https://sh.rustup.rs > install-rust.sh
    pi@raspberrypi:~ $ openssl sha256 install-rust.sh
    SHA256(install-rust.sh)= 22aa1f7f4c4b9be99a9d7e13ad45b2aec6714165a0578dd5ef81ca11f55ea24e
    pi@raspberrypi:~ $ bash install-rust.sh

... and cloned [powersoftau](https://github.com/ebfull/powersoftau) (commit `d47a1d3d1f007063cbcc35f1ab902601a8b3bd91`) and downloaded my challenge file via `wget`.

Next, I `cd`'d to the `powersoftau` directory and started the program.

    cargo run --release --bin compute

This downloaded and installed everything I needed. Once all the network requests were done, I unplugged my router from the wall, so I could still SSH into my RPi, but there was no internet connection (fortunately my roommates were out of town).

Less than two minutes into running, the Rust program crashed unceremoniously with a when the OS decided it had enough.

    Killed

I threw a similar setup on my laptop (MacBook Pro (15-inch, 2016) running 10.13.3) with the same version of Rust and the GitHub repo ran the code in case the Raspberry Pi didn't follow through. I turned the internet connection back off on my laptop and disabled my router.

![I covered the laptop in a silver mylar blanket. I don't think it made anything more secure, but it made me feel safer.](/assets/article_images/2018-02-17-powers-of-tau/silver-mylar-blanket.jpeg)

# Running the Program
To get entropy for the program, I went to the local transit station (16th/Mission BART) and asked people for random numbers. Only a handful of people were willing to talk to me, so I eventually resorted to messaging a bunch of my friends saying "Please send me a number" over Signal and Facebook Messenger (using the Signal option). I also went karaokeing, and I added some of the songs as well.

![I think this counts as entropy.](/assets/article_images/2018-02-17-powers-of-tau/karaoke-entropy.jpeg)

The program took a few hours to run and resulted in this.

    Writing your contribution to `./response`...
    Done!
    
    Your contribution has been written to `./response`
    
    The BLAKE2b hash of `./response` is:
            1f65d9db a726e65f 96e97235 3eb58707
            48bf26e2 d04575b4 e2f95cd6 5ce4fb65
            c7157dfe 497559b9 bd8f453a 6fbe1c68
            daced14e 09e51975 64773fdb 437d8ac7

# Thanks
Thank you to Alok for telling me about this and to all of the people who gave me seed numbers for the ceremony: Alen, Amod, Annirudh, Anton, Axel, Christian, Conor, Corinne, Hailey, JB, Katrina, Leila, Matt, Maximillian, Mike, Mike, Reva, Waseem, and Will.