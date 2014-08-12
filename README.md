BeowulfAPI
==========

Training Documentation for Beowulf API 2.0

## Introduction

Beowulf is a Dog.  She is fluffy and cute.

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

Beowulf currently eats once a day, she gets two scoops of the Wellness food in the purple bag.
Beowulf can have as much water as she can drink until 9 or 10 pm or so.  
		Keep an eye on how much you're giving her, a lot of water will mean 
		she has to go out more often.

## Walk Schedule

Walking Bey is great for bonding time when Dog skills are doing well.
She gets a lot more exercise and interaction at the Dog park though,
so taking her there and then playing with her and petting her at home, seems ideal for now.

If she doesn't go poo at the Dog park, she will need to be taken on a walk.  Sometimes she 
gets so excited about the other Dogs, she just won't go and needs to be away from the distractions.

Walking Bey in the morning during the park's off leash time is really hard on her.  
She really wants to also be off leash so taking her to the park is preferable especially
during that time.

Required: Once in the morning when she wakes up. must do both

Required: Once in the evening around 8 or 9. must do both

Optional: Two additional walks

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
    kVocalizationBarking, //making normal Dog "woof" sound
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
* Required Current State: kPositionStanding
* New State: kPositionSitting
*/
- (void) sit;

/**
* Required Current State: kPositionSitting
* New State: kPostitionLayingDown
*
* Possible Errors: 
* 		will only lay down partway and will wind up in kPostitionNaughtyLayingDown
*		saying @"lay down" instead of only down.  probably works, but a consistant command is easier for Dog.
* Correct this Error: snap (or whatever we figure out) and point and the ground in front of her nose
* 					do your best not to repeat the command or say the her name.
*/
- (void) down;

/**
* Required Current State: kPostitionLayingDown
* New State: kPositionSitting
*
* Required: Dog will only respond to @"Up" from kPostitionLayingDown state.

* Possible Errors: Dog may refuse to sit up
* Correct this Error: snap (or whatever we figure out) and point and the ground in front of her nose
* 					do your best not to repeat the command or say the her name.

* Warning: Dog HATES this command and will bark almost every time
*/
- (void) up;


/**
* Changes Dog State from (kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject) to kPositionStanding.
* 
* Required Current State: kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject
* New State: kPositionStanding
* 
* Possible Errors: Using "down" instead of "off", this will probably work, but confuses Dog to use one word for multiple commands
*/
- (void) off;

/**
* use when Dog is interacting with something she should not
* good for use when Dog is in the midst of what might be a tussle
*/
- (void) leaveIt;

/**
* use when Dog has something in her mouth she should not
* good for use when Dog tries to steal a ball from the park
*/
- (void) dropIt;

/**
* she is really hit and miss on this one.
*/
- (void) come;

/**
* after Dog sits and (in theory) waits patiently to move through a door
* this command lets Dog move through door
*/
- (void) outside;

/**
* generically lets Dog know that she can move.
*/
- (void) okay;

/**
* works only from sit position, either paw may be offered to shake.
*/
- (void) shake;

/**
* this one is a sham.  but it's cute to say it and see her run to the door from the elevator
*/
- (void) goHome;

#pragma mark - Lesser Used Commands
/**
* we worked really hard on this but, she's not great at it.
*/
- (void) stay;

#pragma mark - Failed Commands
- (void) rollOver;
- (void) quiet;
- (void) speak;
- (void) bang;
- (void) heel;

```

## Rewards
```objc

typedef enum {
	kRewardDogBiscuits = -3, //Beowulf hates normal Dog biscuits
    kRewardKibble = 0, //a piece of whatever the current food is, generally apathetic
    kRewardPetting = 1, //Beowulf would love this, though may not understand that it's a treat
    kRewardAnyHumanFood = 3, //If you hand it to her, she'll show interest at least
    kRewardCheese = 4, //It's exciting, but meat is yummier
    kRewardPupperoni = 5, //Favorite kind of treat Dog treat
    kRewardThrowBall = 6, //Beowulf would love this, though may not understand that it's a treat
    kRewardDogIceCream = 7, //This is a real thing.
    kRewardHumanMeat = 10, //Best. Thing. Ever.
} Reward

```


## Distractions



## Likes



## Dislikes


