# Fun with mpd

If you're not familiar with [mpd](http://www.musicpd.org/): it is a
music player daemon called _Music Player Daemon_. I have been using it for
years and today, a Debian update destroyed my setup. At first I was
wondering why there was no music showing up in
[ncmpcpp](http://ncmpcpp.rybczak.net/), which is my client of choice, and
started investigating. A short search for `mpd` in
[htop](http://hisham.hm/htop/) immediately revealed to me, that some rogue
user, whose name is mpd, now runs mpd on the port that I used to run it on
as myself. Well, Debian probably enabled that service for me in some
mysterious way. (This is actually one of the few things I do not like about
Debian.) Well, a quick

> systemctl disable mpd
>
> systemctl stop mpd

should disable it, right? -- __WRONG__!

> Warning: Stopping mpd.service, but it can still be activated by:
>  mpd.socket

At least it told me that. Anyway, what should I do about it? Remove the
socket file? Change the port of my usual mpd instance? To have some music
playing right away, I did the latter first and immediately realized that
I do not want to start `ncmpcpp` with a port parameter all the time. Also,
it is quite nice to have a socket activated mpd.

# My first shot at solving this problem

My first intuition was to do this:

> gpoupadd mpd
>
> gpassw -a saep mpd
>
> gpasswd -a mpd mpd
>
> chown -R saep:mpd ~/Music

and change the `music_directory` entry in `/etc/mpd.conf` to my home music
folder and now I have a socket activated mpd running.

# The actual solution

However, while writing this post I realized a few things. Nobody but me has
access to the laptop. Also, nobody but me in my family would listen to that
music and additionally, I would have to fix permissions for every new file
I add there. That stinks and is overly complicated. So, I can just symlink
my usual `~/.mpd/mpd.conf` to `/etc/mpd.conf` and be done with it.

> rm /etc/mpd.conf
>
> ln -s ~saep/.mpd/mpd/conf /etc/mpd.conf
>
> systemctl restart mpd

Done.

