BeowulfAPI
==========

Training Documentation for Beowulf API 2.0

## Introduction

Beowulf is a dog.  She is fluffy and cute.

## Table of Contents
* [Eating Schedule](#eating-schedule)
* [Walk Schedule](#walk-schedule)
* [Commands](#commands)
* [Rewards](#rewards)
* [Distractions](#distractions)
* [Likes](#likes)
* [Dislikes](#dislikes)
* [Strangers FAQ](#stranger-faq)
* [Something Seems Wrong](#something-seems-wrong)

## Eating Schedule

Beowulf currently eats once a day


## Walk Schedule



## Commands


```objc
typedef enum {
    kStanding = 0, //four legs extended
    kSitting, //two front legs extended only, butt on ground
    kLayingDown, //no legs extended, all of belly on ground
    kNaughtyLayingDown, //front paws at angle, belly not entirely on ground
} DogState;

typedef enum {
    kQuiet = 0, //making no vocalization
    kBarking, //making normal dog "woof" sound
    kClucking, //making short bursts of noise 
    kGrowling, //mean sounding vocalization, teeth showing
    kMumbling, //like growling but doesn't sound aggressive, teeth not showing
} DogVocalizations

@interface Beowulf ()

@property (nonatomic) DogState currentState;
@end

@implementation Beowulf

/**
* Changes Dog State from standing to sitting.
*/
- (void) sit {
	[self sayCommand:@"Sit"];
	if(self.currentState == kStanding) {
		self.currentState = kSitting;
	} else {
		if(kLayingDown) {
			//nothing will happen
		}
	}
}
```

## Rewards



## Distractions



## Likes



## Dislikes


