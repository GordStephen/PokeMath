---
layout: post
title: Optimal Feebas Fishing 
---

Ah, Milotic. One of my favourite Pokemon in general, but also one of the most rewarding to obtain back when it was first introduced in Gen III. Evolving a Feebas into a Milotic was a unique experience in its own right, but catching that Feebas in the first place was a major challenge.

If you didn't play any of the original Ruby/Sapphire/Emerald games, or just don't remember, here's the deal with Feebas: it can only be found in the wild on Route 119, and only via fishing. And then -- and this is what makes it so special -- _it can only be encountered on six random water tiles out of the entire route_ - the rest of the tiles only have Carvannah. For reference, this is Route 119:

![Hoenn's Route 119 (via Bulbapedia)](/public/img/HoennRoute119.png)

...that's a lot of water tiles - 400 to be precise. At least it's not [Route 124](http://bulbapedia.bulbagarden.net/wiki/File:Hoenn_Route_124_E.png)?

Needless to say, in Gen III Feebas is a rare Pokemon indeed. But with a bit of math, we might be able to ease at least some of the pain of finding it. What we know so far: 

- N = 400 fish-able water tiles on Route 119
- K = 6 of those contain Feebas

At this point, the optimal (minimal-time) Feebas-finding strategy seems pretty obvious: just systematically cast your line on each accessible water tile, and eventually you'll encounter our elusive fish friend. This is a classic sampling-without-replacement problem, and so the probability of encountering a specific number of Feebas tiles after checking a specific number of possible Feebas tiles should be given exactly by the [hypergeometric distribution](https://en.wikipedia.org/wiki/Hypergeometric_distribution).

But... there's a catch. Even if you're fishing on one of the six Feebas tiles, you're not guaranteed to catch a Feebas - you might still get a Carvannah instead! This opens up the possibility of overlooking a Feebas tile by mistake. So, maybe we should fish on each tile more than once. But how many times? We need to balance being sure that our current tile doesn't have Feebas (cast as many lines as possible) with a desire to find Feebas as quickly as possible (cast as few lines as possible). This is where things get fun! Let's update what we know:


- N = 400 fish-able water tiles on Route 119
- K = 6 of those contain Feebas
- p = ? probability of encountering a Feebas when landing a Pokemon on a Feebas tile 
- q = 1-p probability of encountering a Carvannah when landing a Pokemon on a Feebas tile

This one extra variable p (previously implicitly assumed to equal 1) complicates our math a fair bit. Let's start by defining the probablilty of encountering only Carvannah when we hook m Pokemon on a Feebas tile. Since Pokemon encounter probabilities are independent this is fairly simple:

\\[ P_{\text{only Carvannah}} = q^m = (1-p)^m \\]

From this we can get the probability of encountering at least one Feebas after m encounters on a Feebas tile, which is the same as the probability of _not_ encountering only Carvannah.

\\[ P_{\text{at least one Feebas}} =  1- P_{\text{only Carvannah}} = 1 - (1-p)^m\\]

Great! So, now we know the probability of encountering a Feebas after m encounters on a Feebas tile.

For our next step, let's consider the probability of actually being on Feebas tile.
