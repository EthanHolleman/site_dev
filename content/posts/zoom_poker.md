---
title: "Casual virtual Poker with Zoom and PlayingCards.io"
date: 2020-12-15
tags: ['poker', 'blogs']
draft: false
---

Recently a few of my friends and I wanted to do virtual Poker
night. We where not interested in playing for cash and so I started looking around for an online platform to make it happen. 

Pretty much everything that comes up with a cursory google search did not satisfy my basic requirements but eventually I came across
[PlayingCards.io](https://playingcards.io/) which provided what I think
is the best solution for free, causal quarantine poker nights.

Step 1 is to set up your "table" with PlayingCards. 
Use [this link](https://playingcards.io/game/standard-deck) to start
building a table. Later once you finish setting everything up you can
share the link to the table and others will be able to join, see and
manipulate the objects on the table.

You can use the automation buttons to handle things like dealing, the
flop, turn, river shuffling, as well as betting. The room I set up looks like this.

![](/posts/images/table.png)

You can deal cards to each player using the *Deal* button and show each round of community cards using
the respectively labeled button.*Empty* sets the pot to 0, *Reset* sets the pot to 0 and all player stacks to 100 and *Reveal* shows all players cards.

The only thing that is a little clunky is betting and collecting your winnings. The automations allow you to add or subtract a value from a counter (which are used to keep track of each player's stack and the current pot) but not read from the state of another counter. This means you cannot create a button that adds the current value in the pot to a player's stack - this needs to be done by hand.

Also anyone can press any button at any time; just something to keep in mind if playing with anyone that you thought of when reading that sentence. 

![](/posts/images/table_hand.png)

Note that cards placed into the "hand" area can only
be seen by the player that put them there. This makes
keeping your pocket cards secret from everyone else
possible. 

If you don't want to set up your own room from scratch
you can [download the room I set up](/posts/docs/playingcards-io-export.zip) and then
load from that file.

No Poker is actually done over Zoom, it is only used as the video call medium. 

It definitely look a couple hands to get used to using the interface but once things got going it worked really well. We found it also helps to keep
track of your stack either on paper or using small 
text boxes on the
virtual table.
