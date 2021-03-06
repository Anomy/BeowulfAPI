BeowulfAPI
==========

Training Documentation for Beowulf API 2.0

## Introduction

Beowulf is a dog.  She is fluffy and cute.
![Imgur](http://i.imgur.com/P3td4Ao.jpg "Logo Title Text 1")

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

### Food
Beowulf currently eats twice a day, in the morning after her AM walk, she gets one scoop of the [Wellness Dry: Complete Health Chicken](https://www.freshdirect.com/pdp.jsp?productId=gro_pid_4007877&catId=dog_food_dry_nat) in the purple bag, or from the green storage container.

### Poison to dogs
There are many foods which are poisonous to dogs that are easy to foget about, apple seeds, grapes, onion and garlic are just a few.  For a better list plase see this [PetMD List:](http://www.humanesociety.org/animals/resources/tips/foods_poisonous_to_pets.html?referrer=https://www.google.com/)

### Water
Beowulf can have as much water as she can drink. 
Keep an eye on how much you're giving her, a lot of water will mean 
she has to go out more often.

## Walk Schedule

(Owner*)self.human often says "walk" when she means "take Dog outside".  Dog park is preferable.

Walking Bey is great for bonding time when dog skills are going well.
She gets a lot more exercise and interaction at the dog park, however,
so taking her there and then playing with her and petting her at home, seems ideal for now.

If she doesn't go poo at the dog park, she will need to be taken on a walk.  Sometimes, when she 
gets so excited about the other dogs or squirrels, she just won't go and needs to be away from the distractions.

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
    kPositionStay, //kPostitionSitting state change blocked until release or okay command is given
} DogPosition;

typedef enum {
    kVocalizationQuiet = 0, //making no vocalization
    kVocalizationBarking, //making normal Dog "woof" sound
    kVocalizationClucking, //making short bursts of noise 
    kVocalizationGrowling, //mean sounding vocalization, teeth showing
    kVocalizationMumbling, //like growling but doesn't sound aggressive, teeth not showing
} DogVocalizations

@interface Beowulf : BorderCollie //inherits from WorkingDogs : DomisticDogs

@property (nonatomic, readonly) DogPosition currentPosition;
@property (nonatomic, readonly) DogVocalization currentVocalization;
@property (nonatomic, strong) Human *human;


#pragma mark - Basic Commands

/**
* Required Current State: kPositionStanding
* New State: kPositionSitting
* 
* returns TRUE IFF dog has two front legs fully extended rising the head off the ground && back two legs are fully collapsed with booty on the floor.
*/
- (void)no;

/**
* Required Current State: kPositionStanding
* New State: kPositionSitting
* 
* returns TRUE IFF dog has two front legs fully extended rising the head off the ground && back two legs are fully collapsed with booty on the floor.
*/
- (BOOL)sit;

/**
* Required Current State: kPositionSitting
* New State: kPostitionLayingDown
*
* Possible Errors: 
* 		will only lay down partway and will wind up in kPostitionNaughtyLayingDown
*		saying @"lay down" instead of only down.  probably works, but a consistant command is easier for Dog.
* Correct this Error: snap (or use correction clicker) and point and the ground in front of dog's nose
* 					do not repeat the command or say the dog's name.
* 
* 
*/
- (BOOL)down;

/**
* Usual Current State: kPositionSitting || kPositionStay
* generically lets Dog know that she can move.
* removes block on state change for 
*/
- (void)okay;
- (void)release;

/**
* works only from sit position, either paw may be offered to shake.
*/
- (void)shake;

/**
* Required Current State: kPostitionLayingDown
* New State: kPositionSitting
*
* Possible Errors: Dog may refuse to sit up
*                  Dog will only respond to @"Up" from kPostitionLayingDown state.
* Correct this Error: snap (or whatever we figure out) and point and the ground in front of her nose
* 					do your best not to repeat the command or say the her name.
* Warning: Dog HATES this command and will bark almost every time
*/
- (void)up;


/**
* Changes Dog State from (kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject) to kPositionStanding.
* 
* Required Current State: kPostitionJumpingOnHuman || kPostitionJumpingOnFurniture || kPostitionJumpingOnObject
* New State: kPositionStanding
* 
* Possible Errors: Using "down" instead of "off", this will probably work, but confuses Dog to use one word for multiple commands
*/
- (void)off;

/**
* use when Dog is interacting with something she should not
* good for use when Dog is in the midst of what might be a tussle
* or some kind of extremely distracted behavior, like skateboards.
* use sparingly.  It's kind of an emergency command.
*/
- (void)leaveIt;

/**
* use when Dog has something in her mouth she should not
* good for use when Dog tries to steal a ball from the park
*/
- (void)dropIt;

/**
* she is really hit and miss on this one.
*/
- (void)come;

/**
* after Dog sits and (in theory) waits patiently to move through a door
* this command lets Dog move through door
*/
- (void)outside;

#pragma mark - Lesser Used Commands

/**
* this one is a sham.  but it's cute to say it and see her run to the door from the elevator
*/
- (void)goHome;

/**
* Required Current State: kPostitionSitting
* New State: kPositionStay
*
* TODO: Rewrite - This command was poorly implemented and due for a re-write.
* 
* returns TRUE if dog sits and stays until told to release
*/
- (BOOL)stay;


#pragma mark - Deprecated Commands  //who am I kidding, they never worked.
- (void) rollOver;
- (void) quiet;
- (void) speak;
- (void) bang;
- (void) heel;

```

## Rewards
```objc

typedef enum {
    kRewardGrapesOrRaisens = -100, //Dog Poison, often given to dogs, some dogs are deathly allergic
    kRewardDogBiscuits = -3, //Beowulf hates normal dog biscuits
    kRewardVegetables = -2, //Beowulf will chew and spit out vegetables
    kRewardFruit = -1, //will simply not eat most fruit
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


## Debugging tips


