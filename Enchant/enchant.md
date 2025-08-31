### Solving the "Enchant" Challenge

I started the **Enchant** challenge, which was about Minecraft’s enchantment table. At first, I thought it would be simple. But when I opened the given file, it was filled with weird, unreadable text like this:

á´²å•Žáƒ¤á´·á‘μáˆ·á´´å„„åˆ¨â„‰ a•Žá´´áŽ­áŠáƒ¤á´·


I was confused—what even was this? It looked like broken encoding. After some searching, I found a **Mojibake decoder** online. I pasted the text there, and it finally turned into something readable:



ᒲ╎リᒷᓵ∷ᔑ⎓ℸ ̣ ╎ᓭ⎓⚍リ


Still looked odd, but then I realized: *"This looks like the Minecraft Enchanting Table language (Standard Galactic Alphabet)!"* So, I used an SGA chart to match each symbol and decode it into plain English.

And just like that, I got the flag:

**Final Flag:**
`scriptCTF{minecraftisfun}`

This challenge wasn’t too tough—no crazy reversing or hacking. The weird text at the start was the tricky part, but once I figured it out, it was a fun and straightforward solve! 🎮
