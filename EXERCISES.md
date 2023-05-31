### Exercise 1

> ***Name*** -> ***Hello World!***

## Instructions

The classical introductory exercise. Just say "Hello, World!".

["Hello, World!"](https://en.wikipedia.org/wiki/"Hello,_world!"_program) is the traditional first program for beginning programming in a new language or environment.

The objectives are simple:

- Write a function that returns the string "Hello, World!".
- Run the test suite and make sure that it succeeds.
- Submit your solution and check it at the website.

If everything goes well, you will be ready to fetch your first real exercise.

## Solution

````php
<?php
function helloWorld()
{
    return "Hello, World!";
}
````



### Exercise 2

> ***Name*** -> ***Reverse String***

## Instructions

Reverse a string

For example: input: "cool" output: "looc"

## Solution 

````php
<?php
function reverseString(string $text): string {
    $result = strrev($text);
    return $result;     
}
````



### Exercise 3 

## Instructions

If you want to build something using a Raspberry Pi, you'll probably use *resistors*. For this exercise, you need to know two things about them:

- Each resistor has a resistance value.
- Resistors are small - so small in fact that if you printed the resistance value on them, it would be hard to read.

To get around this problem, manufacturers print color-coded bands onto the resistors to denote their resistance values. Each band has a position and a numeric value.

The first 2 bands of a resistor have a simple encoding scheme: each color maps to a single number.

In this exercise you are going to create a helpful program so that you don't have to remember the values of the bands.

These colors are encoded as follows:

- Black: 0
- Brown: 1
- Red: 2
- Orange: 3
- Yellow: 4
- Green: 5
- Blue: 6
- Violet: 7
- Grey: 8
- White: 9

The goal of this exercise is to create a way:

- to look up the numerical value associated with a particular color band
- to list the different band colors

Mnemonics map the colors to the numbers, that, when stored as an array, happen to map to their index in the array: Better Be Right Or Your Great Big Values Go Wrong.

More information on the color encoding of resistors can be found in the [Electronic color code Wikipedia article](https://en.wikipedia.org/wiki/Electronic_color_code)

## Solution 

````php
<?php


const COLORS = array(
    "black",
    "brown",
    "red",
    "orange",
    "yellow",
    "green",
    "blue",
    "violet",
    "grey",
    "white"
);
function colorCode(string $color): int
{
    return array_search($color, COLORS);
}
````



#### **Exercise** **4**

> ***Name*** -> ***Hamming***

## Instructions

Calculate the Hamming Distance between two DNA strands.

Your body is made up of cells that contain DNA. Those cells regularly wear out and need replacing, which they achieve by dividing into daughter cells. In fact, the average human body experiences about 10 quadrillion cell divisions in a lifetime!

When cells divide, their DNA replicates too. Sometimes during this process mistakes happen and single pieces of DNA get encoded with the incorrect information. If we compare two strands of DNA and count the differences between them we can see how many mistakes occurred. This is known as the "Hamming Distance".

We read DNA using the letters C,A,G and T. Two strands might look like this:

```
GAGCCTACTAACGGGAT
CATCGTAATGACGGCCT
^ ^ ^  ^ ^    ^^
```

They have 7 differences, and therefore the Hamming Distance is 7.

The Hamming Distance is useful for lots of things in science, not just biology, so it's a nice phrase to be familiar with :)

The Hamming distance is only defined for sequences of equal length, so an attempt to calculate it between sequences of different lengths should not work. The general handling of this situation (e.g., raising an exception vs returning a special value) may differ between languages.



## Solution 

````php
<?php

function distance(string $a, string $b): int
{
    if (strlen($a) !== strlen($b)) {
        throw new InvalidArgumentException('DNA strands must be of equal length.');
    }
    return count(
        array_diff_assoc(
            str_split($a),
            str_split($b)
        )
    );
}

?>
````



### Exercise 5

## Introduction

The way we measure time is kind of messy. We have 60 seconds in a minute, and 60 minutes in an hour. This comes from ancient Babylon, where they used 60 as the basis for their number system. We have 24 hours in a day, 7 days in a week, and how many days in a month? Well, for days in a month it depends not only on which month it is, but also on what type of calendar is used in the country you live in.

What if, instead, we only use seconds to express time intervals? Then we can use metric system prefixes for writing large numbers of seconds in more easily comprehensible quantities.

- A food recipe might explain that you need to let the brownies cook in the oven for two kiloseconds (that's two thousand seconds).
- Perhaps you and your family would travel to somewhere exotic for two megaseconds (that's two million seconds).
- And if you and your spouse were married for *a thousand million* seconds, you would celebrate your one gigasecond anniversary.

> If we ever colonize Mars or some other planet, measuring time is going to get even messier. If someone says "year" do they mean a year on Earth or a year on Mars?
>
> The idea for this exercise came from the science fiction novel ["A Deepness in the Sky"](https://www.tor.com/2017/08/03/science-fiction-with-something-for-everyone-a-deepness-in-the-sky-by-vernor-vinge/) by author Vernor Vinge. In it the author uses the metric system as the basis for time measurements.

## Instructions

Your task is to determine the date and time one gigasecond after a certain date.

A gigasecond is one thousand million seconds. That is a one with nine zeros after it.

If you were born on *January 24th, 2015 at 22:00 (10:00:00pm)*, then you would be a gigasecond old on *October 2nd, 2046 at 23:46:40 (11:46:40pm)*.



## Solution

````php
<?php

function from(DateTimeImmutable $date): DateTimeImmutable
{
    $giga = 1e9; // = 1000000000
    return $date->modify("+{$giga} seconds");
}

````

### Exercise 6

## Introduction

Instructions
Tally the results of a small football competition.

Based on an input file containing which team played against which and what the outcome was, create a file with a table like this:

Team                           | MP |  W |  D |  L |  P
Devastating Donkeys            |  3 |  2 |  1 |  0 |  7
Allegoric Alaskans             |  3 |  2 |  0 |  1 |  6
Blithering Badgers             |  3 |  1 |  0 |  2 |  3
Courageous Californians        |  3 |  0 |  1 |  2 |  1
What do those abbreviations mean?

MP: Matches Played
W: Matches Won
D: Matches Drawn (Tied)
L: Matches Lost
P: Points
A win earns a team 3 points. A draw earns 1. A loss earns 0.

The outcome should be ordered by points, descending. In case of a tie, teams are ordered alphabetically.

Input
Your tallying program will receive input that looks like:

Allegoric Alaskans;Blithering Badgers;win
Devastating Donkeys;Courageous Californians;draw
Devastating Donkeys;Allegoric Alaskans;win
Courageous Californians;Blithering Badgers;loss
Blithering Badgers;Devastating Donkeys;loss
Allegoric Alaskans;Courageous Californians;win
The result of the match refers to the first team listed. So this line:

Allegoric Alaskans;Blithering Badgers;win
means that the Allegoric Alaskans beat the Blithering Badgers.

This line:

Courageous Californians;Blithering Badgers;loss
means that the Blithering Badgers beat the Courageous Californians.

And this line:

Devastating Donkeys;Courageous Californians;draw
means that the Devastating Donkeys and Courageous Californians tied.


## Solution

````php
<?php
class Tournament
{
    /** @var TeamScore[] */
    private array $teams = [];
    public function tally(string $score): string
    {
        if ($score !== '') {
            foreach (explode("\n", $score) as $line) {
                [$teamA, $teamB, $result] = explode(';', $line);
                $this->teams[$teamA] ??= new TeamScore($teamA);
                $this->teams[$teamB] ??= new TeamScore($teamB);
                switch ($result) {
                    case 'win':
                        $this->teams[$teamA]->addWin();
                        $this->teams[$teamB]->addLoss();
                        break;
                    case 'draw':
                        $this->teams[$teamA]->addDraw();
                        $this->teams[$teamB]->addDraw();
                        break;
                    case 'loss':
                        $this->teams[$teamA]->addLoss();
                        $this->teams[$teamB]->addWin();
                }
            }
        }
        //La función de comparación utiliza una expresión de comparación de la nave espacial <=> para ordenar los equipos primero por puntos de forma descendente y luego por nombre de forma ascendente.
        usort($this->teams, static fn(TeamScore $a, TeamScore $b) =>
            [$b->getPoints(), $a->getName()] <=> [$a->getPoints(), $b->getName()]
        );
        return implode("\n", ["Team                           | MP |  W |  D |  L |  P", ...$this->teams]);
    }
}
class TeamScore
{
    private string $team;
    private int    $wins   = 0;
    private int    $losses = 0;
    private int    $draws  = 0;
    public function __construct(string $team)
    {
        $this->team = $team;
    }
    public function addWin(): void
    {
        $this->wins++;
    }
    public function addLoss(): void
    {
        $this->losses++;
    }
    public function addDraw(): void
    {
        $this->draws++;
    }
    public function __toString()
    {
        return sprintf(
            '%-31s|  %d |  %d |  %d |  %d |  %d',
            $this->team,
            $this->getMatchesPlayed(),
            $this->wins,
            $this->draws,
            $this->losses,
            $this->getPoints()
        );
    }
    public function getMatchesPlayed(): int
    {
        return $this->wins + $this->losses + $this->draws;
    }
    public function getPoints(): int
    {
        return 3 * $this->wins + $this->draws;
    }
    public function getName(): string
    {
        return $this->team;
    }
}

````
### Exercise 7

## Instructions

Instructions
Implement a simple shift cipher like Caesar and a more secure substitution cipher.

Step 1
"If he had anything confidential to say, he wrote it in cipher, that is, by so changing the order of the letters of the alphabet, that not a word could be made out. If anyone wishes to decipher these, and get at their meaning, he must substitute the fourth letter of the alphabet, namely D, for A, and so with the others." —Suetonius, Life of Julius Caesar

Ciphers are very straight-forward algorithms that allow us to render text less readable while still allowing easy deciphering. They are vulnerable to many forms of cryptanalysis, but we are lucky that generally our little sisters are not cryptanalysts.

The Caesar Cipher was used for some messages from Julius Caesar that were sent afield. Now Caesar knew that the cipher wasn't very good, but he had one ally in that respect: almost nobody could read well. So even being a couple letters off was sufficient so that people couldn't recognize the few words that they did know.

Your task is to create a simple shift cipher like the Caesar Cipher. This image is a great example of the Caesar Cipher:

Caesar Cipher

For example:

Giving "iamapandabear" as input to the encode function returns the cipher "ldpdsdqgdehdu". Obscure enough to keep our message secret in transit.

When "ldpdsdqgdehdu" is put into the decode function it would return the original "iamapandabear" letting your friend read your original message.

Step 2
Shift ciphers are no fun though when your kid sister figures it out. Try amending the code to allow us to specify a key and use that for the shift distance. This is called a substitution cipher.

Here's an example:

Given the key "aaaaaaaaaaaaaaaaaa", encoding the string "iamapandabear" would return the original "iamapandabear".

Given the key "ddddddddddddddddd", encoding our string "iamapandabear" would return the obscured "ldpdsdqgdehdu"

In the example above, we've set a = 0 for the key value. So when the plaintext is added to the key, we end up with the same message coming out. So "aaaa" is not an ideal key. But if we set the key to "dddd", we would get the same thing as the Caesar Cipher.

Step 3
The weakest link in any cipher is the human being. Let's make your substitution cipher a little more fault tolerant by providing a source of randomness and ensuring that the key contains only lowercase letters.

If someone doesn't submit a key at all, generate a truly random key of at least 100 alphanumeric characters in length.

Extensions
Shift ciphers work by making the text slightly odd, but are vulnerable to frequency analysis. Substitution ciphers help that, but are still very vulnerable when the key is short or if spaces are preserved. Later on you'll see one solution to this problem in the exercise "crypto-square".

If you want to go farther in this field, the questions begin to be about how we can exchange keys in a secure way. Take a look at Diffie-Hellman on Wikipedia for one of the first implementations of this scheme.



## Solution

````php
<?php

class SimpleCipher
{
    public string $key = '';
    private array $alphabet;
    public function __construct(string $key = null)
    {
        if ($key !== null && ! ctype_lower($key)) {
            throw new InvalidArgumentException();
        }
        
        $this->alphabet = range('a', 'z');
        $key !== null ? $this->key = $key : array_map(
            fn() => $this->key .= $this->determineCharacterBilateral(random_int(0, 25)),
            range(1, 100)
        );
    }
    public function encode(string $plainText): string
    {
        return $this->encodeOrDecode($plainText, static function ($position, $keyPost) {
            $value = $position + $keyPost;
            return $value >= 26 ? $value - 26 : $value;
        });
    }
    public function decode(string $cipherText): string
    {
        return $this->encodeOrDecode($cipherText, static function ($position, $keyPost) {
            $value = $position - $keyPost;
            return $value < 0 ? $value + 26 : $value;
        });
    }
    private function determineCharacterBilateral($character)
    {
        if (is_int($character)) {
            return $this->alphabet[$character];
        }
        if (is_string($character) && ctype_alpha($character)) {
            return array_keys($this->alphabet, $character)[0];
        }
        throw new InvalidCharacterException();
    }
    private function encodeOrDecode(string $cipherText, callable $operation): string
    {
        $returnString = '';
        foreach (str_split($cipherText) as $key => $character) {
            $returnString .= $this->alphabet[$operation(
                $this->determineCharacterBilateral($character),
                $this->determineCharacterBilateral($this->key[$key])
            )];
        }
        return $returnString;
    }
}


````
### Exercise 8

## Instructions

Your task is to build a high-score component of the classic Frogger game, one of the highest selling and addictive games of all time, and a classic of the arcade era. Your task is to write methods that return the highest score from the list, the last added score and the three highest scores.



## Solution

````php
<?php

class HighScores
{
    public function __construct(array $scores)
    {
        $this->scores = $scores;
        $this->latest = end($scores);
        $this->personalBest = max($scores);
        rsort($scores);
        $this->personalTopThree = array_slice($scores, 0, 3);
    }
}

````
### Exercise 9

## Instructions

Bob is a lackadaisical teenager. In conversation, his responses are very limited.

Bob answers 'Sure.' if you ask him a question, such as "How are you?".

He answers 'Whoa, chill out!' if you YELL AT HIM (in all capitals).

He answers 'Calm down, I know what I'm doing!' if you yell a question at him.

He says 'Fine. Be that way!' if you address him without actually saying anything.

He answers 'Whatever.' to anything else.

Bob's conversational partner is a purist when it comes to written communication and always follows normal rules regarding sentence punctuation in English.

The commented tests at the bottom of the bob_test.php are Stretch Goals, they are optional. They may be easier to solve if you are using the mb_string functions, which aren't installed by default with every version of PHP.



## Solution

````php
<?php

class Bob
{
    public function respondTo($request)
    {
        $isSilence = !!preg_match('/^\s*$/', $request);
        $isQuestion = substr(trim($request), -1) === '?';
        $isYell = strtoupper($request) === $request &&
            preg_match('/[A-Za-z]/', $request);
        return match (true) {
            $isSilence => 'Fine. Be that way!',
            $isQuestion && $isYell => 'Calm down, I know what I\'m doing!',
            $isQuestion => 'Sure.',
            $isYell => 'Whoa, chill out!',
            default => 'Whatever.'
        };
    }
}

````
### Exercise 10

## Instructions
Your task is determine the RNA complement of a given DNA sequence.

Both DNA and RNA strands are a sequence of nucleotides.

The four nucleotides found in DNA are adenine (A), cytosine (C), guanine (G) and thymine (T).

The four nucleotides found in RNA are adenine (A), cytosine (C), guanine (G) and uracil (U).

Given a DNA strand, its transcribed RNA strand is formed by replacing each nucleotide with its complement:

G -> C
C -> G
T -> A
A -> U



## Solution

````php
<?php

function toRna(string $dna): string
{
    $map = [
        'G' => 'C',
        'C' => 'G',
        'T' => 'A',
        'A' => 'U'
    ];
    return strtr($dna, $map);
}

````