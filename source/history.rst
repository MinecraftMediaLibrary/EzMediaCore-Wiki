History of EzMediaCore
================================

In the way beginning, I was first interested in playing audio (specifically sounds)
back on a Minecraft server I used to host with friends. We would play popular songs at
the time and listen to them while playing survival. I first started off using
`this plugin <https://dev.bukkit.org/projects/music>`__ made by Zombie_Striker. It
worked pretty decently.

Later on, I found a Spigot thread post talking about playing videos in Minecraft.
More specifically, they shared a video of playing media in Minecraft using maps.
The original video could be found `here <https://www.youtube.com/watch?v=xohW6dOGl58>`__.

After a couple months, I contacted the developer
(`BananaPuncher714 <https://github.com/BananaPuncher714>`__) and asked if I could work
with them on the project. He gladly accepted the offering and shared the source code with
me. At the time, 1.16 just came out and his plugin was only updated for 1.14 and 1.15. Due
to how it uses NMS, I had to update it because it had issues on newer versions. It ended up
working but not the best way. The video player would lag severely, and also VLC NativeDiscovery
was buggy. It was not the best experience.

BananaPuncher714 later rewrote the project from scratch supporting 1.16. The results at the end
were great, very smooth. He even added a player for entities too using their name tags. It was
cool to watch, but not ready for production.

A couple months later, I decided to host an SMP server for my friends in highschool and decided
to write a plugin which could fetch audio from a Youtube video, download it, and play it via a
resourcepack. It worked! And it worked great too. I decided to to try and make my own library
as a result from this success.

As I expanded my library from not just audio but to more interaction with actual video players,
I decided to open source my library for developers to use today. After months of development,
I have a put a ton of work myself into improving the library. If you are interested in contributing
with me, feel free to contact me on Discord or open a Github issue about it.
