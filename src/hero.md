It still happens to me, after almost a decade of owning S4's, that I find myself accidentally controlling the wrong deck (C/D instead of A/B) because I forgot about the state of the deck switch button.

The "toggle" style button doesn't allow you to build muscle memory and when things need to be done quickly this becomes a major pain in the ass.

So after 8 years of thinking about it, I finally bought an extra S4. The MK1's are pretty affordable second-hand these days. Worst case scenario I'd end up with a bunch of nice knobs.

When I opened it up I was pretty happy to see they used a neatly panellised PCB design, I tend to waaaaaaay over-engineer things so now I could just leave the PCB on, cut the traces on it, and connect the components to my own PCB.

However, things get better.

The S4 is using 74HC595 and 74HC165 chips to interface with the LED's and buttons and exposes all IO very neatly though simple JST connectors. This means you could just trace all the leads on the PCB and just connect a micro controller to these connectors and be done. And I did!

Not everything is working perfectly, the FX section unfortunately needs a custom PCB and not everything has been completely figured out but the majority of the work has been done. If you want to chat about this, join us in the DJTT thread (link below) and if you're interested in the technical aspects have a look at the docs on Github (link below).

Want to stay up-to-date? Shoot me an email or better comment on DJTT and you'll get an email when something new gets posted. 

Cheers!

Will

## Links
- [DJTT Thread](https://forum.djtechtools.com/showthread.php?t=96697)
- [Github](https://github.com/willwillems/KontrolS1)
- [Contact](mailto:s1@willwillems.com)
