# 01-learn-december-2022
[Learn You A Haskell - Miran Lipovaca](http://learnyouahaskell.com/)

## Introduction
- Purely functional programming language
- In FP, we express everything in the form of functions
- functions has no side effects
- variables are mostly immutable
- Only thing a function can do is to take in parameters and return a value
- Say if a function is called multiple times with the same parameters, it is guaranteed to return the same result -> Referntial Transparency
- Suits for complex computation and deduce a business logic
- **Haskell** is lazy (won't execute unless specified, one detected any changes)
- Makes programs as a series of *transformation of data* 
- Statically typed. (Compiler knows what is what data type -> errors are caught at compile time)
- Has **Type Inference** (Compiler figures out the type from the datam, no need type annotation in every line of code, makes code more generic)
- Strict Compiler
- Haskell was published in **2003**

## The Compiler
- GHC (Glasgow Haskell Compiler) is the most widely used Haskell Compiler
- comes batteries included -> [here] (https://www.haskell.org/downloads/)
- GHC => Takes in haskell script (.hs extension), compiles it interractively
- **ghci** -> interactive GHC Compiler
- **:l <file-name>.hs** -> to load the file to ghci
- **:r** -> to reload the script (for getting any changes reflected)
- type `ghci` something like this will appear
`
GHCi, version 6.8.2: http://www.haskell.org/ghc/  :? for help  
Loading package base ... linking ... done.  
Prelude>
`
- to change `Prelude>` prompt to `ghci>` prompt -> **:set prompt "ghci> "**

### NOTES:
- Always use Negating numbers within paranthsis
`5 * (-3)`

## Operations & General patterns
- Arithmetics -> +, -, *, /
- Boolean -> &&, ||, not(). -> (True/ False) values
- Other funtions
	- `succ 8` gives 9 => gives the successor
	- `min 9 10` gives 9 => minimum number
	- `max 9 10` gives 10 => maximum number
- func<space><parameter> => takes higher precedence
`
succ 9 * 10 => 10 * 10 => 100
succ (9 * 10) => succ 90 => 91
`
- infix version of functions can be
`
div 92 10 <=> 92 `div` 10
`
- function calls are made with spaces rather than ()
`
bar (bar 3) <=> bar(bar(3))
`
- functions are defined similar way as they are called
`
doubleMe x = x * 2 <=> what we do as doubleMe(x) { x * 2 }
doubleMe 9 -- gives 18
`
- Functions can be defined in any order
- Sample if statement
`
doubleSmallNumber x = if x > 100
			then x
			else x * 2
`
- if statement in Haskell mandates for an else statement, because if is an expression and every expression in Haskell need to return something
- a strict version of the function is
`
doubleSmallNumber' x = (if x > 100 then x else x * 2) + 1) 
`
- functions can't begin with Capital letters
- a variable in other language is a function without a parameter in haskell
`
kevinO'Brian = "It's Kevin O'Brian"
-- a function, not a variable, "'" character is valid in a function name
`

## lists
- lists, strings (list of chars), list comprehensions
- lists are homogeneous DS (stores data of same type)
- denoted within square brackets, separated by commas
`
-- let keyword -> similar to defining and loading
a = 1 <=> let a = 1
`
- list example
`
let lostNumbers = [4,8,15,16,23,42]

-- list of chars (char within single quotes) is same as strings (within double quotes)
['h', 'e', 'l', 'l', 'o'] <=> "hello"
`
- combine two lists
`
-- append at end
[1,2,3,4] ++ [5,6,7,8] => [1,2,3,4,5,6,7,8]
"hello" ++ " " ++ "world" => "hello world"
['h', 'e'] ++ ['l'] ++ ['l', 'o'] => "hello"
-- "++" operator basically walks thru all the elements of the list

-- add at the start -> use cons operator":"
'H':"askell" => "Haskell"
5:[1,2,3,4] => [5,1,2,3,4]

--- [1,2,3] <=> 1:2:3:[]
`
- get value from an index -> use "!!" and indexing starts from 0
`"Steve Jobs" !! 3 => 'v'
[9.4, 33.2, 96.5, 11.2, 23.25] !! 1 => 33.2
`
- lists are compared lexicographically (1 elements, then 2nd, then 3rd, etc)
- Other list functions
`
-- Can be done only if the list is not empty
head [3,4,5,2,1] => 3 -> returns 1st element
last [3,4,5,1,2] => 2 -> returns last element
tail [3,4,5,1,2] => [4,5,1,2] -> pops head and returns rest of the list (except 1st)
init [3,4,5,1,2] => [3,4,5,1] -> pops last and returns rest of the list (except last)

length [3,4,5,1,2] => 5 -> len of the list

null [3,2,1] <=> [3,2,1] == [] -> check if list is empty -> True if empty and False if not empty

reverse [3,4,5,1,2] => [2,1,5,4,3] -> reverses a list

take 3 [3,4,5,1,2] => [3,4,5] -> takes x number of elements from the beginning of the list (take 0 [any list] => [], take more than the list => the entire list)
drop 3 [3,4,5,1,2] => [1,2] -> drop x, drops x number of elememts from beginning of the list and returns the rest (drop 0 => entire list, drop more than list => [])

maximum [3,4,5,1,2] => 5 -> maximum of the list
minimum [3,4,5,1,2] => 1 -> minimum of the list

sum [3,4,5,1,2] => 15 -> sum of all elements in the list
product [3,4,5,1,2] => 120 -> product of all elements in the list

4 `elem` [3,4,5,1,2] => True -> checks if element is in the list, True if present, False if not

-- Ranges
[1..10] => [1,2,3,4,5,6,7,8,9,10]
['a'..'j'] => "abcdefghij"
['K'..'Z'] => "KLMNOPQRSTUVWXYZ"

[2,4..20] => [2,4,6,8,10,12,14,16,18,20] -- ranges with steps -> 1st 2 elements and then the upper limit
[20, 19..1] => to reverse list from 20 to 1 ([20..1] does not work)

-- floats in range are inaccurate
-- not specifying an upper-limit will give an inifinite list

-- cycle -> will cycle of the elements in the list for inifinite number of times. need to cut off them to display
take 10 (cycle [1,2,3]) => [1,2,3,1,2,3,1,2,3,1]
take 12 (cycle "LOL ") => "LOL LOL LOL "

take 10 (repeat 5) => [5,5,5,5,5,5,5,5,5,5] -> takes and repeats an element infinitely
replicate 3 10 => [10,10,10] => replicates y, x times
`
### List Comprehension
- Say for example;
	- A Set of first 10 even numbers -> S = { 2.x | x belongs to Natural Number, x <= 10}
	- Same can be written in Haskell as list comprehension as `[ x * 2 | x <- [1..10]]` => [2,4,6,8,10,12,14,16,18,20]
	- Say lets add a predicate for >= 12 => `[ x * 2 | x <- [1..10], x * 2 >= 12]` => [12,14,16,18,20]
- Example 2:
	- All numbers from 50 to 100, remainder when divided by 7 is 3
	- `[x | x <-[50..100], x `mod` 7 == 3]` => [52,59,66,73,80,87,94]
- Example 3:
	- Odd numbers > 10 -> "BANG!" | < 10 -> "BOOM!" | if not Odd throw away
	- boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x ]
- Example 4:
	- All numbers from 10 to 20, but not 13, 15, 19
	- `[x | x <- [10..20], x /=13, x/=15, x/=19]` => [10,11,12,14,16,17,18,20] -> '/= -> not equal to'
- Example 5:
	- All combination Product for [2,5,10] and [8,10,11]
	- `[x * y | x <- [2,5,10], y <- [8,10,11]]` => [16,20,22,40,50,55,80,100,110]
- Example 6: 
	- More than 50
	- `[x * y | x <- [2,5,10], y <- [8,10,11], x * y > 50] => [55,80,100,110]`
- Example 7:
	- All Adjective and Nouns
`
let nouns = ["hobo","frog","pope"]
let adjectives = ["lazy","grouchy","scheming"]
[ adjective ++ " " ++ noun | adjective <- adjectives, noun <- nouns ] => ["lazy hobo","lazy frog","lazy pope","grouchy hobo","grouchy frog",  
"grouchy pope","scheming hobo","scheming frog","scheming pope"]
`
- Example 8:
	- Own length function
	- `length' xlist = sum [ 1 | _ <- xlist ]` -> replace every element of list with 1 and adds thru sum function
- Example 9:
	- Remove Non-Upper Cases
	- `removeNonUpperCase st = [ c | c <- st, c `elem` ['A'..'Z'] ]`
- Example 10:
	- Remove all odds
`
let xxs = [[1,3,5,2,3,1,2,4,5],[1,2,3,4,5,6,7,8,9],[1,2,4,2,1,6,3,1,3,2,3,6]]
[ [ x | x <- xs, even x ] | xs <- xxs]
`

## Tuples
- Like Lists
- Known length
- Paranthesis enclosed
- Can combine types, heterogeneous types
- Cases where only x and y co-ordinates are used a list of list does not restrict from adding another co-ordinate
- Tuples will restrict, A tuple with 2 values (pairs) can be used, like `[(1,2),(8,11),(4,5)]`
- Adding another element to a tuple in the list of tuple will throw `Couldn't match expected type `(t, t1)' - against inferred type `(t2, t3, t4)'`

### Other functions
`
-- fst -> takes a pair and returns first component
fst (8,11) => 8
-- snd -> takes a pair and returns second component
snd (8,11) => 11

-- zip -> takes 2 lists and joins matching pairs 
zip [1,2,3,4,5] [5,5,5,5,5] =>[ (1,5),(2,5),(3,5),(4,5),(5,5) ]
zip [1 .. 5] ["one", "two", "three", "four", "five"] => [(1,"one"),(2,"two"),(3,"three"),(4,"four"),(5,"five")]

If lengths don't match longer list will cut off till shorter is matched
`

- Example: Triangles
`
-- sides < 10
let triangels = [ (a,b,c) | a <- [1..10], b <- [1..10], c <- [1..10] ]
-- assuming b is not > hypothenuse and a is not larger than b
let triangels = [ (a,b,c) | a <- [1..10], b <- [1..10], c <- [1..10], a^2 + b^2 == c^2  ]
-- perimeter is 24
let triangels = [ (a,b,c) | a <- [1..10], b <- [1..10], c <- [1..10], a^2 + b^2 == c^2, a + b + c == 24 ]
`

## Types and Type Classes
TBU















