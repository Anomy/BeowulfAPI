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
* [Biting](#biting)

## Eating Schedule

Beowulf currently eats once a day


## Walk Schedule



## Commands


```objc
typedef enum {
    kPostitionStanding = 0, //four legs extended
    kPostitionSitting, //two front legs extended only, butt on ground
    kPostitionLayingDown, //no legs extended, all of belly on ground
    kPostitionNaughtyLayingDown, //front paws at angle, belly not entirely on ground
    kPostitionJumpingOnHuman, //Paws on human
    kPostitionJumpingOnFurniture, //Paws on furniture
    kPostitionJumpingOnObject, //Paws on object
    kPositionSittingWiggleButt, //Sitting with butt clearly moving back and forth, butt does not leave ground
    kPositionStandingWiggleButt, //Standing with but clearly moving back and forth
} DogPosition;

typedef enum {
    kVocalizationQuiet = 0, //making no vocalization
    kVocalizationBarking, //making normal dog "woof" sound
    kVocalizationClucking, //making short bursts of noise 
    kVocalizationGrowling, //mean sounding vocalization, teeth showing
    kVocalizationMumbling, //like growling but doesn't sound aggressive, teeth not showing
} DogVocalizations

@interface Beowulf ()

@property (nonatomic, readonly) DogPosition currentPosition;
@property (nonatomic, readonly) DogVocalization currentVocalization;
@property (nonatomic, strong) Human *human;

@end

@implementation Beowulf

/**
* Changes Dog State from kPositionStanding to kPositionSitting.
*
* Required Current State: kPositionStanding
* New State: kPositionSitting
*
* Required: Dog will only respond to @"Sit" from kPositionStanding state.
*/
- (void) sit;

/**
* Changes Dog State from kPositionSitting to kPostitionLayingDown.
*
* Required Current State: kPositionSitting
* New State: kPostitionLayingDown
*
* Required: Dog will only respond to @"Sit" from kPositionStanding state.
* 
* Possible Errors: will only sit partway and will wind up in kPostitionNaughtyLayingDown
* Correct this Error: snap (or whatever we figure out) and point and the ground in front of her nose
* 					do your best not to repeat the command or say the her name.
*/
- (void) down;

/**
* Changes Dog State from (kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject) to kPositionStanding.
* 
* Required Current State: kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject
* New State: kPositionStanding
* 
* Possible Errors: Using "down" instead of "off", this will probably work, but confuses dog to use one word for multiple commands
*/
- (void) off;

/**
*/

```

## Rewards
```objc

typedef enum {
	kRewardDogBiscuits = -3, //Beowulf hates normal dog biscuits
    kRewardKibble = 0, //a piece of whatever the current food is, generally apathetic
    kRewardPetting = 1, //Beowulf would love this, though may not understand that it's a treat
    kRewardAnyHumanFood = 3, //If you hand it to her, she'll show interest at least
    kRewardCheese = 4, //It's exciting, but meat is yummier
    kRewardPupperoni = 5, //Favorite kind of treat dog treat
    kRewardThrowBall = 6, //Beowulf would love this, though may not understand that it's a treat
    kRewardDogIceCream = 7, //This is a real thing.
    kRewardHumanMeat = 10, //Best. Thing. Ever.
} Reward

```


## Distractions



## Likes



## Dislikes


