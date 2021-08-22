# **Live coding session**

### **from Srdjan**

```ruby
# Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

p minSubLength([2,3,1,2,4,3], 7) == 2
p minSubLength([1, 10, 5, 2, 7], 9) == 1
p minSubLength([1, 11, 100, 1, 0, 200, 3, 2, 1, 250], 280) == 4
p minSubLength([1, 2, 4], 8) == 0

# Divisors of 42 are : 1, 2, 3, 6, 7, 14, 21, 42. These divisors squared are: 1, 4, 9, 36, 49, 196, 441, 1764. The sum of the squared divisors is 2500 which is 50 * 50, a square!

# Given two positive integers we want to find all integers between them whose sum of squared divisors is itself a square. 42 is such a number.

# The result will be an array of arrays, each subarray having two elements, first the number whose squared divisors is a square and then the sum of the squared divisors.

=begin
def retrieve_divisors(num)
  divisors = []
  1.upto(num).each do |n|
    divisors << n if ((num % n) == 0)
  end
  divisors
end

def sum_of_squared_nums(arr)
  arr.map { |num| num*num}.reduce(:+)
end

def find_root(num)
  1.upto(num).each do |number|
    return number if number*number == num
    break if number*number > num
  end
  nil
end

def list_squared(start_num, end_num)
  list = []
  start_num.upto(end_num).each do |num|
    divisors = retrieve_divisors(num)
    sum = sum_of_squared_nums(divisors)
    root = find_root(sum)
    list << [num, sum] if root
  end
  list
end
=end

p list_squared(1, 250) == [[1, 1], [42, 2500], [246, 84100]]
p list_squared(42, 250) == [[42, 2500], [246, 84100]]
p list_squared(250, 500) == [[287, 84100]]

# You are given an array which contains only integers (positive and negative). Your job is to sum only the numbers that are the same and consecutive. The result should be one array.

# You can asume there is never an empty array and there will always be an integer.

p sum_consecutives([1,4,4,4,0,4,3,3,1, 1]) == [1,12,0,4,6,2]
p sum_consecutives([1,1,7,7,3]) == [2,14,3]
p sum_consecutives([-5,-5,7,7,12,0]) ==  [-10,14,12,0]
```



### **from David**

###### **Exercise 1**

```ruby
# You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

# Implement a function likes :: [String] -> String, which must take in input array, containing the names of people who like an item. It must return the display text as shown in the examples:

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Array of strings
  -
  -
Output:
  - String with interpolation
  -
  
=====> Rules
Explicit Requiremnts:
  - Empty array allowed
  - return "no one liked this" if an empty array is passed as an argument

Implicit Requiremnts:
  - Just strings as elements. no other data type or special characters
  - and should be used in the final string for the last element interpolated
  - # For 4 or more names, the number in and 2 others simply increases.

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
likes [] -- must be "no one likes this"
 - empty array when no input is given
 
likes ["Peter"] -- must be "Peter likes this"
 - When there is one name only just interpolate the name without and

likes ["Jacob", "Alex"] -- must be "Jacob and Alex like this"
 - When there are 2 names then seperate them with an 'and'
 
likes ["Max", "John", "Mark"] -- must be "Max, John and Mark like this"
- when there are 3 names seperate each name by comma, except the last name which is seperated by an 'and'

likes ["Alex", "Jacob", "Mark", "Max"] -- must be "Alex, Jacob and 2 others like this"
 - when there are 4+ names then seperate the first two by comma and use the 'and' Sting followed by the count of the number of remaining names.

=====> Data structure(s):
Input: array
Intermediate: conditional statement
Output: string interpolated 

=====> Algorithm:
given an arry of names as strings.
find the number of names and iterpolate them based on the rules from above.

=====> Optional Implementation (Pseudo-code):

=end


def likes(arr)
  return "no one likes this" if arr.empty?
  answer = ""
    
  
  if arr.count == 1
    answer = "#{arr[0]} likes this"
  elsif arr.count == 2
    answer = "#{arr[0]} and #{arr[1]} like this"
  elsif arr.count == 3
    answer = "#{arr[0]}, #{arr[1]} and #{arr[2]} like this"
  elsif arr.count > 3
    answer = "#{arr[0]}, #{arr[1]} and #{arr.count - 2} others like this"
  end
  answer
end


p likes [] == "no one likes this"
p likes ["Peter"] == "Peter likes this"
p likes ["Jacob", "Alex"] == "Jacob and Alex like this"
p likes ["Max", "John", "Mark"] == "Max, John and Mark like this"
p likes ["Alex", "Jacob", "Mark", "Max"] == "Alex, Jacob and 2 others like this"

```

### **From Chris B.**

###### **Exercise 1**

```ruby
# Given a string, concatenate into a new string with case-insensitive alphabetical 
# order of appeareance. Whitespace and punctuation shall be removed.

def split_str(str)
  str.scan(/\w/i).sort_by {|e| e.downcase }
end

def alphabetized(str)
  split_str(str).join
end

p alphabetized("Riaz Ahamed Naina") == "aAaaadehiimNnRz"
```



###### **Exercise 2: Need to practice**

```ruby
# If you take a number like 735291, and rotate it to the left, you get 352917. If you now keep the first digit fixed in place, and rotate the remaining digits, you get 329175. Keep the first 2 digits fixed in place and rotate again to 321759. Keep the first 3 digits fixed in place and rotate again to get 321597. Finally, keep the first 4 digits fixed in place and rotate the final 2 digits to get 321579. The resulting number is called the maximum rotation of the original number.

# Write a method that takes an integer as argument, and returns the maximum rotation of that argument. You can (and probably should) use the rotate_rightmost_digits method from the previous exercise.

# Note that you do not have to handle multiple 0s.

=begin
========== THE PEDAC PROCESS ==========

=====> Problem: Maximum number of rotation
Input:
  - interger
  -
Output:
  - max rotated integer
  -

=====> Rules
Explicit Requiremnts:
  - final integer with each integer rotated 
  - when there is one integer . return the integer
Implicit Requiremnts:
  - no zeros or any other data types as arguments
  - no special characters
  - # the leading zero gets dropped

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
  max_rotation(735291) == 321579
  step1 735291 - first integer is rotated
  step2 352917 - 1st fixed second is rotated to the back
  step3 329175 - 1st and 2nd fixed
  step4 321759 - 1st, 2nd and 3rd fixed

  step5 321597 - 1st, 2nd, 3rd aand 4th fixed
  step6 321579 - 1st, 2nd, 3rd,  4th and 5th (which is length -1 ) fixed
  
  max_rotation(3) == 3
  when there is one integer . return the integer
  
  max_rotation(35) == 53
  just rotate once
  
  
  max_rotation(105) == 15 # the leading zero gets dropped
  
  
  max_rotation(8_703_529_146) == 7_321_609_845 

=====> Data structure(s):
Input: integer
Intermediate: string, array
Output: integer

=====> High Level Algorithm:

return the integer if integer < 10
convert the integer into an array of strings of digits. Iterate through the index while moving the current element to the back  

Keep 

=====> Optional Implementation (Pseudo-code):

=end

def split_number(num)
  num.digits.reverse.map(&:to_s)
end

def rotate_items(num)
  counter = 0
  new_arr = split_number(num)
  loop do
    break if counter >= new_arr.length - 1
    second_element = new_arr.delete_at(counter) # removes element at current index
    new_arr << second_element # pushes deleted element to end of array
    counter += 1
  end
  new_arr.join.to_i

end

def max_rotation(num)
  # split_number(num)
  rotate_items(num)
end

# Example:
p max_rotation(735291) #== 321579
# p max_rotation(3) #== 3
# p max_rotation(35) #== 53
# p max_rotation(105) #== 15 # the leading zero gets dropped
# p max_rotation(8_703_529_146) #== 7_321_609_845

# My solution
def max_rotation(num)
  arr = num.digits.reverse.map(&:to_s)
  arr.each_with_index { |_, idx| arr << arr.delete_at(idx) }.join.to_i
end
```

###### **Exercise 3: Anagrams** 

```ruby
=begin
Given the array...

Copy Code
words =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
          'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
          'flow', 'neon']
Write a program that prints out groups of words that are anagrams. Anagrams are words that have the same exact letters in them but in a different order. Your output should look something like this:

Copy Code
["demo", "dome", "mode"]
["neon", "none"]
#(etc)
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Given a array of strings. 
  -
  -
Output:
  - collect the anagrams into subarry and print the subaarray on different lines
  -

=====> Rules
Explicit Requiremnts:
  - all of the words have the same length
  - all the words are lower case
Implicit Requiremnts:
  - no special characters or other datatypes
  - no upper case
  - unmatched anagrams allowed but not printed out

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
words =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
          'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
          'flow', 'neon']
          
          ["demo", "dome", "mode"]
          ["neon", "none"]
          [evil, vile, live, veil]
          [tied, diet, edit, tide]
          [wolf, flow, fowl]

=====> Data structure(s):
Input: array
Intermediate: array, string
Output: array of anagrams

=====> High Level Algorithm:
  - Iterate through the collection of words and collect anagrams of a word to a subarray
  

=====> Optional Implementation (Pseudo-code):
create a new hash 'hsh'
iterate through the array and for every iteration
  check if hsh has the anagram of the current element (eg; "dome" => ["demo", "dome", "mode"])
    if yes then append the current element to the value which is an array of anagrams for the key
    if no then create a new key with the value as an array having the current element 
  return the values of `hsh`

=end

words1 =  ['demo', 'dome', 'mode', 'live', 'mod', 'demoo']
words2 =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
 'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
 'flow', 'neon']

def group_anagrams(words)
  
  result = words.each_with_object(Hash.new) do |ele, hsh|
    sorted_ele = ele.chars.sort.join
    hsh.has_key?(sorted_ele) ? hsh[sorted_ele] << ele : hsh[sorted_ele] = [ele]
  end
  result.select { |_, value| value.length > 1 }.values
end

p group_anagrams(words1) == [["demo", "dome", "mode"]] # => ["demo", "dome", "mode"]
p group_anagrams(words2) == [["demo", "dome", "mode"], ["none", "neon"],
                            ["tied", "diet", "edit", "tide"],
                            ["evil", "live", "veil", "vile"],
                            ["fowl", "wolf", "flow"]
                          ]
```

###### **Example 4**

```ruby
=begin

If


sz is greater (>) than the length of str it is impossible to take a chunk of size sz hence return "".
Examples:
revrot("123456987654", 6) --> "234561876549"
revrot("123456987653", 6) --> "234561356789"
revrot("66443875", 4) --> "44668753"
revrot("66443875", 8) --> "64438756"
revrot("664438769", 8) --> "67834466"
revrot("123456779", 8) --> "23456771"
revrot("", 8) --> ""
revrot("123456779", 0) --> "" 
revrot("563000655734469485", 4) --> "0365065073456944"
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
The input is a string str of digits. Cut the string into chunks (a chunk here is a substring of the initial string) of size sz (ignore the last chunk if its size is less than sz).

If a chunk represents an integer such as the sum of the cubes of its digits is divisible by 2, reverse that chunk; otherwise rotate it to the left by one position. Put together these modified chunks and return the result as a string.

Input: string and integer

Output: string

=====> Rules
Explicit Requiremnts:
  - first arg is a string, second arg == Integer (sz)
  - sz > str.length ------> ""
  - sz is <= 0 or if str is empty return ""
  
Implicit Requiremnts:
  - can be an empty string (1st argument)
  - 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p revrot("1234", 0) == ""

p revrot("", 0) == ""
empty string == 0

p revrot("1234", 5) == ""
sz > str.length

p revrot("733049910872815764", 5) == "330479108928157"
"73304 === 33047
99108  === 91089
72815  === 28157
764" - ignore this < sz

p revrot("123456987654", 6) == "234561876549"

p revrot("123456987653", 6) == "234561356789"

p revrot("66443875", 4) == "44668753"
6644 === 4466 - sum of the cubes of the induvidual digits / 2 true hence reverse
3875 === 8753

p revrot("66443875", 8) == "64438756"

p revrot("664438769", 8) == "67834466"

p revrot("123456779", 8) == "23456771"

p revrot("", 8) == ""

p revrot("123456779", 0) == ""

p revrot("563000655734469485", 4) == "0365065073456944"


=====> Data structure(s):
Input: string, integer
Intermediate: array 
Output: string

=====> High Level Algorithm:
Split the string into chunks equal in length to the second argument. Reverse the chunk when the sum of the cubes of its digits is divisible by 2. Otherwise rotate the first number to the last. Join all the chunk and return the string.

=====> Optional Implementation (Pseudo-code):
method -----> revrot(str, sz) -----> String

return "" if sz > str.length or  sz is <= 0

- initialize arr to the return of the method to split str into chunks equal in length to sz
  - split str into invidual string
  - split the string into lengths of sz
  - reject chunk < sz in length

- check if the sum of the cube of digits is divisible by 2
  - iterate through the array while mutating and reverse the elements whose the sum of the cube of digits is divisible by 2
  - if not divisible then shift the first digit to the last of the element
  
join all the elements and return the string
  
=end

# Code With Intent

def chunk_string(str, sz)
  str.chars.each_slice(sz).to_a.select { |ele| ele.length == sz } 
end

def divide_two?(integer_arr)
  integer_arr.map { |num| num ** 3 }.sum % 2 == 0
end

def divisible_two(arr)
  arr.map do |sub_arr|
    integer_arr = sub_arr.map(&:to_i)
    divide_two?(integer_arr) ? integer_arr.map(&:to_s).reverse : integer_arr.rotate
  end
end  

def revrot(str, sz)
  return "" if sz > str.length || sz <= 0
  arr = chunk_string(str, sz)
  divisible_two(arr).flatten.join
end

p revrot("1234", 0) == ""
p revrot("", 0) == ""
p revrot("1234", 5) == ""
p revrot("733049910872815764", 5) == "330479108928157"
p revrot("123456987654", 6) == "234561876549"
p revrot("123456987653", 6) == "234561356789"
p revrot("66443875", 4) == "44668753"
p revrot("66443875", 8) == "64438756"
p revrot("664438769", 8) == "67834466"
p revrot("123456779", 8) == "23456771"
p revrot("", 8) == ""
p revrot("123456779", 0) == ""
p revrot("563000655734469485", 4) == "0365065073456944"

```

###### **Example5**

```ruby
=begin
-----------------------INSTRUCTIONS--------------------------------------
# Divisors of 42 are : 1, 2, 3, 6, 7, 14, 21, 42. These divisors squared are: 1, 4, 9, 36, 49, 196, 441, 1764. The sum of the squared divisors is 2500 which is 50 * 50, a square!

# Given two positive integers we want to find all integers between them whose sum of squared divisors is itself a square. 42 is such a number.

# The result will be an array of arrays, each subarray having two elements, first the number whose squared divisors is a square and then the sum of the squared divisors.

--------------------------PROBLEM----------------------------------------
Questions:
Input: 2 Integers, representing a range of numbers
Output: 1 Array of arrays, each sub_array will contain; 
          -the numbers whose squared divisors is a square
          -sum of the squared divisors

---------------------------RULES-----------------------------------------
Explicit:
  -Given integers will be positive
  -find all integers between given integers whose sum of squared divisors is a square
    -find all divisors of a number
    -find the sum of all divisors squared
    -if the sum if a perfect square --> include array of number and sum of squared divisors
Implicit:
  -inputs will not be empty
  -will always be a integer (whole number)

--------------------------EXAMPLES---------------------------------------
p list_squared(42, 250) == [[42, 2500], [246, 84100]]
42..250
42 divisors --> 1, 2, 3, 6, 7, 14, 21, 42
squares of divisors --> 1, 4, 9, 36, 49, 196, 441, 1764
sum of squared divisors --> 2500
2500 if a square of 50! (50 * 50 == 2500)
returns ==> [42, 2500]

----------------------------ALGO-----------------------------------------
==> For each integer within the range of integers given as arguments, check to see if all of the divisors of the integers, when squared and added together is the product of a square. 

-- method --> list_squared(integer1, integer2) --> 1 Array of Arrays
  -intialize 'squared' to an empty array
  -iterate through the range of numbers given as arguments
    -find divisors of the current integer (divisors)
    -if divisors squared and added together form the product of a square
      -push sub_array to 'squared'
  -return 'squared'
    
-- method --> find_divisors(integer) --> array
  -initialize 'divisors' as empty array
  -iterate through all numbers between 1 and the given integer
    -initialize 'square' to current number can be divided evenly into given number
    -if 'square' is truthy
      -push current element and square to 'divisors'
  -return 'divisors'
  
-- method --> square_product(array) --> integer or nil
  -transform all elements of given array to themselves squared
  -find sum of all sqaured divisors
  -if sum is a product of aperfect square
    -return square
  -otherwise
    -return nil

=end

def find_divisors(num)
  divisors = []
  1.upto(num) do |current_num|
    divisors << current_num if num % current_num == 0
  end
  divisors
end

def square_product(array)
  squared = array.map { |num| num * num }.sum
  if Math.sqrt(squared) % 1 == 0
    squared
  end
end

def list_squared(start_num, end_num)
  squared = []
  start_num.upto(end_num) do |num|
    divisors = find_divisors(num)
    if square_product(divisors)
      squared << [num, square_product(divisors)]
    end
  end
  squared
end

p list_squared(1, 250) == [[1, 1], [42, 2500], [246, 84100]]
p list_squared(42, 250) == [[42, 2500], [246, 84100]]
p list_squared(250, 500) == [[287, 84100]]
```



### from MED

###### ex1

```ruby
=begin
Sort the given array of strings in alphabetical order, case insensitive. For example:

["Hello", "there", "I'm", "fine"]  -->  ["fine", "Hello", "I'm", "there"]
["C", "d", "a", "B"])              -->  ["a", "B", "C", "d"]
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Sort the given array of strings in alphabetical order, case insensitive. For example:

Input: array

Output: array

=====> Rules
Explicit Requiremnts:
  - case insensitive
  - sort alphabetically
Implicit Requiremnts:
  - no empty string
  - no other datatypes

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
["Hello", "there", "I'm", "fine"]  -->  ["fine", "Hello", "I'm", "there"]


["C", "d", "a", "B"])              -->  ["a", "B", "C", "d"]

=====> Data structure(s):
Input: array
Intermediate:n/a
Output: array

=====> High Level Algorithm:
given an array of strings, arrange them in alphabetical order ignoring the case of the elements

=====> Optional Implementation (Pseudo-code):
alpha(arr) ------> array

Loop through the array and compare the current element downcased with the next element downcased. 
 if equal retain the position 
 if equates to -1 then keep the current element in its position
 if equates to +1 THEN swap the position
 
 do this for all elements ignoring the case
 return the sorted array

=end

# Code With Intent


def alpha(arr)
  arr.sort { |a, b| a.downcase <=> b.downcase }
end

array_1 = ["Hello", "there", "I'm", "fine"] 
array_2 = ["C", "d", "a", "B"]

p alpha(array_1) == ["fine", "Hello", "I'm", "there"]
p alpha(array_2) == ["a", "B", "C", "d"]

```

###### ex2

```ruby
=begin
#Find the missing letter

Write a method that takes an array of consecutive (increasing) letters as input and that returns the missing letter in the array.

You will always get an valid array. And it will be always exactly one letter be missing. The length of the array will always be at least 2.
The array will always contain letters in only one case.

Example:

['a','b','c','d','f'] -> 'e' ['O','Q','R','S'] -> 'P'

["a","b","c","d","f"] -> "e"
["O","Q","R","S"] -> "P"
(Use the English alphabet with 26 letters!)

Have fun coding it and please don't forget to vote and rank this kata! :-)

I have also created other katas. Take a look if you enjoyed this kata!
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Write a method that takes an array of consecutive (increasing) letters as input and that returns the missing letter in the array. 

Input: array of letters

Output: missing letter - string

=====> Rules
Explicit Requiremnts:
  - all the letters will be the same case
  - min 2 elements in the array
Implicit Requiremnts:
  - the missing letter is always between the first and the last element
  - there is no empty string or any other datatype
  - return string will match the same case as the other elements in the array

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p find_missing_letter(["a","b","c","d","f"]) == "e"

p find_missing_letter(["O","Q","R","S"]) == "P"

p find_missing_letter(["b","d"]) == "c"

p find_missing_letter(["a","b","d"]) == "c"

p find_missing_letter(["b","d","e"]) == "c"
 

=====> Data structure(s):
Input: array
Intermediate: array
Output: string

=====> High Level Algorithm:
iterate over the sequence of elements within the array and find the missing element in teh sequence

=====> Optional Implementation (Pseudo-code):
find_missing_letter(arr) -----> string

- create a new array 'str_arr' - ranging from arr[0] to arr[-1]
- compare str_arr.join with arr.join and return the unmatched element in a new arr
- print the first unmatched element from the returned array 
=end

# Code With Intent

def str_arr(arr)
  (arr[0]..arr[-1]).to_a.join
end

def find_missing_letter(arr)
  str_arr(arr).scan(/[^#{arr.join}]/).first
end

p find_missing_letter(["a","b","c","d","f"]) == "e"
p find_missing_letter(["O","Q","R","S"]) == "P"
p find_missing_letter(["b","d"]) == "c"
p find_missing_letter(["a","b","d"]) == "c"
p find_missing_letter(["b","d","e"]) == "c"
```

###### ex3

```ruby
=begin
Consider the range 0 to 10. 
The primes in this range are: 2, 3, 5, 7, and thus the prime pairs are: (2,2), (2,3), (2,5), (2,7), (3,3), (3,5), (3,7),(5,5), (5,7), (7,7).

Let's take one pair (2,7) as an example and get the product, then sum the digits of the result as follows: 2 * 7 = 14, and 1 + 4 = 5. 
We see that 5 is a prime number. Similarly, for the pair (7,7), we get: 7 * 7 = 49, and 4 + 9 = 13, which is a prime number.

You will be given a range and your task is to return the number of pairs that revert to prime as shown above. 
In the range (0,10), there are only 4 prime pairs that end up being primes in a similar way: (2,7), (3,7), (5,5), (7,7). Therefore, solve(0,10) = 4)

Note that the upperbound of the range will not exceed 10000. A range of (0,10) means that: 0 <= n < 10.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: 2 Integer arguments defining the range 

Output: Integer

=====> Rules
Explicit Requiremnts:
  - Select only prime numbers
  -
Implicit Requiremnts:
  - only positive numbers
  - 0 allowed

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solve(0,10) = 4
(2,2 = 4), (2,3 = 6) , (2,5 = 10), (2,7 = 14), (3,3 = 9), (3,5 = 15), (3,7 = 21),(5,5 = 25), (5,7 = 35), (7,7 = 49)
(2,7 = 1 + 4 = 5), (3,7 = 2 + 1 = 3), (5,5 = 2 + 5 = 7) (7,7 = 4 + 9 = 13) === 4

p solve(0,20) == 14
p solve(2,200) == 457
p solve(2,2000) == 17705
p solve(1000,3000) == 12801

=====> Data structure(s):
Input: integers
Intermediate:
Output:

=====> High Level Algorithm:

=====> Optional Implementation (Pseudo-code):
solve(num1,num2)  = Integer

- create a new array arr ranging from num1 to num2
- select the primes from arr into a new arr prime_arr
    - create a method select_prime(arr) that checks for prime numbers 
- create pairs of the primes in a new arr

- transform the elemnts by multiplying the pairs to give the new element in the transfoemed array 
- add each digit of the elements in the transformed array to give a new element.
    select the elements that are prime numbers
- count the number of prime numbers within the final array
- return the count



-----------------------------------------
a = [2, 3, 5, 7]   
arr = []

(0...a.size).each do |index_1|
  (index_1...a.size).each do |index_2|
    arr << [a[index_1], a[index_2]]
  end
end

p arr




(2,2), (2,3), (2,5), (2,7), (3,3), (3,5), (3,7),(5,5), (5,7), (7,7).
----------------------------------





=end

# Code With Intent

# def select_prime(arr)
#   new_arr = arr.select do |ele|
#     next if ele == 1
#     ele.remainder(2) != 0 && ele.remainder(3) != 0
#   end
#   new_arr.unshift(2) if arr.include?(2)
#   new_arr.unshift(3) if arr.include?(3)
#   new_arr.sort
# end

def prime?(num)
  return false if num < 2
  
  (2...num).each do |int|
    return false if num % int == 0
  end
  
  true 
end

def create_pair(prime_arr)
  arr = []
  a = prime_arr
  (0...a.size).each do |index_1|
    (index_1...a.size).each do |index_2|
      arr << [a[index_1], a[index_2]]
    end
  end
  arr
end

def solve(num1, num2)
  arr = (num1..num2).to_a
  
  prime_arr = arr.select {|ele|  prime?(ele) }
  transformed_arr = create_pair(prime_arr).map { |ele| ele.reduce(:*).digits.sum }
  transformed_arr.select {|ele|  prime?(ele) }.count
  
end


p solve(0,10) == 4
p solve(0,20) == 14
p solve(2,200) == 457
p solve(2,2000) == 17705
p solve(1000,3000) == 12801




# a = [2, 3, 5, 7]   
# arr = []
# # a.each_with_index { |e, i| arr << a[i],  }

```

###### ex4

```ruby
=begin
Once upon a time, on a way through the old wild mountainous west,…
… a man was given directions to go from one point to another. The directions were "NORTH", "SOUTH", "WEST", "EAST". Clearly "NORTH" and "SOUTH" are opposite, "WEST" and "EAST" too.

Going to one direction and coming back the opposite direction right away is a needless effort. Since this is the wild west, with dreadfull weather and not much water, it's important to save yourself some energy, otherwise you might die of thirst!

How I crossed a mountainous desert the smart way.
The directions given to the man are, for example, the following (depending on the language):

["NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"].

You can immediatly see that going "NORTH" and immediately "SOUTH" is not reasonable, better stay to the same place! So the task is to give to the man a simplified version of the plan. A better plan in this case is simply:

["WEST"]

Other examples:
In ["NORTH", "SOUTH", "EAST", "WEST"], the direction "NORTH" + "SOUTH" is going north and coming back right away.

The path becomes ["EAST", "WEST"], now "EAST" and "WEST" annihilate each other, therefore, the final result is [] (nil in Clojure).

In 

, "NORTH" and "SOUTH" are not directly opposite but they become directly opposite after the reduction of "EAST" and "WEST" so the whole path is reducible to ["WEST", "WEST"].

Task
Write a function dirReduc which will take an array of strings and returns an array of strings with the needless directions removed (W<->E or S<->N side by side).

See more examples in "Sample Tests:"
Notes
Not all paths can be made simpler. The path ["NORTH", "WEST", "SOUTH", "EAST"] is not reducible. "NORTH" and "WEST", "WEST" and "SOUTH", "SOUTH" and "EAST" are not directly opposite of each other and can't become such. Hence the result path is itself : ["NORTH", "WEST", "SOUTH", "EAST"].
=end


=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: array of directions

Output: array of dirtections simplified

=====> Rules
Explicit Requiremnts:
  - north south occuring immediately removes each other
  - east west occuring immediately removes each other
  -
Implicit Requiremnts:
  - only directions
  - no other data type

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
a = ["NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"]
p direduc(a) ==  ["WEST"]
["NORTH", "SOUTH", 
"SOUTH", ("EAST", "WEST"), "NORTH", "WEST"]
"SOUTH", (), "NORTH", "WEST"]
 "WEST"]

u = ["NORTH", "WEST", "SOUTH", "EAST"]
p direduc(u) == ["NORTH", "WEST", "SOUTH", "EAST"]
no cancellation as they do not occur in pairs

b = ["NORTH", "EAST", "WEST", "SOUTH", "WEST", "WEST"]
p direduc(b) == ["WEST", "WEST"]

=====> Data structure(s):
Input: array
Intermediate: array, hash
Output: array

=====> High Level Algorithm:
iterate through the array and simplify the array by removing NORT/SOUTH pairs and EAST/WEST pairs in sequence. Return the simplified array

=====> Optional Implementation (Pseudo-code):

direduc(arr)

Initialize hsh = { "NORTH" => "SOUTH", "SOUTH" => "NORTH", "EAST" => "WEST", "WEST" => "EAST" }
initialilze check_arr = []

Iterate thoroujgh arr 
  - pass each element and compare ther current element with the previous element
  - if hsh[current_element] == check_arr[-1]
      delete checck_arr[-1]
    repeat untill the last element
  return check_array

=end

# Code With Intent

def direduc(arr)
  hsh = { "NORTH" => "SOUTH", "SOUTH" => "NORTH", "EAST" => "WEST", "WEST" => "EAST" }
  check_arr = []
  
  (0...arr.length).each do |idx|
    if hsh[check_arr[-1]] == arr[idx]
      check_arr.pop
    else 
      check_arr << arr[idx]
    end
  end
  check_arr
end
  
a = ["NORTH", "SOUTH", "SOUTH", "EAST", "WEST", "NORTH", "WEST"]
p direduc(a) ==  ["WEST"]
u = ["NORTH", "WEST", "SOUTH", "EAST"]
p direduc(u) == ["NORTH", "WEST", "SOUTH", "EAST"]
b = ["NORTH", "EAST", "WEST", "SOUTH", "WEST", "WEST"]
p direduc(b) == ["WEST", "WEST"]
```

###### ex5

```ruby
=begin
Your task is to Reverse and Combine Words. It's not too difficult, but there are some things you have to consider...

So what to do?
Input: String containing different "words" separated by spaces

1. More than one word? Reverse each word and combine first with second, third with fourth and so on...
   (odd number of words => last one stays alone, but has to be reversed too)
2. Start it again until there's only one word without spaces
3. Return your result...
Some easy examples:
Input:  "abc def"
Output: "cbafed"

Input:  "abc def ghi 123"
Output: "defabc123ghi"

Input:  "abc def gh34 434ff 55_eri 123 343"
Output: "43hgff434cbafed343ire_55321"
I think it's clear?! First there are some static tests, later on random tests too...

Hope you have fun! :-)
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: string

Output:string

=====> Rules
Explicit Requiremnts:
  - More than one word? Reverse each word and combine first with second, third with fourth and so on...
   (odd number of words => last one stays alone, but has to be reversed too)
  -
Implicit Requiremnts:
  -
  - when ther is one string with no space just return the string

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p reverse_and_combine_text("abc def") == "cbafed"

p reverse_and_combine_text("abc def ghi jkl") == "defabcjklghi"
#### "abc def ghi jkl"
step 1: cba fed ihg lkj
step 2 - cbafed ihgljk
step 3 - defabc kjlghi
step 4 - defabckjlghi
p reverse_and_combine_text("sdfsdf wee sdffg 342234 ftt") == "gffds432243fdsfdseewttf"

### "sdfsdf wee sdffg 342234 ftt"
step 1 - fdsfds eew gffds 432243 ttf
step 2 - fdsfdseew gffds432243 ttf
step 3 - weesdfsdf 342234sdffg ftt
step 4 - weesdfsdf342234sdffg ftt
step 5 - gffds432243fdsfdseew ttf
step 6 - gffds432243fdsfdseewttf

p reverse_and_combine_text("dfghrtcbafed") == "dfghrtcbafed"

p reverse_and_combine_text("234hh54 53455 sdfqwzrt rtteetrt hjhjh lllll12  44") == "trzwqfdstrteettr45hh4325543544hjhjh21lllll"

p reverse_and_combine_text("sdfsdf wee sdffg 342234 ftt") == "gffds432243fdsfdseewttf"

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
Reverse and Combine Words untill the string becomes one with no space

=====> Optional Implementation (Pseudo-code):
reverse_and_combine_text(str)

initialize split_str = str.split
return split_str.first if split_str.count == 1

create_pairs(split_str) Subprocess
  - reverse all the induvidual items
  - split the array into pairs.
  - combine the pairs leaving the odd one alone
  - do this until there is one string only
  - return the string

=end

# Code With Intent

def create_pairs(split_str)
  loop do 
    break if split_str.length == 1
    split_str.map!(&:reverse)
    split_str = split_str.each_slice(2).map { |array| array.join }
  end
  split_str.first
end

def reverse_and_combine_text(str)
  split_str = str.split
  return split_str.first if split_str.count == 1
  
  create_pairs(split_str)
end
 
p reverse_and_combine_text("abc def") == "cbafed"
p reverse_and_combine_text("abc def ghi jkl") == "defabcjklghi"
p reverse_and_combine_text("dfghrtcbafed") == "dfghrtcbafed"
p reverse_and_combine_text("234hh54 53455 sdfqwzrt rtteetrt hjhjh lllll12  44") == "trzwqfdstrteettr45hh4325543544hjhjh21lllll"
p reverse_and_combine_text("sdfsdf wee sdffg 342234 ftt") == "gffds432243fdsfdseewttf"
```

###### ex6: 

```ruby
=begin
In this Kata, we are going to see how a Hash (or Map or dict) can be used to keep track of characters in a string.

Consider two strings "aabcdefg" and "fbd". How many characters do we have to remove from the first string to get the second string? Although not the only way to solve this, we could create a Hash of counts for each string and see which character counts are different. That should get us close to the answer. I will leave the rest to you.

For this example, solve("aabcdefg","fbd") = 5. Also, solve("xyz","yxxz") = 0, because we cannot get second string from the first since the second string is longer.

More examples in the test cases.

Good luck!p 
p solve("xyz","yxz") == 0
p solve("abcxyz","ayxz") == 2
p solve("abcdexyz","yxz") == 5
p solve("xyz","yxxz") == 0
p solve("abdegfg","ffdb") == 0
p solve("aabcdefg","fbd") == 5
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: strings

Output: integer

=====> Rules
Explicit Requiremnts:
  - 2nd string > 1st string return 0
  - when the 2nd string cant be formed return 0
  - Hash
Implicit Requiremnts:
  - lowercasse / case sensitve???
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solve("abcxyz","ayxz") == 2
abcxyz - remove b c 

p solve("abcdexyz","yxz") == 5
a b c d e 
p solve("xyz","yxxz") == 0
 2nd string > 1st string return 0
p solve("abdegfg","ffdb") == 0
cant form 2nd string

p solve("aabcdefg","fbd") == 5
aaceg.count = 5

=====> Data structure(s):
Input: string
Intermediate: hash, array??
Output: integer

=====> High Level Algorithm:
rturn the number of items needed to be deleted in 1st argument to give second arg
else retrun 0

=====> Optional Implementation (Pseudo-code):
solve(str1, str2)

initialize str1_hsh = str1.chars.tally
initialize str2_hsh = str2.chars.tally

iterate through str2_hsh 
  - check if str1_hsh has the key in it
  - if yes then subtract str1_hsh[key] -= str2_hsh[key]
  - otherwise return 0
str1_hsh.values.include?(-1) then return 0
str1_hsh.values.sum

=end

# Code With Intent

def solve(str1, str2)
  str1_hsh = str1.chars.tally
  str2_hsh = str2.chars.tally
  
  str2_hsh.each do |k, v|
    str1_hsh.keys.include?(k) ?  str1_hsh[k] -= str2_hsh[k] : 0
  end
  str1_hsh.values.include?(-1) ? 0 : str1_hsh.values.sum
end

### option 2
def solve(str1, str2)
  str2.chars.all? { |char| str1.sub!(char, '') } ? str1.size : 0
end

p solve("abcxyz","ayxz") == 2
p solve("abcdexyz","yxz") == 5
p solve("xyz","yxxz") == 0
p solve("abdegfg","ffdb") == 0
p solve("aabcdefg","fbd") == 5
```



### **My personal sets**

###### **Exercises**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: two string arguments
  -
  -
Output:
  - uncommon characters in the string
  -

=====> Rules
Explicit Requiremnts:
  - comparing two string arguments
  - 
Implicit Requiremnts:
  - no special characters
  - no empty strings
  - no integers or any other data types

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p unique_string_characters("xyab","xzca") #== "ybzc"
 - uncommon strings in both argument 1 and 2

p unique_string_characters("a","z") #== "az"
 - uncommon strings in both argument 1 and 2
 
p unique_string_characters("abcd","de") #== "abce"
 - uncommon strings in both argument 1 and 2
 
p unique_string_characters("abc","abba") #== "c"
 - uncommon strings in both argument 1 and 2 and repeated common characters ignored

p unique_string_characters("xyz","zxy") 
 - When there are no uncommon characters return an empty string

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
- compare the 2 given string arguments and return a new array comprising of the all the uncommon characters between the two strings collectively. Ignore any repeated common characters and return "" an empty string if there are no comon characters

=====> Optional Implementation (Pseudo-code):

=end

def unique_string_characters(str1, str2)
  (
    str1.scan(/[^#{str2}]/) + 
    str2.scan(/[^#{str1}]/)
  ).join
end

p unique_string_characters("xyab","xzca") == "ybzc"
p unique_string_characters("a","z") == "az"
p unique_string_characters("abcd","de") == "abce"
p unique_string_characters("abc","abba") == "c"
p unique_string_characters("xyz","zxy") == ""
```



---

# **21 questions**

### **qns** 

```ruby
#### Problems to solve
1) Find the longest substring in alphabetical order.
Example: the longest alphabetical substring in “asdfaaaabbbbcttavvfffffdf” is
“aaaabbbbctt”.
The input will only consist of lowercase characters and will be at least one
letter long.
  
2) Capitalize every second character of every third word of a given string.

to_weird_case("Lorem Ipsum is simply dummy text of the printing") == "Lorem Ipsum 
iS simply dummy tExT of the pRiNtInG"
to_weird_case("It is a long established fact that a reader will be 
distracted") == "It is a long established fAcT that a rEaDeR will be dIsTrAcTeD"
to_weird_case("aaA bB c") == "aaA bB c"
to_weird_case("Miss Mary Poppins word is supercalifragilisticexpialidocious") == 
"Miss Mary POpPiNs word is sUpErCaLiFrAgIlIsTiCeXpIaLiDoCiOuS"

3) Longest vowel chain:
The vowel substrings in the word “codewarriors” are ‘o’,‘e’,‘a’,‘io’. The
longest of these has a length of 2.
Given a lowercase string that has alphabetic characters only and no spaces,
return the length of the longest vowel substring. Vowels are any of aeiou.

def solve(str)
  str.scan(/[aeiou]+/).map(&:length).max
end

p solve("codewarriors") == 2
p solve("suoidea") == 3
p solve("iuuvgheaae") == 4
p solve("ultrarevolutionariees") == 3
p solve("strengthlessnesses") == 1
p solve("cuboideonavicuare") == 2
p solve("chrononhotonthuooaos") == 5
p solve("iiihoovaeaaaoougjyaw") == 8

4) Given an array of strings made only from lowercase letters, return an array of
all characters that show up in all strings within the given array (including
duplicates).
For example, if a character occurs 3 times in all strings but not 4 times, you
need to inlude that character three times in the final answer
ruby
common_chars(["bella", "label", "roller"]) #== ["e", "l", "l"]
common_chars(["cool", "lock", "cook"]) #== ["c", "o"]
common_chars(["aabbaaaa", "ccdddddd", "eeffee", "ggrrrrr", "yyyzzz"]) == []

5) Difference of Two:
The objective is to return all pairs of integers from a given array of integers
that have a difference of 2.
The result array should be sorted in ascending order of values. Assume there are
no duplicate integers in the array. The order of the integers in the input array
should not matter.

difference_of_two([1, 2, 3, 4]) == [[1, 3], [2, 4]]
difference_of_two([4, 1, 2, 3]) == [[1, 3], [2, 4]]
difference_of_two([1, 23, 3, 4, 7]) == [[1, 3]]
difference_of_two([4, 3, 1, 5, 6]) == [[1, 3], [3, 5], [4, 6]]
difference_of_two([2, 4]) == [[2, 4]]
difference_of_two([1, 4, 7, 10, 13]) == []

6) You need to play around with the provided string (s).
# Move consonants forward 9 places through the alphabet. If they pass ‘z’, start
# again at ‘a’. Move vowels back 5 places through the alphabet. If they pass ‘a’,
# start again at ‘z’.  Provided string will always be lower case, won’t be empty
# and will have no special characters.

p vowel_back("testcase") == "czbclvbz"
p vowel_back("codewars") == "ljmzfvab" 
p vowel_back("exampletesthere") == "zgvvyuzczbcqzaz"
p vowel_back("returnofthespacecamel") == "azcpawjocqzbyvlzlvvzu"
p vowel_back("bringonthebootcamp") == "kadwpjwcqzkjjclvvy"
p vowel_back("weneedanofficedog") == "fzwzzmvwjoodlzmjp"
  
7)
Find the missing letter:
Write a method that takes an array of consecutive (increasing) letters as input
and that returns the missing letter in the array. You will always get an valid
array. And it will be always exactly one letter be missing. The length of the
array will always be at least 2. The array will always contain letters in only
one case. Use the English alphabet with 26 letters.
ruby
find_missing_letter(["a","b","c","d","f"]) == "e"
find_missing_letter(["O","Q","R","S"]) == "P"
find_missing_letter(["b","d"]) == "c"
find_missing_letter(["a","b","d"]) == "c"
find_missing_letter(["b","d","e"]) == "c"
  
8)
Complete the function scramble(str1, str2) that returns true if a portion of
str1 characters can be rearranged to match str2, otherwise returns false.
Notes: Only lower case letters will be used (a-z). No punctuation or digits will
be included.
ruby
scramble('fnollfkjchgjgedghmc', 'cwyydgtuidth') == false
scramble('hi', 'ih') == true
scramble('i', 'hi') == false
scramble('rkqodlw', 'world') == true
scramble('cedewaraaossoqqyt', 'codewars') == true
scramble('rkqodlw','world') == true
scramble('cedewaraaossoqqyt','codewars') == true
scramble('katas','steak') == false
scramble('scriptjava','javascript') == true
scramble('scriptingjava','javascript') == true
  
9)
Given a string, concatenate into a new string with case-insensitive alphabetical
order of appeareance. Whitespace and punctuation shall be removed.
ruby
alphabetized("The Holy Bible") == "BbeehHilloTy"
  
10)
You are given an array (which will have a length of at least 3, but could be
very large) containing integers. The array is either entirely comprised of odd
integers or entirely comprised of even integers except for a single integer N.
Write a method that takes the array as an argument and returns this “outlier” N.
ruby
find_outlier([0, 1, 2]) == 1
find_outlier([1, 2, 3]) == 2
find_outlier([2, 4, 0, 100, 4, 11, 2602, 36]) == 11
find_outlier([160, 3, 1719, 19, 11, 13, -21]) == 160
  
11)
We are given a string, and we ar replacing WUB with an empty space.
ruby
song_decoder("WUBHIWUBTHERE!")= "HI THERE!"
song_decoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB")  == 'WE ARE THE 
CHAMPIONS MY FRIEND'
song_decoder("AWUBWUBWUBBWUBWUBWUBC") == "A B C"
song_decoder("WUBWUBAWUBBWUBCWUB") == "A B C"

12)
Write a function that when given a URL as a string, parses out just the domain
name and returns it as a string.
ruby
domain_name("http://github.com/carbonfive/raygun") == "github" 
domain_name("http://www.zombie-bites.com") == "zombie-bites"
domain_name("https://www.cnet.com") == "cnet"

13)
Given an non-empty string check if it can be constructed by taking a substring
of it and appending multiple copies of the substring together. You may assume
the given sring consists of lowercase english letters only.
ruby

def repeated_substring_pattern(str)
  arr = str.scan(/(.+)(\1)+/)
  return false if arr.empty?
  arr.first.join == str
end

repeated_substring_pattern("abab") == true
repeated_substring_pattern("aba") == false
repeated_substring_pattern("aabaaba") == false
repeated_substring_pattern("abaababaab") == true
repeated_substring_pattern("abcabcabcabc") == true

14)
A pangram is a sentence that contains every single letter of the alphabet at
least once. For example, the sentence “The quick brown fox jumps over the lazy
dog” is a pangram, because it uses the letters A-Z at least once (case is
irrelevant).
Given a string, detect whether or not it is a pangram. Return True if it is,
False if not. Ignore numbers and punctuation.
ruby
p pangram?("The quick brown fox jumps over the lazy dog.") == true
p pangram?("This is not a pangram.") == false
  
15)
You have to create a method that takes a positive integer number and returns
the next bigger number formed by the same digits. If no bigger numbere can be
composed using those digits, return -1.
ruby

def next_bigger_num(num)
  arr = num.to_s.chars.permutation(num.to_s.length).to_a.map(&:join).sort.select { |n| n.to_i > num }.first
  arr ? arr.to_i : -1
end

next_bigger_num(9) == -1
next_bigger_num(12) == 21
next_bigger_num(513) == 531
next_bigger_num(2017) == 2071
next_bigger_num(111) == -1
next_bigger_num(531) == -1
next_bigger_num(123456789) == 123456798

16)
The maximum sum subarray problem consists in finding the maximum sum of a
contiguous subsequence in an array of integers:
ruby
max_sequence([]) == 0
max_sequence([-2, 1, -3, 4, -1, 2, 1, -5, 4]) == 6
max_sequence([11]) == 11
max_sequence([-32]) == 0
max_sequence([-2, 1, -7, 4, -10, 2, 1, 5, 4]) == 12

17)
Write a method to find the longest common prefix amongst an array of strings.
If there is no common prefix, return an empty string “”.
All given inputs are in lowecase letters a-z.
ruby

def common_prefix(arr)
  first_word = arr.shift
  catcher = arr.map { |word| word.chars.join("*") + "*" } 
  common = []
  catcher.each { |combo| common << first_word.scan(/#{combo}/).first }
  common.min_by(&:length)
end 

common_prefix(["flower", "flow", "flight"]) == "fl"
common_prefix(["dog", "racecar", "car"]) == ""
common_prefix(["interspecies", "interstellar", "interstate"]) == "inters"
common_prefix(["throne", "dungeon"]) == ""
common_prefix(["throne", "throne"]) == "throre"

18)
The marketing team is spending way too much time typing in hashtags.
Let’s help them with our own Hashtag Generator!
Here’s the deal:
It must start with a hashtag (#).
All words must have their first letter capitalized.
If the final result is longer than 140 chars it must return false.
If the input or the result is an empty string it must return false.
ruby
generateHashtag("") == false
generateHashtag(" " * 200) == false
generateHashtag("Do We have A Hashtag") == "#DoWeHaveAHashtag"
generateHashtag("Codewars") == "#Codewars"
generateHashtag("Codewars Is Nice") ==  "#CodewarsIsNice"
generateHashtag("Codewars is nice") == "#CodewarsIsNice"
generateHashtag("code" + " " * 140 + "wars") == "#CodeWars"
generateHashtag("Loooooooooooooooooooooooooooooooooooooooooooooooooooooooo\
oooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo\
ooooooooooooooooooooooooong Cat") == false
generateHashtag("a" * 139) == "#A" + "a" * 138
generateHashtag("a" * 140) == false
  
19)
Longest Palindrome:
Find the length of the longest palindrome in a given string.
As an example, if the input was “I like racecars that go fast”, the substring
(racecar) length would be 7.
If the length of the input string is 0, the return value must be 0.
ruby
longest_palindrome("a") == 1
longest_palindrome("aa") == 2
longest_palindrome("baa") == 2
longest_palindrome("aab") == 2
longest_palindrome("baabcd") == 4
longest_palindrome("baablkj12345432133d") == 9

20)
Given a string, return a version of the string with each letter in its position
capitalized, and separated with  a dash “-” based upon its index position in the
string.
ruby
accum("abcd") == "A-Bb-Ccc-Dddd"
accum("RqaEzty") == "R-Qq-Aaa-Eeee-Zzzzz-Tttttt-Yyyyyyy"
accum("cwAt") == "C-Ww-Aaa-Tttt"

21)
Write a method that takes a string as an argument and groups the number of time
each character appears in the string as a hash sorted by the highest number of
occurrences.
The characters should be sorted alphabetically. You should ignore spaces, special
characters and count uppercase letters as lowercase ones.
  
get_char_count(“cba”) == { 1 => [“a”, “b”, “c”] }
get_char_count(“Mississippi”) == { 4 => [“i”, “s”], 2 => [“p”], 1 => [“m”] }
get_char_count(“Hello. Hello? HELLO!!“) == { 6 => [“l”], 3 => [“e”, “h”, “o”] }
get_char_count(“abc123&qu...
```



---



# **Problem Sets Live**

###### **Problem 1 Repeated substrings**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: string of characters
Output: boolean

=====> Rules
Explicit Requiremnts:
  - only strings
  - look for patterns with no odd one out
  -
Implicit Requiremnts:
  - boolean Output
  - no empty string, no special characters

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p repeated_substring_pattern("abab") == true
  - [a, b] , [a,b]
p repeated_substring_pattern("aba") == false
  - [a] [b] [a]
p repeated_substring_pattern("abaababaab") == true
  - [abaab], [abaab]
p repeated_substring_pattern("abcabcabcabc") == true
  - [abc], [abc], [abc]

=====> Data structure(s):
input: string
intermediate : array, hash
Output:boolean

=====> Algorithm:
given a string of characters
iterate through the characters creating a collection of repeatting patterns leaving the odd one out
if the returned collection forms the given string then return true else false

=====> Optional Implementation (Pseudo-code):

=end

def split_array(str)
  arr = []
  split_str = str.split("")
  (1..str.length).each { |e| split_str.each_slice(e) {|ele| arr << ele }}
  arr.select { |array| array.length > 1 }
end

def create_hash(str)
  hsh = {}
  split_array(str).each do |sub|
    hsh.has_key?(sub) ? hsh[sub] << sub : hsh[sub] = [sub]
  end
  hsh
end

def select_values(str)
  new_hsh = create_hash(str).select { |_, value| value.length > 1 }
  new_hsh.values.map { |e| e.flatten.join }
end

def repeated_substring_pattern(str)
  select_values(str).any?(str)
end

p repeated_substring_pattern("abab") == true
p repeated_substring_pattern("aba") == false
p repeated_substring_pattern("abaababaab") == true
p repeated_substring_pattern("abcabcabcabc") == true

#### chris solution
def repeated_substring_pattern(str)
  sub_strings = []
  1.upto(str.size - 1) { |num| str.chars.each_cons(num) { |el| sub_strings << el }}
  sub_strings.map!(&:join)
  
  sub_strings.each do |sub_str|
    current_str = sub_str
    loop do
      # p "#{current_str} before loop"
      break if current_str.size > str.size || current_str == str
      current_str += current_str
      # p "#{current_str} after loop"
    end
    # p "current str: #{current_str} and str: #{str}"
    return true if current_str == str
  end
  false
end

### Monte's Solution
def repeated_substring_pattern(str)
  characters = str.chars
  p arr1 = characters[0..(characters.size / 2) - 1]
  p arr2 = characters[(characters.size / 2).. - 1]
  arr1.join == arr2.join  
end
```

###### **Problem 2: Reverse a string** 

**without using the built-in #reverse method**

```ruby
=begin
take a string as an argument, return the string in reverse order without using the built-in reverse method.

reverse_string("abcde") == "edcba"
reverse_string(" ") == " "
reverse_string("football") == "llabtoof"
=end

def reverse_string(str)
  arr = str.split("")
  reverse_arr = []
  arr.length.times { reverse_arr << arr.pop }
  reverse_arr.join
end

p reverse_string("abcde") == "edcba"
p reverse_string(" ") == " "
p reverse_string("football") == "llabtoof"

# Option 2 using #reverse_each
def reverse_string(str)
  arr = str.split("")
  reverse_arr = []
  arr.reverse_each { |letter| reverse_arr << letter }
  reverse_arr.join
end
```

###### **Problem 3: Fizzbuzz**

```ruby
=begin
write a method that takes two arguments: the first is the starting number, and the second is the ending number. Print out all numbers between the two numbers except if a number is divisible by 3, print out "Fizz", if a number is divisible by 5, print out "Buzz", and if a number is divisible by 3 and 5, print out "FizzBuzz".

fizzbuzz(1, 10)
fizzbuzz(1, 15)
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input:
  - 2 integers
  -
Output:
  - divisible by 3 "Fizz"
  - divisible by 5 "Buzz"
  - divisible by 3 && 5 "FizzBuzz"

=====> Rules
Explicit Requiremnts:
  - input needs to be whole numbers
  -
Implicit Requiremnts:
  - no Alphabets or special characters
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
fizzbuzz(1, 10)
  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  3 #=> "Fizz"
  5 #=> "Buzz"
  6 #=> "Fizz"
  9 #=> "Fizz"
  10 #=> "Buzz"
fizzbuzz(1, 15)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
3 #=> "Fizz"
5 #=> "Buzz"
6 #=> "Fizz"
9 #=> "Fizz"
10 #=> "Buzz"
12 #=> "Fizz"
15 #=> "FizzBuzz"

=====> Data structure(s):
Input: array
Intermediate: array
Output:string

=====> Algorithm:
create a collection ranging from the first argument to the last argument
iterate over the collection and print "Fizz" if the integer is divisible by 3, "Buzz" if the integer is divisible by 5 and "FizzBuzz" if divisible by both Integers 3 and 5

=====> Optional Implementation (Pseudo-code):

=end

def num_array(num1, num2)
  (num1..num2).to_a
end

def fizzbuzz(num1, num2)
  num_array(num1, num2).each do |number|
    if number % 3 == 0 && number % 5 == 0
      puts "FizzBuzz"
    elsif number % 3 == 0
      puts "Fizz"
    elsif number % 5 == 0
      puts "Buzz"
    else
      puts number
    end
  end
end

fizzbuzz(1, 10)
puts "=================="
fizzbuzz(1, 15)
```

###### **Problem 4:  Find Primes** 

**find primes between two numbers**

```ruby
# Write a method that takes two numbers. Return an array containing all primes between the two numbers (include the two given numbers in your answer if they are prime). Don't use Ruby's 'prime' class.

def find_primes(num1, num2)
  arr = (num1..num2).to_a
  new_arr = arr.select { |num| num.remainder(2) != 0 && num.remainder(3) != 0 }
  new_arr.unshift(3) if arr.include?(3)
  new_arr.unshift(2) if arr.include?(2)
  new_arr
end

p find_primes(3, 10) #== [3, 5, 7]
p find_primes(11, 20) #== [11, 13, 17, 19]
p find_primes(100, 101) #== [101]
p find_primes(1, 100) #== [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
p find_primes(1, 2) #== [2]
```

###### **Problem 5: Remove vowels**

```ruby
# Write a method that takes an array of strings and returns an array of the same string values, except with the vowels removed.

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input:
  -string
  -
Output:
  - string with no vowels
  -

=====> Rules
Explicit Requiremnts:
  - no special characters
  -
Implicit Requiremnts:
  - no empty string
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p remove_vowels(['green', 'yellow', 'black', 'white']) == ['grn', 'yllw', 'blck', 'wht']

=====> Data structure(s):
Input: array of strings
Intermediate: array of strings
Output: array of strings

=====> Algorithm:
given a array of strings
iterate through the array and create a new array whose elements are transformed from the original array with vowels removed

=====> Optional Implementation (Pseudo-code):

=end

def remove_vowels(arr)
  arr.map { |ele| ele.scan(/[^aeiou]/i).join }
end

p remove_vowels(['green', 'yellow', 'black', 'white']) #== ['grn', 'yllw', 'blck', 'wht']
```

###### **Problem 6: Scramble**

**Write a function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise, return false.**

```ruby
def create_hash(str)
  hsh = {}
  str.chars.each do |ele|
    hsh.has_key?(ele) ? hsh[ele] += 1 : hsh[ele] = 1
  end
  hsh
end

def scramble(str1, str2)
  hsh_str1 = create_hash(str1)
  hsh_str2 = create_hash(str2)
  str2.chars.map { |ele| hsh_str1[ele] ? hsh_str1[ele] >= hsh_str2[ele] : false }.all?(true)
end

# Write a function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise, return false.
p scramble('javaass', 'jjss') == false
p scramble('rkqodlw', 'world') == true
p scramble('cedewaraaossoqqyt', 'codewars') == true
p scramble('katas', 'steak') == false
p scramble('scriptjava', 'javascript') == true
p scramble('scriptingjava', 'javascript') == true
```

###### **Problem 7: Common Chars**

```ruby
def common_chars arr
  uniques = arr[0].chars.uniq
  common_chars = []
  uniques.each do |char|
    count = []
    arr.each { |substring| count << substring.count(char) }
    count.min.times { |_| common_chars << char }
  end
  common_chars
end

p common_chars(['bella', 'label', 'roller']) #== ['e', 'l', 'l']
p common_chars(['cool', 'lock', 'cook']) #== ['c', 'o']
p common_chars(['aabbaa', 'cccdddd', 'eeffee', 'ggrrrr']) #== []

# Given an array of strings made only from lowercase letters, return an array of all characters that show up in all strings within the given array (including duplicates). For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.

# Option 2
def common_chars(array)
  array = array.map { |word| word.dup }
  chars = array.shift.chars
  chars.select do |char|
    array.all? { |word| word.sub!(char, "") }
  end
end

# Option 3
def common_chars(arr)
  arr.first.chars.select { |char| arr.all? { |word| word.sub!(char, "") } }
end
```

###### **Problem 8: Next Biggest num** 

```ruby
=begin
You have to create a method that takes a positive integer number and returns the next bigger number formed by the same digits:

12 ==> 21
513 ==> 531
2017 ==> 2071
If no bigger number can be composed using those digits, return -1:
9 ==> -1
111 ==> -1
531 ==> -1
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Take a number and return the next possible biggest numbr using the numbers as combinations
  - integer
  -
Output:
  - integer
  -

=====> Rules
Explicit Requiremnts:
  - integer
  -
Implicit Requiremnts:
  - no special charcters or sting or other datatypes
  - a number nust be input. cant have 0 or no argument

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p next_bigger_num(9) == -1
  when no next big number return -1
  
p next_bigger_num(12) == 21
  next big number combo
  
p next_bigger_num(513) == 531
  next big number combo
  
p next_bigger_num(2017) == 2071
  next big number combo
  
p next_bigger_num(111) == -1
  cant find next big number as the combination is the same as the original
  
p next_bigger_num(531) == -1
  cant find next big number return -1
  
p next_bigger_num(123456789) == 123456798
  next big number combination


=====> Data structure(s):
Input: integer
Intermediate: array, str
Output: Integer

=====> High Level Algorithm:
  given an integer
  create different possible combinations with each Induvidual integers combined
  chose the second biggest number where the first number is the given number
  if no second number found then return -1

=====> Optional Implementation (Pseudo-code):

=end

# code with intent

def to_string_arr(num)
  arr = num.digits.map(&:to_s).reverse
end

def create_combo(num)
  arr = []
  str_arr = to_string_arr(num)
  str_arr.permutation.each { |ele| arr << ele } 
  arr = arr.map(&:join).map(&:to_i).select { |ele| ele >= num }
  arr.sort![1]
end

def  next_bigger_num(num)
  return -1 if num.to_s.length == 1 
  
  # to_string_arr(num)
  return -1 if create_combo(num) == num || create_combo(num) == nil
  create_combo(num)
end

p next_bigger_num(9) == -1
p next_bigger_num(12) == 21
p next_bigger_num(513) == 531
p next_bigger_num(2017) == 2071
p next_bigger_num(111) == -1
p next_bigger_num(531) == -1
p next_bigger_num(123456789) == 123456798

# Option 2 : Note--- program uses too mush memory for the last iteration
def find_max(num)
  num.digits.sort.reverse.join.to_i
end

def collection_combination(num)
  arr = [num]
  max_num = find_max(num)
  new_arr = (num + 1..max_num).to_a.select { |number| number.digits.sort == num.digits.sort }
  new_arr.each { |ele| arr << ele }
  arr
end

def next_bigger_num(num)
  final_num = collection_combination(num)[1]
  final_num ? final_num : -1
end

# Option 3: Program uses too much memory for the last test case
def find_max(num)
  num.digits.sort.reverse.join.to_i
end

def collection_combination(num)
  max_num = find_max(num)
  (num + 1..max_num).to_a.each { |number| return number if number.digits.sort == num.digits.sort }
  return -1
end

def next_bigger_num(num)
  final_num = collection_combination(num)
end
```

###### **Problem 9: Common Prefix**

```ruby
=begin
Write a method to find the longest common prefix string amongst an array of strings. If there is no common prefix, return an empty string,

All given inputs are in lowercase letters a-z.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem: given a string
Input:
  - given an array of strings 
  - 
Output:
  - common prefix in all the elements as strings
  - 

=====> Rules
Explicit Requiremnts:
  - if no common prefix return an empty string ""
  - return a string having the common characters as prefix
Implicit Requiremnts:
  - no special characters or any other data types
  - 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

puts common_prefix(["flower", "flow", "fliwht"]) == "fl"
"fl" is common prefix in all three

puts common_prefix(["dog", "racecar", "car"]) == ""
no common prefix

puts common_prefix(["interspecies", "interstellar", "interstate"]) == "inters"

puts common_prefix(["throne", "dungeon"]) == ""
no common prefix

puts common_prefix(["throne", "throne"]) == "throne"
since both of the string are equal then the whole string is returned

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
given an array of strings. 
iterate over the characters in the first element of the array and create a collection different combination of prefixes. Select the largest prefix that is present in all the elements in the main collection. If no prefix then return ""

=====> Optional Implementation (Pseudo-code):

=end

def prefix_array(string_arr)
  arr = []
  str = ""
  string_arr[0].chars.each { |ele| arr << (str += ele) }
  arr
end

def select_prefix(string_arr)
  prefix_array(string_arr).select { |ele| string_arr.all? { |str| str.start_with?(ele) } }.last
end

def common_prefix(string_arr)
  # prefix_array(string_arr)
  result = select_prefix(string_arr)
  result ? result : ""
end

p common_prefix(["flower", "flow", "fliwht"]) == "fl"
p common_prefix(["dog", "racecar", "car"]) == ""
p common_prefix(["interspecies", "interstellar", "interstate"]) == "inters"
p common_prefix(["throne", "dungeon"]) == ""
p common_prefix(["throne", "throne"]) == "throne"
```

###### **Problem 10: Substring Test** 

 ```ruby
 =begin
 Given 2 strings, your job is to find out if there is a substring that appears in both strings. You will return true if you find a substring that appears in both strings, and false if not. A substring is longer than 1 character.
 =end
 
 =begin
 ========== THE PEDAC PROCESS ==========
 
 =====> Problem:
 Input:
   - 2 substrings
   -
 Output:
   - boolean
   -
 
 =====> Rules
 Explicit Requiremnts:
   - two differnt strings
   - space can be included in the substrings
   - when both the argikments are spaces or empty then return false
   - Case insensitive
   
 Implicit Requiremnts:
   - no special characters
   - no other data types
   - order of the string doesnt matter
 
 =====> (Any Questions / Assumptions needing clarification?)
 (e.g. return the same string object or an entirely new string???)
 
 =====> Examples, Edge Cases(test rules and boundaries)
 p substring_test('Something', 'Fun') #== false
   "Fun" not present
 
 p substring_test('Something', 'Home')# == true
   "Home" present
 
 p substring_test('Something', ' ') #== false
   " " . emptyy space not present
 
 p substring_test('BANANA', 'banana')# == true
    case insensitive
    
 p substring_test('test', 'llt') #== false
   second substring not present in the first
   
 p substring_test(' ', ' ') #== false
   both the substrings are just spaces
   
 p substring_test('1234567', '541265')# == true
   string representation od the integers acceptable as arguments
   here '541265' is present within `1234567`
 
 
 =====> Data structure(s):
 Input: string
 Intermediate: string
 Output: boolean
 
 =====> High Level Algorithm:
 given 2 string arguments. Case insensitively check if all the characters from the second argument are present in the first argument. If no characters return false. if the second argument is ' ' then return false
 
 =====> Optional Implementation (Pseudo-code):
 
 =end
 
 def substring_test(str1, str2)
   str2_arr = str2.split("")
   arr = str2_arr.select { |ele| str1.downcase.include?(ele.downcase) }.join
   ["", " "].any?(arr) ? false : arr == str2
 end
 
 p substring_test('Something', 'Fun') == false
 p substring_test('Something', 'Home') == true
 p substring_test('Something', ' ') == false
 p substring_test('BANANA', 'banana') == true
 p substring_test('test', 'llt') == false
 p substring_test(' ', ' ') == false
 p substring_test('1234567', '541265') == true
 ```

###### **Problem 11: Contiguous Collection**

```ruby
# Problem 1: Max sequence
=begin
The maximum sum subarray problem consists of finding the maximum sum of a contiguous subsequence in an array of integers.

Example:
max_sequence([-2, 1, -3, 4, -1, 2, 1, -5, 4]) == 6 #=> [4, -1, 2, 1]

The easy case is when the array is made up of only positive numbers and the maximum sum is the sum of the whole array. If the array is made up of negative numbers, return 0 instead. 

An empty array is considered to have zero greatest sum. Note that the empty array is also a valid subarray
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: array of integers. Both positive and negative
  -
  -
Output:
  - 0 if empty array
  - -1 if negative
  - else sum of the longest contiguous sub array

=====> Rules
Explicit Requiremnts:
  - Input array of integers
  - elements can be negative, positive
  - empt array can be passed in as an argument
Implicit Requiremnts:
  - no strings allowed
  - no other datatype allowed such as floats

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p max_sequence([]) == 0
  0 since empty array

p max_sequence([-2, 1, -3, 4, -1, 2, 1, -5, 4]) == 6
  [ 4, -1, 2, 1] #===> 6

p max_sequence([11]) == 11
 just one integer hence return the same

p max_sequence([-32]) == 0
 negative return value hence 0

p max_sequence([-2, 1, -7, 4, -10, 2, 1, 5, 4]) == 12
  [2, 1, 5, 4] == 12

=====> Data structure(s):
Input: array
Intermediate: array
Output: integer

=====> High Level Algorithm:
Create a collections of various possible contiguous sequence as sub arrays. return the sum of the sub array whicg is the highest 

=====> Optional Implementation (Pseudo-code):
return 0 if empty array is passed in as an argument

create a collection with different subarrays which are contiguous numbers from the given collection
transform this collection into a new array with each element equal to the sum of the contiguous array
select the maximum value and return it

return -1 if the return value is negative
=end

# Code With intent

def contiguous_collection(array)
  arr = []
  (1..array.length).each { |ele| array.each_cons(ele) { |es| arr << es } }
  arr
end

def max_value(array)
  arr = contiguous_collection(array)
  arr.map(&:sum).max
end

def max_sequence(array)
  return 0 if array.empty?
  # contiguous_collection(array)
  sum = max_value(array)
  sum > 1 ? sum : 0 
end

p max_sequence([]) == 0
p max_sequence([-2, 1, -3, 4, -1, 2, 1, -5, 4]) == 6
p max_sequence([11]) == 11
p max_sequence([-32]) == 0
p max_sequence([-2, 1, -7, 4, -10, 2, 1, 5, 4]) == 12
```

###### **Problem 12: Get char sum**

```ruby
=begin
Write a method that takes a string as an argument and groups the number of time
each character appears in the string as a hash sorted by the highest number of
occurrences.
The characters should be sorted alphabetically. You should ignore spaces, special
characters and count uppercase letters as lowercase ones.
=end

def create_hash(str)
  hsh = str.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele] += 1}
  hsh.each_with_object({}) { |(k, v), h| h.has_key?(v) ? h[v] << k : h[v] = [k]  } 
end

def get_char_count(str)
  str = str.downcase.scan(/[a-z]/).sort
  create_hash(str)
end

p get_char_count('cba') == { 1 => ['a', 'b', 'c'] }
p get_char_count('Mississippi') == { 4 => ['i', 's'], 2 => ['p'], 1 => ['m'] }
p get_char_count('Hello. Hello? HELLO!!') == { 6 => ['l'], 3 => ['e', 'h', 'o'] }
```

###### **Problem 13: Finding parents**

```ruby
def find_children(str)
  hsh = str.chars.group_by { |ele| ele.downcase } 
  hsh.values.map { |e| e.join.downcase.capitalize }.sort.join
end

# def find_children(dancing_brigade)
#   dancing_brigade.chars.sort_by { |char| [char.downcase, char] }
# end

# p find_children("abBA") #== "AaBb"
# p find_children("AaaaaZazzz") #== "AaaaaaZzzz"
# p find_children("CbcBcbaA") #== "AaBbbCcc"
# p find_children("xXfuUuuF") #== "FfUuuuXx"
# p find_children("") #== ""
```



---

# **Important iterating and combination methods**

###### **#combination**

###### **#permutation**

###### **#each_slice**

###### **#each_cons**

###### **#chunk_while**

###### **#zip**

###### **#tally**

###### **#group_by**

###### **#permutations**

###### **#each_with_object**

###### **#reduce #inject**

###### #**max_by(*n)**

###### **#first(*n)**

###### **#gsub**

###### **#slice_when**

###### **#abs**



---

# **Codewars problem**

###### **Example 1: count letters**

```ruby
=begin
[Train: Count letters in string \| Codewars](https://www.codewars.com/kata/5808ff71c7cfa1c6aa00006d/train/ruby)
6 kyu
Count letters in string
In this kata, you've to count lowercase letters in a given string and return the letter count in a hash with 'letter' as key and count as 'value'. The key must be 'symbol' instead of string in Ruby and 'char' instead of string in Crystal.

Example:

letterCount('arithmetics') #=> {:a=>1, :c=>1, :e=>1, :h=>1, :i=>2, :m=>1, :r=>1, :s=>1, :t=>2}
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Given a string as an argument
  -
  -
Output:
  - hash with key as the symbol of the characters present in the string and the values is its count
  -

=====> Rules
Explicit Requiremnts:
  - Only strings
  - no empty string
Implicit Requiremnts:
  - no special characters or any other data types
  - lower case only
  - is the order preserved? 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p letter_count('codewars') == {:a=>1, :c=>1, :d=>1, :e=>1, :o=>1, :r=>1, :s=>1, :w=>1})

p letter_count('activity') == {:a=>1, :c=>1, :i=>2, :t=>2, :v=>1, :y=>1}

p letter_count('arithmetics') == {:a=>1, :c=>1, :e=>1, :h=>1, :i=>2, :m=>1, :r=>1, :s=>1, :t=>2})

=====> Data structure(s):
Input: string
Intermediate: array
Output: hash

=====> High Level Algorithm:
iterate through the characters in the string and count their occurances. collect the information within a hash with keys as the string representation of the character and its count as its associated value


=====> Optional Implementation (Pseudo-code):
iterate through the string and conver into an array of symbols.
return a hash with each unique character as its key and its count as the associated value
=end

# Option 1
def letter_count(str)
  str.chars.map(&:to_sym).tally
end

p letter_count('codewars') == {:a=>1, :c=>1, :d=>1, :e=>1, :o=>1, :r=>1, :s=>1, :w=>1}
p letter_count('activity') == {:a=>1, :c=>1, :i=>2, :t=>2, :v=>1, :y=>1}
p letter_count('arithmetics') == {:a=>1, :c=>1, :e=>1, :h=>1, :i=>2, :m=>1, :r=>1, :s=>1, :t=>2}

# Option 2
def create_hash(arr) # helper method
  hsh = {}
  arr.each { |ele| hsh.has_key?(ele) ? hsh[ele] += 1 : hsh[ele] = 1 }
  hsh
end

def letter_count(str)
  arr = str.chars.map(&:to_sym)
  create_hash(arr)
end

# Option 3
def letter_count(str)
  str.chars.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele.to_sym] += 1 }
end
```

###### **Example 2: Find all pairs**

```ruby
=begin
Find all pairs

You are given array of integers, your task will be to count all pairs in that array and return their count.

Notes:

Array can be empty or contain only one value; in this case return 0
If there are more pairs of a certain number, count each pair only once. E.g.: for [0, 0, 0, 0] the return value is 2 (= 2 pairs of 0s)
Random tests: maximum array length is 1000, range of values in array is between 0 and 1000
Examples
[1, 2, 5, 6, 5, 2]  -->  2
...because there are 2 pairs: 2 and 5

[1, 2, 2, 20, 6, 20, 2, 6, 2]  -->  4
...because there are 4 pairs: 2, 20, 6 and 2 (again)
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
You are given array of integers, your task will be to count all pairs in that array and return their count.

Input:
  - array if integers
  -
Output:
  - return the count of the pairs
  -

=====> Rules
Explicit Requiremnts:
  - array of integers
  - 
Implicit Requiremnts:
  - no other objetcs or datatypes as elements
  - output the count of the pairs
  - 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p pairs([1, 2, 5, 6, 5, 2]) == 2
[2, 2] [5, 5] 

p pairs([1, 2, 2, 20, 6, 20, 2, 6, 2]) == 4
[2, 2] [2, 2] [20, 20] [6, 6]

p pairs([0, 0, 0, 0, 0, 0, 0]) == 3 
[0, 0], [0, 0]

p pairs([1000, 1000]) == 1

p pairs([]) == 0
no pairs so return 0

p pairs([54]) == 0
no pairs so return 0

=====> Data structure(s):
Input: array
Intermediate: hash, array
Output: integer

=====> High Level Algorithm:
iterate through tthe given collection and count the number of occurance of each element. Sort them into pairs and return the count of the pairs

=====> Optional Implementation (Pseudo-code):
given an array of integers
convert the array into a hash object with keys as elemnts and the value as its count
collect the key-value pairs that are > 1 into a new hash
return 0 if none are selected ie. empty hash
collect the values into a new array and add all the elements
divide the sum by 2 and return the value

=end

# Code With Intent

def pairs(arr)
  arr.tally.select { |_, v| v > 1 }.values.map { |e| e / 2 }.sum 
end

p pairs([1, 2, 5, 6, 5, 2]) == 2
p pairs([1, 2, 2, 20, 6, 20, 2, 6, 2]) == 4
p pairs([0, 0, 0, 0, 0, 0, 0]) == 3 
p pairs([1000, 1000]) == 1
p pairs([]) == 0
p pairs([54]) == 0

# Option 2

def pairs(arr)
  arr.uniq.reduce(0) { |sum, ele| sum + (arr.count(ele) / 2)  }
end
```

###### **Example 3: Instance count  -----**

```ruby
=begin
Return substring instance count
Complete the solution so that it returns the number of times the search_text is found within the full_text.

Usage example:

solution('aa_bb_cc_dd_bb_e', 'bb') # should return 2 since bb shows up twice
solution('aaabbbcccc', 'bbb') # should return 1
=end

def solution(str, arg)
  hsh = str.chars.each_with_object(Hash.new(0)) { |ele, h| h[ele] += 1 }
  arg_arr = arg.chars.uniq
  arg_length = arg.length
  hsh.select { |k, v| k == arg_arr[0] }.values.sum / arg_length
end

p solution('abcdeb','b') #== 2
p solution('abcdeb', 'a') #== 1
p solution('abbc', 'bb') #== 1

# Option 2
def solution(str, arg)
  str.scan(/#{arg}/).count
end
```

###### **Example4: Alphabet symmetry**

```ruby
# Alphabet symmetry
# Consider the word "abode". We can see that the letter a is in position 1 and b is in position 2. In the alphabet, a and b are also in positions 1 and 2. Notice also that d and e in abode occupy the positions they would occupy in the alphabet, which are positions 4 and 5.

# Given an array of words, return an array of the number of letters that occupy their positions in the alphabet for each word. For example,

# solve(["abode","ABc","xyzD"]) = [4, 3, 1]
# See test cases for more examples.

# Input will consist of alphabet characters, both uppercase and lowercase. No spaces.

# Good luck!

# If you like this Kata, please try:

# Last digit symmetry

# Alternate capitalization

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given an array of words, return an array of the number of letters that occupy their positions in the alphabet for each word.

Input:
  - array of sttrings
  -
Output:
  - array of integers
  -

=====> Rules
Explicit Requiremnts:
  - no special characters
  - aonly alphabets
  - not case sensitive
Implicit Requiremnts:
  - no special characters
  - no other datatypes

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solve(["abode","ABc","xyzD"]) == [4,3,1]
a = 1    A = 1      D = 4
b = 2    B = 2
d = 4    c = 3
e = 5
total 4    3            1  ===> [4, 3, 1]

p solve(["abide","ABc","xyz"]) == [4,3,0]
a = 1    A = 1      0
b = 2    B = 2
d = 4    c = 3
e = 5
total 4    3         0  ===> [4, 3, 0]

p solve(["IAMDEFANDJKL","thedefgh","xyzDEFghijabc"])== [6,5,7]
DEF    defgh     DEFghij
JKL
6      5         7

p solve(["encode","abc","xyzD","ABmD"]) == [1, 3, 1, 3]
c   abc  D  ABD
1    3   1   3

=====> Data structure(s):
Input: Array
Intermediate: Array, hash
Output: array

=====> High Level Algorithm:
iterate over the given collection of strings and count the number of alphabets in the correct place as in A - Z. Return the count in a transformed array

=====> Optional Implementation (Pseudo-code):
iterate over the given collection of strings
create a hash with keys as alphabets and values as its corresponding position

split the current element into array

iterate over the new array and check if the current element in the new array matched with the value in the hash
count the occurance this happens

do this for all the elements in the original collection of strings and return a new transformed array with elements equal to the count

=end

# Code With Intent
# My_solution
def solve(arr)
  final_arr = []
  hsh = ('a'..'z').to_a.zip(0..23).to_a.to_h
  arr.each do |ele|
    final_arr << ele.chars.select.with_index { |e, idx|  hsh[e.downcase] == idx }
  end
  final_arr.map(&:length)
end

p solve(["abode","ABc","xyzD"]) #== [4,3,1]
p solve(["abide","ABc","xyz"]) #== [4,3,0]
p solve(["IAMDEFANDJKL","thedefgh","xyzDEFghijabc"]) #== [6,5,7]
p solve(["encode","abc","xyzD","ABmD"]) #== [1, 3, 1, 3]
```

###### **Example5: Longest Vowel chain**

```ruby
=begin
Longest vowel chain
The vowel substrings in the word codewarriors are o,e,a,io. The longest of these has a length of 2. Given a lowercase string that has alphabetic characters only and no spaces, return the length of the longest vowel substring. Vowels are any of aeiou.

=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem: Given a lowercase string that has alphabetic characters only and no spaces, return the length of the longest vowel substring.

Input:
  - string object
  -
Output:
  - Integer (count oof the max substring)
  -

=====> Rules
Explicit Requiremnts:
  - lowercase
  - string object
Implicit Requiremnts:
  - no other data types or special characters
  - no Uppercase

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solve("codewarriors") == 2
[o, e, a, io] 

p solve("suoidea") == 3
[uoi, ea]

p solve("iuuvgheaae") == 4
[iuu, eaae]

p solve("ultrarevolutionariees") == 3
[u, a, e, o, u, io, a, iee]

p solve("strengthlessnesses") == 1
p solve("cuboideonavicuare") == 2
p solve("chrononhotonthuooaos") == 5
p solve("iiihoovaeaaaoougjyaw") == 8

=====> Data structure(s):
Input: String
Intermediate: Array
Output: Integer

=====> High Level Algorithm:
iterate through the string and gather the vowel strings into  a new array. Find out the vowel substring
with max length

=====> Optional Implementation (Pseudo-code):
Split the string based on non vowel characters
create a new array with the corresponding length of the vowel substring
return the max value

=end

# Code With Intent

def solve(str)
  str.split(/[^aeiou]/).map(&:length).max
end

p solve("codewarriors") == 2
p solve("suoidea") == 3
p solve("iuuvgheaae") == 4
p solve("ultrarevolutionariees") == 3
p solve("strengthlessnesses") == 1
p solve("cuboideonavicuare") == 2
p solve("chrononhotonthuooaos") == 5
p solve("iiihoovaeaaaoougjyaw") == 8

# Other option
def solve(s)
  s.scan(/[aeiou]+/).map(&:size).max
end
```

###### **Example6: Non-even substring**

```ruby
=begin
Non-even substring
Given a string of integers, return the number of odd-numbered substrings that can be formed.

For example, in the case of "1341", they are 1, 1, 3, 13, 41, 341, 1341, a total of 7 numbers.

solve("1341") = 7. See test cases for more examples.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given a string of integers, return the number of odd-numbered substrings that can be formed.

Input:string of integers
  -
  -
Output:
  - count of odd numberedd substrings
  -

=====> Rules
Explicit Requiremnts:
  - Input is a string of integers
  - no other special characters or alphabets
Implicit Requiremnts:
  - no other data types
  - no empty strings

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p solve("1341") == 7
[1, 1, 3, 13, 41, 341, 1341] 

p solve("1357") == 10
[1, 3, 5, 7, 13, 135, 1357, 35, 357, 57]

p solve("13471") == 12
[1, 3, 7, 1, 13, 1347, 13471, 347, 3471, 471, 47, 71]

p solve("134721") == 13
[1, 13, 1347, 134721, 3, 347, 34721, 47, 4721, 7, 721, 21, 1]

p solve("1347231") == 20
p solve("13472315") == 28


=====> Data structure(s):
Input: string
Intermediate: array
Output: integer

=====> High Level Algorithm:
iterate through the string and form sequence of string which are the odd equivalent of Integers. select the possible combinations and return the number of such possible combinations

=====> Optional Implementation (Pseudo-code):
convert the string into an array of induvidual string representation of the numbers 
create a contiguous sequence sub array of numbers with their length ranging from 1 to the string length
join the strings within the sub array and convert them to Integers
select the odd ones
return the count of the odd numbered element

=end

# Code With Intent

def solve(str)
  split_str = str.split("")
  arr = []
  (1..str.length).each { |e| split_str.each_cons(e) { |ele| arr << ele} }
  arr.map! { |ele| ele.join.to_i }
  arr.select { |ele| ele.odd? }.size
end

p solve("1341") == 7
p solve("1357") == 10
p solve("13471") == 12
p solve("134721") == 13
p solve("1347231") == 20
p solve("13472315") == 28

# Option 2
def solve(s) 
  s.chars.map.with_index{|n,i| n.to_i.odd? ? i+1 : 0}.reduce(:+)
end
```

###### **Example7: Substring Fun**

```ruby
=begin
Substring fun
For example:

["yoda", "best", "has"]  -->  "yes"
  ^        ^        ^
  n=0     n=1     n=2
Note: Test cases contain valid input only - i.e. a string array or an empty array; and each word will have enough letters.
=end


=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Complete the function that takes an array of words.

You must concatenate the nth letter from each word to construct a new word which should be returned as a string, where n is the position of the word in the list.

Input:
  - array of strings
  -
Output:
  - string
  -

=====> Rules
Explicit Requiremnts:
  -array of string objects
  - special characters ignored
Implicit Requiremnts:
  - no other datatype
  - empty array allowed
  - case sensitive

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p nth_char(['yoda', 'best', 'has']) == 'yes'
p nth_char([]) == ''
p nth_char(['X-ray']) == 'X'
p nth_char(['No', 'No']) == 'No'
p nth_char(['Chad', 'Morocco', 'India', 'Algeria', 'Botswana', 'Bahamas', 'Ecuador', 'Micronesia']) ==  'Codewars'

=====> Data structure(s):
Input: Array
Intermediate: array
Output: string

=====> High Level Algorithm:
iterate through the collection and concatenate the element at the current element corresponding to the current element index. return the joined word as a string

=====> Optional Implementation (Pseudo-code):
iterate over the array
for every iteration choose the character at index whose value is the same as the index of the current element
create a new array with the choosen letters as elements. 
join the letters to form the word 
return the word

=end

# Code With Intent

def nth_char(arr)
  arr.map.with_index { |ele, i| ele[i] }.join 
end

p nth_char(['yoda', 'best', 'has']) == 'yes'
p nth_char([]) == ''
p nth_char(['X-ray']) == 'X'
p nth_char(['No', 'No']) == 'No'
p nth_char(['Chad', 'Morocco', 'India', 'Algeria', 'Botswana', 'Bahamas', 'Ecuador', 'Micronesia']) ==  'Codewars'
```

###### **Example8: Repeated String**

```ruby
=begin
[Train: Repeated Substring \| Codewars](https://www.codewars.com/kata/5491689aff74b9b292000334/train/ruby)
6 kyu
For a given nonempty string s find a minimum substring t and the maximum number k, such that the entire string s is equal to t repeated k times. The input string consists of lowercase latin letters. Your function should return a tuple (in Python) (t, k) or an array (in Ruby and JavaScript) [t, k]

Example #1:

for string

s = "ababab"
the answer is

["ab", 3]
Example #2:

for string

s = "abcde"
the answer is

because for this string "abcde" the minimum substring t, such that s is t repeated k times, is itself.
=end


=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: given a string
  -
  -
Output: array with repeated sub character and its count
  -
  -

=====> Rules
Explicit Requiremnts:
  - only string object 
  - no special datatype
Implicit Requiremnts:
  - no empty string
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p f("ababab") == ["ab", 3]
[ab, ab, ab]
p f("abcde") == ["abcde", 1]
[abcde]

=====> Data structure(s):
Input: string
Intermediate: array, hash
Output: array

=====> High Level Algorithm:
iterate over the string and select the repeated sequence of strings which forms the whole string.

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def f(str)
  arr = []
  (1..str.length).each { |n| str.split("").each_cons(n) { |ele|  arr << ele } }
  arr.tally.select { |k, v| k.join * v == str  }.map { |k, v| [k.join, v] }.first
end

p f("ababab") == ["ab", 3]
p f("abcde") == ["abcde", 1]
p f("abceeeabc") == ["abceeeabc", 1]
```

###### **Example9: Typoglycemia Generator**

```ruby
=begin
Background
There is a message that is circulating via public media that claims a reader can easily read a message where the inner letters of each words is scrambled, as long as the first and last letters remain the same and the word contains all the letters. 

Another example shows that it is quite difficult to read the text where all the letters are reversed rather than scrambled.

In this kata we will make a generator that generates text in a similar pattern, but instead of scrambled or reversed, ours will be sorted alphabetically

Requirement
return a string where:

1) the first and last characters remain in original place for each word
2) characters between the first and last characters must be sorted alphabetically
3) punctuation should remain at the same place as it started, for example: shan't -> sahn't

Assumptions

1) words are separatedseperated by single spaces
2) only spaces separate words, special characters do not, for example: tik-tak -> tai-ktk
3) special characters do not take the position of the non special characters, for example: -dcba -> -dbca
4) for this kata punctuation is limited to 4 characters: hyphen(-), apostrophe('), comma(,) and period(.)
5) ignore capitalisation

for reference: http://en.wikipedia.org/wiki/Typoglycemia

========== THE PEDAC PROCESS ==========

=====> Problem:
the first and last letters remain the same and the word contains all the letters. inner letters of each words is scrambled

Input: string
  -
  -
Output: string
  -
  -

=====> Rules
Explicit Requiremnts:
  - Given a string of characters
  - can include punctuation
  - they remain in the same position
  - should handle empty string
  - should handle 2 letter word
Implicit Requiremnts:
  - no other datatypes as arguments
  - first and the last characters of wach elements are retained in their position
  - other characters are sorted alphabetically
  - single characters return the same
  - all lowercase

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p scramble_words('paefilnoorsss') == 'paefilnoorsss'
p and s are maintiained inther places
others are ordered in alphabetical order

p scramble_words('i') == 'i'
p scramble_words('') == ''
p scramble_words('me') == 'me'
p scramble_words('you') == 'you'
p scramble_words('card-carrying') == 'caac-dinrrryg'
p scramble_words("shan't") == "sahn't"
p scramble_words('-dcba') == '-dbca'
p scramble_words('dcba.') == 'dbca.'

=====> Data structure(s):
Input: string
Intermediate: array 
Output: string

=====> High Level Algorithm:
iterate over the string and for each word in the current iteration preserve the position of the first and the last characters and arrange the rest of the characters in ascending order. Keep the position of the punctuation

=====> Optional Implementation (Pseudo-code):
given a string of characters

if 0, 1 or 2 letters then return the given string
more than 2 letter in the string
  split the string into an array having each word as a seperate string
  preserve the first and the last character position of each word within the string
  preserve the position of the punctuation
  sort the characters within the each word from index 1 .. -1
  join all the characters and return the rearranged string

=end

# Code With Intent

def scramble(word)
  characters = word.chars
  letters = characters.select { |ele| ('a'..'z').include?(ele) }
  letters[1..-2] = letters[1..-2].sort
  characters.map { |ele| ('a'..'z').include?(ele) ? letters.shift : ele }.join
end

def scramble_words(str)
  return str if str.length <= 3
  
  str.split.map { |ele| scramble(ele) }.join(" ")
end

# Option 2
# def scramble_words(words)
#   words.gsub(/(?<=\w)([^ ]+)(?=\w)/){|a| cs = a.scan(/\w/).sort; a.gsub(/\w/){cs.shift}}
# end

# Option 3
def scramble_words(words)
 words.gsub(/(?<=\w)(\S+)(?=\w)/) { |a| cs = a.scan(/\w/).sort; a.gsub(/\w/){ cs.shift } }
end

# Option 4 
def arrange(word)
  alphabets = word.scan(/[a-z]/)
  alphabets[1..-2] = alphabets[1..-2].sort
  word.gsub(/\w/) { |i| alphabets.shift  }  
end

def scramble_words(str)
  return str if str.length < 4
  str.split(" ").map { |word| arrange(word) }.join(" ")
end

p scramble_words('professionals') #== 'paefilnoorsss'
p scramble_words('i') #== 'i'
p scramble_words('') #== ''
p scramble_words('me') #== 'me'
p scramble_words('you') #== 'you'
p scramble_words('card-carrying') #== 'caac-dinrrryg'
p scramble_words("shan't") #== "sahn't"
p scramble_words('-dcba') #== '-dbca'
p scramble_words('dcba.') #== 'dbca.'
p scramble_words("you've gotta dance like there's nobody watching, love like you'll never be hurt, sing like there's nobody listening, and live like it's heaven on earth.") #== "you've gotta dacne like teehr's nbdooy wachintg, love like ylo'ul neevr be hrut, sing like teehr's nbdooy leiinnstg, and live like it's haeevn on earth."
```

###### **Example10: Most frequently used words**

```ruby
# Top 3 most frequently used words

def top_3_words(str)
  str.downcase!
  return [] if  str.scan(/[a-z]/).empty?
  arr = str.scan(/[a-zA-Z']+/)
  arr.tally.sort_by { |a, b| b}.reverse.slice(0, 3).map(&:first)
end

# Option 2
# def top_3_words(text)
#   text.scan(/[A-Za-z']+/)
#       .select { |x| /[A-Za-z]+/ =~ x }
#       .group_by { |x| x.downcase }
#       .sort_by { |k,v| -v.count }
#       .first(3)
#       .map(&:first)
# end

# Option 3 - new method #max_by (takes a method argument and a block)
# def top_3_words(text)
#  counts = Hash.new(0)
#   text.downcase.scan(/[a-z]+[a-z']*/) { |word| counts[word] += 1 }
#   counts.max_by(3) { |word, count| count}.map(&:first)
# end

p top_3_words("a a a  b  c c  d d d d  e e e e e") == ["e", "d", "a"]
p top_3_words("e e e e DDD ddd DdD: ddd ddd aa aA Aa, bb cc cC e e e") == ["e", "ddd", "aa"]
p top_3_words("  //wont won't won't ") == ["won't", "wont"]
p top_3_words("  , e   .. ") == ["e"]
p top_3_words("  ...  ") == []
p top_3_words("  '  ") == []
p top_3_words("  '''  ") == []
p top_3_words("""In a village of La Mancha, the name of which I have no desire to call to
mind, there lived not long since one of those gentlemen that keep a lance
in the lance-rack, an old buckler, a lean hack, and a greyhound for
coursing. An olla of rather more beef than mutton, a salad on most
nights, scraps on Saturdays, lentils on Fridays, and a pigeon or so extra
on Sundays, made away with three-quarters of his income.""") == ["a", "of", "on"]
```

###### **Example11: Domain name**

```ruby
=begin
Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. For example:

domain_name("http://github.com/carbonfive/raygun") == "github" 
domain_name("http://www.zombie-bites.com") == "zombie-bites"
domain_name("https://www.cnet.com") == "cnet"
=end

def domain_name(name)
  name.split(/\/\/|\./).select { |ele| !%w(http: https: www).any?(ele) }.first
end

# Option 2
# def domain_name(url)
#  ["https://", "http://", "www."].each {|str| url.sub!(str, '') }
#  url.split(".").first
# end

# Option 3 (doesnt work for https)
# def domain_name(url)
#   URI.parse(url).host.split(".").select { |ele| !%w(http: https: www).any?(ele) }.first
# end

p domain_name("http://google.com") #== "google"
p domain_name("http://google.co.jp") #== "google"
p domain_name("www.xakep.ru") #== "xakep"
p domain_name("https://youtube.com") #== "youtube"
p domain_name("https://www.youtube.com") #== "youtube"
p domain_name("youtube.com") #== "youtube"
```

###### **Example12: Detect Panagram**

```ruby
=begin
A pangram is a sentence that contains every single letter of the alphabet at least once. For example, the sentence "The quick brown fox jumps over the lazy dog" is a pangram, because it uses the letters A-Z at least once (case is irrelevant).

Given a string, detect whether or not it is a pangram. Return True if it is, False if not. Ignore numbers and punctuation.
=end

def panagram?(str)
  str.downcase.scan(/[a-z]/).uniq.sort == ('a'..'z').to_a
end

# option 2
# def panagram?(str)
#  ('a'..'z').all? { |ele| p str[/#{ele}/i] }
# end

p panagram?("The quick brown fox jumps over the lazy dog.") == true
p panagram?("This is not a pangram.") == false
```

###### **Example13: kebabize**

```ruby
=begin
Modify the kebabize function so that it converts a camel case string into a kebab case.

kebabize('camelsHaveThreeHumps') // camels-have-three-humps
kebabize('camelsHave3Humps') // camels-have-humps
Notes:

the returned string should only contain lowercase letters
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem: converrt thte given camel case to kebab case
Input:
  - String
  -
Output:
  - String
  -

=====> Rules
Explicit Requiremnts:
  - upper case/ lower case allowe
  - no special characters allowed
Implicit Requiremnts:
  - no empty string
  - no other datatype
  - ignore Integers

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p kebabize('myCamelCasedString') == 'my-camel-cased-string'
my
Camel
Cased
String

p kebabize('myCamelHas3Humps') == 'my-camel-has-humps'
my
Camel
Has
Humps

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
given the string. 
split the string into differents words with each new word having a lowercase ending
convert them into lower case and then form the new string by joining them with a '-'

=====> Optional Implementation (Pseudo-code):
split the string into a new array with element as words ending with the last lowercase letter in sequence
join the elements by "-"
lowercase the string
return the joined string
=end

# Code With Intent
def kebabize(str)
 str.gsub(/[^a-z]/i,'').split(/(?=[A-Z])/).join('-').downcase
end

p kebabize('myCamelCasedString') #== 'my-camel-cased-string'
p kebabize('myCamelHas3Humps') #== 'my-camel-has-humps'
```

###### **Example14:Dubstep**

```ruby
# def song_decoder(str)
#   str.gsub(/(WUB)/, "*").split("*").select { |ele| ele != "" }.join(" ")
# end

def song_decoder(str)
  str.gsub(/(WUB)+/, " ").strip
end

p song_decoder("AWUBBWUBC") #== "A B C"
p song_decoder("AWUBWUBWUBBWUBWUBWUBC") #== "A B C"
p song_decoder("WUBAWUBBWUBCWUB") #== "A B C"
p song_decoder("JKDWUBWBIRAQKFWUBYEWUBWV") #== "JKD WBIRAQKF YE WV"
```

###### **Example15: Ten min walk**

```ruby
=begin
You live in the city of Cartesia where all roads are laid out in a perfect grid. You arrived ten minutes too early to an appointment, so you decided to take the opportunity to go for a short walk. The city provides its citizens with a Walk Generating App on their phones -- everytime you press the button it sends you an array of one-letter strings representing directions to walk (eg. ['n', 's', 'w', 'e']). You always walk only a single block in a direction and you know it takes you one minute to traverse one city block, so create a function that will return true if the walk the app gives you will take you exactly ten minutes (you don't want to be early or late!) and will, of course, return you to your starting point. Return false otherwise.

Note: you will always receive a valid array containing a random assortment of direction letters ('n', 's', 'e', or 'w' only). It will never give you an empty array (that's not a walk, that's standing still!).
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem: Ten min walk each input is one block and takes 1 min to traverse a block and can only travel in one direction in a block
Input:
  - array of one lettered strings representing directions
  -
Output:
  - Boolean
  -

=====> Rules
Explicit Requiremnts:
  - n, s, w, e represents north, south, west, east
  - one direction is 1 min
  - can travel only in one direction for a given block
  - should come back ro the same spot after 10 mins
  - travel has to be 10mins
  - need 10 inputs
  - count of n ==s
  - count of w == e
Implicit Requiremnts:
  - no empty array
  - no other datatypes

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p is_valid_walk(['n','s','n','s','n','s','n','s','n','s']) #== true
5s's and 5n's . they neutraliz each other hence return to the same spot after 10 mins

p is_valid_walk(['w','e','w','e','w','e','w','e','w','e','w','e']) #== false
6w's and 6e's = 12 mins

p is_valid_walk(['w']) #== false
1 min


p is_valid_walk(['n','n','n','s','n','s','n','s','n','s']) #== false
6n's and 4s's 10 mins but not equal. hence did not return to the spot


=====> Data structure(s):
Input: array
Intermediate: array, hash
Output: boolean

=====> High Level Algorithm:
iterate through the given direction and check if the number of 'north' is equal to the south or the number of east equal to the west. Also the total count should be 10. otherwise you have not returned exactly in 10 mins

=====> Optional Implementation (Pseudo-code):
given array arr
return true if the arr.count != 10 
create a new hash with each unique element and its count
initialize the following
n_count = 0
s_count = 0
w_count = 0
e_count = 0

reassign the counts to the corresponding values
if the sum of the values == 10 && the number of n == s && the number of e == w return true


=end

# Code With Intent

def create_hash(arr)
  arr.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele] += 1 }
end

def check(arr, hsh)
  n_count = hsh['n'] 
  s_count = hsh['s'] 
  w_count = hsh['w']
  e_count = hsh['e'] 
  n_count == s_count && w_count == e_count if [n_count, s_count, w_count, e_count].sum == 10
end

def is_valid_walk(arr)
  return false if arr.count != 10
  hsh = create_hash(arr)
  check(arr, hsh) 
end

# option 2

# def create_hash(arr)
#   arr.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele] += 1 }
# end

# def check(arr, hsh)  
#   hsh['n'] == hsh['s'] && hsh['w'] == hsh['e'] if hsh.values.sum == 10
# end

# def is_valid_walk(arr)
#   return false if arr.count != 10
#   hsh = create_hash(arr)
#   check(arr, hsh) 
# end

p is_valid_walk(['n','s','n','s','n','s','n','s','n','s']) #== true
p is_valid_walk(['w','e','w','e','w','e','w','e','w','e','w','e']) #== false
p is_valid_walk(['w']) #== false
p is_valid_walk(['n','n','n','s','n','s','n','s','n','s']) #== false
```

###### **Example16: Reverse > 5**

```ruby
=begin
16. Stop gninnipS My sdroW!
(https://www.codewars.com/kata/5264d2b162488dc400000001)
6 kyu
Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

Examples: spinWords( "Hey fellow warriors" ) => returns "Hey wollef sroirraw"
=end

# def spin_words(string)
#   string.split.map { |ele| ele.length > 4 ? ele.reverse : ele }.join(" ")
# end

def spin_words(string)
  string.gsub(/\w{5,}/, &:reverse)
end

p spin_words("Hey fellow warriors") #== "Hey wollef sroirraw"
p spin_words("This is a test") #== "This is a test" 
p spin_words("This is another test") #== "This is rehtona test"
p spin_words("test") #== "test"
p spin_words("Welcome") #== "emocleW"
```

###### **Example17: Expanded numbers**

```ruby
def expanded_form(num) 
  num.digits.map(&:to_s)
  .map.with_index { |num, idx| num << ('0' * idx) }
  .reject { |ele| ele.chars.uniq.join == '0' }
  .reverse.join(" + ")
end

=begin
option 2
def expanded_form(num)
  num.to_s
     .chars
     .reverse
     .map.with_index { |d, idx| d.to_i * 10**idx }
     .reject(&:zero?)
     .reverse
     .join (' + ')
end
=end

p expanded_form(12) == '10 + 2'
p expanded_form(42) == '40 + 2'
p expanded_form(70304) == '70000 + 300 + 4'
```

###### **Example18: Persistent Bugger**

```ruby
=begin
Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

For example:

 persistence(39) # returns 3, because 3*9=27, 2*7=14, 1*4=4
                 # and 4 has only one digit

 persistence(999) # returns 4, because 9*9*9=729, 7*2*9=126,
                  # 1*2*6=12, and finally 1*2=2

 persistence(4) # returns 0, because 4 is already a one-digit number
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Positive parameter
  -
  -
Output: multiplicative persistence until single digit is reached
  - no of times multiplied
  -

=====> Rules
Explicit Requiremnts:
  - only positive number is allowed
  - mutiply the digits untill singlge number is reached
Implicit Requiremnts:
  - no other datatype
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p persistence(39) == 3
3 * 9 = 27
2 * 7 = 14
1 * 4 = 4

p persistence(4) == 0
single digit then 0

p persistence(25) == 2
2* 5 = 10
1 * 0 = 0

p persistence(999) == 4
9*9*9 = 729
7*2*9 = 126
1*2*6 = 12
1*2 = 2

=====> Data structure(s):
Input: number
Intermediate: array
Output: Integer

=====> High Level Algorithm:
take a positive number and multiply its digits persistently untill a single digit is acheived

=====> Optional Implementation (Pseudo-code):
Create a new array arr and assign the first value of its element to the Integer given
split the last element in the array by induvidual elements in a new array
multiply the elements in the new array and append them to the array arr
do this until a single digit is reached
return the count of arr - 1

=end

# Code With Intent

def persistence(num)
  arr = [num]
  until arr.last.digits.length == 1
    arr << arr.last.digits.reduce(:*)
  end
  arr.length - 1
end

=begin
### OPtion 2
def persistence(num)
  arr = [num]
  while arr.last.digits.length > 1
    arr << arr.last.digits.reduce(:*)
  end
  arr.length - 1
end
=end

=begin
### Recursion 
def persistence(num)
  arr = [] 
  arr[0] = num if arr.empty?
  return 0 if num.digits.length < 2 # Base case
  while num.digits.length > 1
    num = num.digits.reduce(:*)
    arr << num
    persistence(num) # recursive case
  end
  arr.length - 1

### More recursion
	def persistence(n)
  	n < 10 ? 0 : 1 + persistence(n.digits.reduce(:*))
	end
end

p persistence(39) == 3
p persistence(4) == 0
p persistence(25) == 2
p persistence(999) == 4

p persistence(39) == 3
p persistence(4) == 0
p persistence(25) == 2
p persistence(999) == 4
```

###### **Example19: Title Case**

```ruby
=begin
A string is considered to be in title case if each word in the string is either (a) capitalised (that is, only the first letter of the word is in upper case) or (b) considered to be an exception and put entirely into lower case unless it is the first word, which is always capitalised.

Write a function that will convert a string into title case, given an optional list of exceptions (minor words). The list of minor words will be given as a string with each word separated by a space. Your function should ignore the case of the minor words string -- it should behave in the same way even if the case of the minor word string is changed.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
convert the first argument into TITLE case

Input: strings
  - first argument is to be converted to A TITLE CASE  
  - second argumentis the exception
Output: 
  - title cased string
  - 

=====> Rules
Explicit Requiremnts:
  - First word has to be capitalised regardless
  - rest of the words have to be capitalised unless the following
  - the send arguments has to be ignored while capitalizing
  - if no second argument then no exceptions and 
  - no second arg so all words are capitalised
Implicit Requiremnts:
  - no other datatypes
  - no special characters

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p title_case('a clash of KINGS', 'a an the of') #== 'A Clash of Kings'
all words capitalized except 'of' from second arg
'A' is still capitalized as it is in the beginning

p title_case('THE WIND IN THE WILLOWS', 'The In') #== 'The Wind in the Willows'
'in' is still kept in lowercase as it is an exception in the second arg


p title_case('the quick brown fox') #== 'The Quick Brown Fox'
no second arg so all words are capitalised


=====> Data structure(s):
Input: Strings
Intermediate: Array
Output: string

=====> High Level Algorithm:
Iterate through the words and capitalise each word unless it is part of the exception in the second argument. Ignore any exception if the exception is the first word. Exceptions otherwise should be lower case inthe first argument

=====> Optional Implementation (Pseudo-code):
Split the first argument into an array 'arr' and lowercase all the elements
If no second argument then capitalize all the words and return the joined string by space
if second arg present
  split the second arg into an array arr2 and lowercase all the elements
  iterate thrugh arr and for each element check if it is present in arr2.
  if present then move on to the next word
  else capitalize it.
  Join all the words in arr by " "
  capitalize the first word in arr
  join the words in arr by " "
  return the joined string

=end

# Code With Intent

def split_str(string)
  string.split(" ").map(&:downcase)
end

def title_case(str, check="")
  arr = split_str(str)
  arr2 = split_str(check)
  return "" if arr.empty?
  
  arr.map { |ele| arr2.include?(ele) ? ele : ele.capitalize! } 
  arr[0].capitalize!
  arr.join(" ")
end

### Option 2
def title_case(str, option="")
  str.capitalize.gsub(/\w+/) { |ele| option[/\b#{ele}\b/i] ? ele : ele.capitalize }
end

p title_case('a clash of KINGS', 'a an the of') == 'A Clash of Kings'
p title_case('THE WIND IN THE WILLOWS', 'The In') == 'The Wind in the Willows'
p title_case('the quick brown fox') == 'The Quick Brown Fox'
p title_case("First A Of In", "an often into") == "First A Of In"
```

###### **Example 20: Count & group char**

```ruby
=begin
Write a method that takes a string as an argument and groups the number of times each character appears in the string as a hash sorted by the highest number of occurrences.

The characters should be sorted alphabetically e.g:

get_char_count("cba") => {1=>["a", "b", "c"]}
You should ignore spaces, special characters and count uppercase letters as lowercase ones.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Write a method that takes a string as an argument and groups the number of times each character appears in the string as a hash sorted by the highest number of occurrences.

Input:
  - string
  -
Output:
  - hash with each character count as key and unique chars in array as values
  -

=====> Rules
Explicit Requiremnts:
  - ignore special characters
  - no other datatypes
  - keys == count
  - value == array of uniq chars
Implicit Requiremnts:
  - upper case allowed
  - all returned chars are lowercase

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p get_char_count("Mississippi") == 
{4=>["i", "s"], 2=>["p"], 1=>["m"]}

p get_char_count("Hello. Hello? HELLO!!") == 
{6=>["l"], 3=>["e", "h", "o"]}

p get_char_count("aaa...bb...c!") == 
{3=>["a"], 2=>["b"], 1=>["c"]}

=====> Data structure(s):
Input: string
Intermediate: hash, array
Output: hash, array

=====> High Level Algorithm:
iterate over the given word and count the number of times each characters occur. Insert the collected information into a hash where the key represents the total count of a character and the corresponding values are the array containing the uniq characters

=====> Optional Implementation (Pseudo-code):
split the word into array containing letters
group by the count of number of occurances of the letters as keys and the corresponding values to an array of uniq characters
ignore any special characters
return the hash

=end
  
# Code With Intent

def create_hash(word)
  word.downcase.scan(/[a-z0-9]/i).each_with_object(Hash.new(0)) { |ele, h| h[ele] += 1 }
end

def get_char_count(word)
  hsh = create_hash(word)
  new_hash = {}
  hsh.each do |k, v| 
    new_hash.has_key?(v) ? new_hash[v] << k : new_hash[v] = [k]
  end
  new_hash.to_h.values.each { |arr| arr.sort! }
  new_hash
end

### Option 2
def get_char_count(str)
  str = str.downcase.gsub(/\W/, '')
  frequencies = str.chars.uniq.group_by { |char| str.count(char) }
  frequencies.transform_values(&:sort)
end

p get_char_count("Mississippi") == {4=>["i", "s"], 2=>["p"], 1=>["m"]}
p get_char_count("Hello. Hello? HELLO!!") == {6=>["l"], 3=>["e", "h", "o"]}
p get_char_count("aaa...bb...c!") == {3=>["a"], 2=>["b"], 1=>["c"]}
p get_char_count("aaabbbccc") == {3=>["a", "b", "c"]}
p get_char_count("abc123") == {1=>["1", "2", "3", "a", "b", "c"]}
```

###### **Example21: Find the Mine**

```ruby
=begin
You've just discovered a square (NxN) field and you notice a warning sign. The sign states that there's a single bomb in the 2D grid-like field in front of you.

Write a function mineLocation/MineLocation that accepts a 2D array, and returns the location of the mine. The mine is represented as the integer 1 in the 2D array. Areas in the 2D array that are not the mine will be represented as 0s.

The location returned should be an array (Tuple<int, int> in C#) where the first element is the row index, and the second element is the column index of the bomb location (both should be 0 based). All 2D arrays passed into your function will be square (NxN), and there will only be one mine in the array.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Write a function mineLocation/MineLocation that accepts a 2D array, and returns the location of the mine. The mine is represented as the integer 1 in the 2D array. Areas in the 2D array that are not the mine will be represented as 0s.

Input: nested array
  -
  -
Output:
  - array 
  -

=====> Rules
Explicit Requiremnts:
  - 1s are represented by the location of the mine
  - 0s represents the free area where there is no mine
Implicit Requiremnts:
  - has to be nested array
  - each array has to have 3 elements 0s or 1s
  - no other datatypes allowed
  - returns an array with 2 elements

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p mineLocation( [ [1, 0, 0], [0, 0, 0], [0, 0, 0] ] ) #== [0, 0]
1 present inthe nested array at location 0
within the nested array the 1 is present in the index 0

p mineLocation( [ [0, 0, 0], [0, 1, 0], [0, 0, 0] ] ) #== [1, 1]
nested array location 1
element location within the array 1

p mineLocation( [ [0, 0, 0], [0, 0, 0], [0, 1, 0] ] ) #== [2, 1]
nested array location 2
element location within the array 1

=====> Data structure(s):
Input: array
Intermediate: array
Output: array

=====> High Level Algorithm:
iterate through the given array and find out the location of the nested array and the loction or index within which the mine is located

=====> Optional Implementation (Pseudo-code):
iterate through the nested array
check if each nested array has 1
if yes then note the index of the nested array. 
  note the position of 1 within the array
else move on to the next array and repeat the above

return the position of 1 in an array

=end

# Code With Intent

def mineLocation(arr)
  arr.each_with_index { |narr, idx| return [idx, narr.index(1)] if narr.include?(1) }
end

p mineLocation( [ [1, 0, 0], [0, 0, 0], [0, 0, 0] ] ) == [0, 0]
p mineLocation( [ [0, 0, 0], [0, 1, 0], [0, 0, 0] ] ) == [1, 1]
p mineLocation( [ [0, 0, 0], [0, 0, 0], [0, 1, 0] ] ) == [2, 1]
```

###### **Example22: Scramblies**

```ruby
=begin
Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.

Notes:

Only lower case letters will be used (a-z). No punctuation or digits will be included.
Performance needs to be considered
Input strings s1 and s2 are null terminated.
=end


=begin
========== THE PEDAC PROCESS ==========

=====> Problem:

Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.

Input: string
  -
  -
Output: boolean
  -
  -

=====> Rules
Explicit Requiremnts:
  Only lower case letters will be used (a-z). No punctuation or digits will be included.
  Performance needs to be considered
  Input strings s1 and s2 are null terminated.
  
Implicit Requiremnts:
  - no other datatypes
  - no empty string

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p scramble('rkqodlw', 'world') #== true

p scramble('cedewaraaossoqqyt', 'codewars') #== true
p scramble('katas', 'steak') #== false
p scramble('rkqodlw','world') #== true
p scramble('cedewaraaossoqqyt','codewars') #== true
p scramble('katas','steak') #== false
p scramble('scriptjava','javascript') #== true
p scramble('scriptingjava','javascript') #== true


=====> Data structure(s):
Input: string
Intermediate: array
Output: boolean

=====> High Level Algorithm:
compare the two arguments and check if you can form the second argument from the first argument

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def scramble(str1, str2)
  hsh1 = str1.scan(/[#{str2}]/).tally
  hsh2 = str2.chars.tally
  hsh2.all? { |k, v| hsh1.has_key?(k) ? hsh1[k] >= v : false }
end

### Option 2
def scramble(s1, s2)
  s2.chars.uniq.none? { |c| s1.count(c) < s2.count(c) }
end

### Option 3
def scramble(s1, s2)
  s2.chars.uniq.all? { |ele| s1.count(ele) >= s2.count(ele) }
end

p scramble('rkqodlw', 'world') #== true
p scramble('cedewaraaossoqqyt', 'codewars') #== true
p scramble('katas', 'steak') #== false
p scramble('rkqodlw','world') #== true
p scramble('cedewaraaossoqqyt','codewars') #== true
p scramble('katas','steak') #== false
p scramble('scriptjava','javascript') #== true
p scramble('scriptingjava','javascript') #== true
```

###### **Example23: Longest substring**

```ruby 
=begin
Example: the longest alphabetical substring in "asdfaaaabbbbcttavvfffffdf" is "aaaabbbbctt".

There are tests with strings up to 10 000 characters long so your code will need to be efficient.

The input will only consist of lowercase characters and will be at least one letter long.

If there are multiple solutions, return the one that appears first.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
find the longest alphabetical substring
Input:
  - string
  -
Output:
  - hash tag
  - false

=====> Rules
Explicit Requiremnts:
  - min one letter long
  - all are lowercase
  - 
Implicit Requiremnts:
  - capture the words occuring in sequence
  - repeating letters are part of the same sequence
  - If only one letter then return it
  - no sequence then return the first letter

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p longest('asd') == 'as'
a,s 
d comes before s hence it is not in sequence

p longest('nab') == 'ab'
a, b

p longest('abcdeapbcdef') == 'abcde'
'abcde'

p longest('asdfaaaabbbbcttavvfffffdf') == 'aaaabbbbctt'
'asdfaaaabbbbctt'. all of them are in sequence even though the letters are repeated

p longest('asdfbyfgiklag') =='fgikl'


p longest('z') == 'z'
z

p longest('zyba') == 'z'
z

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
iterate through the letters and collect the letters in sequence. 

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def longest(str)
  arr = []
  (1..str.length).each { |e| str.chars.each_cons(e) { |ele| arr << ele } }
  arr = arr.select do |sub_arr|
    sub_arr.map(&:ord) == sub_arr.sort.map(&:ord) 
  end
  hsh = arr.group_by { |inner_arr| inner_arr.count }
  hsh.select { |k, _| hsh.keys.max == k }.values.first.first.join
end

### Option 2
def longest(str)
  str.chars.slice_when { |a, b| a > b }.max_by(&:size).join
end

### Option 3
REGEX = ('a'..'z').to_a.join('*') + '*'

def longest(s)
  s.scan(/#{REGEX}/).max_by(&:size)
end

p longest('asd') #== 'as'
p longest('nab') #== 'ab'
p longest('abcdeapbcdef') #== 'abcde'
p longest('asdfaaaabbbbcttavvfffffdf') #== 'aaaabbbbctt'
p longest('asdfbyfgiklag') #=='fgikl'
p longest('z') #== 'z'
p longest('zyba') #== 'z'

```

###### **Example24: The hash tag generator** 

```ruby 
=begin
The marketing team is spending way too much time typing in hashtags.
Let's help them with our own Hashtag Generator!

Here's the deal:

It must start with a hashtag (#).
All words must have their first letter capitalized.
If the final result is longer than 140 chars it must return false.
If the input or the result is an empty string it must return false.
Examples
" Hello there thanks for trying my Kata"  =>  "#HelloThereThanksForTryingMyKata"
"    Hello     World   "                  =>  "#HelloWorld"
""                                        =>  false
=end

=begin
========== THE PEDAC PROCESS ==========
Create a hash tag generator

=====> Problem:
Input: 
  - string
  -
Output:
  - string
  -

=====> Rules
Explicit Requiremnts:
  - all lwords first letter capitalized
  - false if the final result > 140 chars
  - empty string returns false
Implicit Requiremnts: 
  - join all the string and prepend # to it
  - no other special chars or other datatypes

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p generateHashtag("") == false

p generateHashtag(" " * 200) == false

p generateHashtag("Do We have A Hashtag") == "#DoWeHaveAHashtag"

p generateHashtag("Codewars") == "#Codewars"

p generateHashtag("Codewars Is Nice") ==  "#CodewarsIsNice"

p generateHashtag("Codewars is nice") == "#CodewarsIsNice"

p generateHashtag("code" + " " * 140 + "wars") == "#CodeWars"
final string is less than 140 chars long

p generateHashtag("Looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong Cat") == false
 > 140 chars

p generateHashtag("a" * 139) == "#A" + "a" * 138
< 140 chars

p generateHashtag("a" * 140) == false
> 140 chars

 
=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
Create a hash tag by joining all the words after capitalizing them and then adding the # in front of it

=====> Optional Implementation (Pseudo-code):
return false if str.split.empty?
split the string into an array of induvidual words 'arr'
iterate through the array and capitalize all the induvidual words
join all the words to form a string
return true if the overall length of the string is < 140 chars long
append the `#` to the front of teh string
else return false if length > 140


=end

# Code With Intent

def generateHashtag(str)
  return false if str.split.empty?
  arr = str.split.map(&:capitalize)
  arr.join.length + 1 > 140 ? false : "#" + "#{arr.join}"
end

## option 2
def generateHashtag(str)
  return false if str.split.empty?
  hsh_tag = "#"
  str.split.each { |word| hsh_tag << word.capitalize }
  hsh_tag.length > 140 ? false : hsh_tag
end

p generateHashtag("") == false
p generateHashtag(" " * 200) == false
p generateHashtag("Do We have A Hashtag") == "#DoWeHaveAHashtag"
p generateHashtag("Codewars") == "#Codewars"
p generateHashtag("Codewars Is Nice") ==  "#CodewarsIsNice"
p generateHashtag("Codewars is nice") == "#CodewarsIsNice"
p generateHashtag("code" + " " * 140 + "wars") == "#CodeWars"
p generateHashtag("Looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong Cat") == false
p generateHashtag("a" * 139) == "#A" + "a" * 138
p generateHashtag("a" * 140) == false
```

###### **Example25: Pete the baker**

```ruby
=begin
Pete likes to bake some cakes. He has some recipes and ingredients. Unfortunately he is not good in maths. Can you help him to find out, how many cakes he could bake considering his recipes?

Write a function cakes(), which takes the recipe (object) and the available ingredients (also an object) and returns the maximum number of cakes Pete can bake (integer). For simplicity there are no units for the amounts (e.g. 1 lb of flour or 200 g of sugar are simply 1 or 200). Ingredients that are not present in the objects, can be considered as 0.

Examples:

// must return 2
cakes({flour: 500, sugar: 200, eggs: 1}, {flour: 1200, sugar: 1200, eggs: 5, milk: 200}); 
// must return 0
cakes({apples: 3, flour: 300, sugar: 150, milk: 100, oil: 100}, {sugar: 500, flour: 2000, milk: 2000}); 
=end


=begin
========== THE PEDAC PROCESS ==========

=====> Problem:

Write a function cakes(), which takes the recipe (object) and the available ingredients (also an object) and returns the maximum number of cakes Pete can bake (integer). For simplicity there are no units for the amounts (e.g. 1 lb of flour or 200 g of sugar are simply 1 or 200). Ingredients that are not present in the objects, can be considered as 0.

Input: 
  - hash objects containing the ingredients
  - 
Output:
  - output has to be the number of cakes Pete can make. 
  - Integer

=====> Rules
Explicit Requiremnts:
  - ANy missinng ingredient has the value 0
  - 1 lb of flour == 1
  - 200 gm of sugar == 200
Implicit Requiremnts:
  - return the min quatity of cakes you can make
  - no special characters

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p cakes({"flour"=>500, "sugar"=>200, "eggs"=>1},{"flour"=>1200, "sugar"=>1200, "eggs"=>5, "milk"=>200}) #== 2
totel no of cakes == 2
f = 1200 = 2 
s = 1200
e = 5
m = 200


p cakes({"cream"=>200, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>1700, "flour"=>20000, "milk"=>20000, "oil"=>30000, "cream"=>5000}) #== 11
c = 200r  5000    25
f = 300   20000   66
s = 150   1700    11
m = 100   20000   20
o = 100   30000   30


p cakes({"apples"=>3, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>500, "flour"=>2000, "milk"=>2000}) #== 0

p cakes({"apples"=>3, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>500, "flour"=>2000, "milk"=>2000, "apples"=>15, "oil"=>20}) #== 0

p cakes({"eggs"=>4, "flour"=>400},{}) #== 0

p cakes({"cream"=>1, "flour"=>3, "sugar"=>1, "milk"=>1, "oil"=>1, "eggs"=>1},{"sugar"=>1, "eggs"=>1, "flour"=>3, "cream"=>1, "oil"=>1, "milk"=>1}) #== 1


=====> Data structure(s):
Input: Hash
Intermediate: hash, array
Output: integer

=====> High Level Algorithm:
compare the available ingredient with the required ingredient and determine how many cakes can be made

=====> Optional Implementation (Pseudo-code):
create a new array arr
check if all the required ingredients are present in the available ingredients
if no
  return 0
otherwise 
  iterate through the available ingredients hash and divide the associated value by hte value of the required ingredients. capture the return value in arr,
  select the smallest value in the arr and return it

=end

# Code With Intent

def cakes(required, available)
  arr = []
  return 0 if !required.keys.all? { |key, _| available.has_key?(key) } 
  required.each { |name, amount| arr << available[name] / amount }
  arr.min
end

p cakes({"flour"=>500, "sugar"=>200, "eggs"=>1},{"flour"=>1200, "sugar"=>1200, "eggs"=>5, "milk"=>200}) == 2
p cakes({"cream"=>200, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>1700, "flour"=>20000, "milk"=>20000, "oil"=>30000, "cream"=>5000}) == 11
p cakes({"apples"=>3, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>500, "flour"=>2000, "milk"=>2000}) == 0
p cakes({"apples"=>3, "flour"=>300, "sugar"=>150, "milk"=>100, "oil"=>100},{"sugar"=>500, "flour"=>2000, "milk"=>2000, "apples"=>15, "oil"=>20}) == 0
p cakes({"eggs"=>4, "flour"=>400},{}) == 0
p cakes({"cream"=>1, "flour"=>3, "sugar"=>1, "milk"=>1, "oil"=>1, "eggs"=>1},{"sugar"=>1, "eggs"=>1, "flour"=>3, "cream"=>1, "oil"=>1, "milk"=>1}) == 1

```

###### **Example26: Mean Square Error**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Complete the function that

accepts two integer arrays of equal length
compares the value each member in one array to the corresponding member in the other
squares the absolute value difference between those two values
and returns the average of those squared absolute value difference between each member pair.

Input: arrays

Output: integer

=====> Rules
Explicit Requiremnts:
  - two arrays with equal number of Integers as elements
  - 
Implicit Requiremnts:
  - can return a float
  - no other data types
  - negative integers allowed in the array

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solution([1, 2, 3], [4, 5, 6]) == 9
[1, 2, 3], [4, 5, 6]              -->   9   because (9 + 9 + 9) / 3

p solution([10, 20, 10, 2], [10, 25, 5, -2]) == 16.5
[10, 20, 10, 2], [10, 25, 5, -2]  -->  16.5 because (0 + 25 + 25 + 16) / 4

p solution([-1, 0], [0, -1]) == 
[-1, 0], [0, -1]                  -->   1   because (1 + 1) / 2

=====> Data structure(s):
Input: array
Intermediate: array
Output: integer

=====> High Level Algorithm:
compare each elemnts in the corresponding array and find the square of the remainder. Summ all the squares and find the mean

=====> Optional Implementation (Pseudo-code):
create a new array arr with each corresponding elements as nested array 
[1, 2, 3], [4, 5, 6]  ==> arr = [1, 4],[2, 5][3, 6]

find the difference of each nested array [1, 4],[2, 5][3, 6] => [-3][-3][-3]
find the square root of each element [-3][-3][-3] => 9, 9, 9
find the mean of them ( 9 + 9 + 9 ) / 3 => 9
return the mean
=end

# Code With Intent

def solution(arr1, arr2)
  arr1.zip(arr2).map { |num1, num2| (num1 - num2) ** 2 }.sum / arr1.size.to_f
end

p solution([1, 2, 3], [4, 5, 6]) == 9
p solution([10, 20, 10, 2], [10, 25, 5, -2]) == 16.5
p solution([-1, 0], [0, -1]) == 1
```

###### **Example27: Exponent method**

```ruby
=begin


Note: The ** operator has been disabled.

Examples:
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Create a method called "power" that takes two integers and returns the value of the first argument raised to the power of the second. Return nil if the second argument is negative.

Input: integers

Output: integer

=====> Rules
Explicit Requiremnts:
  - given two integers
  - returns an integer
Implicit Requiremnts:
  - negative integers allowed
  - no other data types or other charated allowed

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p power(2, 3) == 8
2**3

p power(10, 0) == 1
10**0

p power(-5, 3) == -125
(-5)**3

p power(-4, 2) == 16
-4 ** 2

p power(10, 0) == 1

p power(2, 3) == 8

p power(3, 2) == 9

p power(-5, 3) == -125

p power(-4, 2) == 16

p power(8, -2) == nil
negative power hence nil


=====> Data structure(s):
Input: integer
Intermediate: integer
Output:integer

=====> High Level Algorithm:
if the second argument is negatibe then retuen nil else return the value of the first argument raised to the power of the seconf argument

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def power(num1, num2)
  num2 < 0 ? nil : num2 == 0 ? 1 : ([num1] * num2).reduce(:*)
end

p power(2, 3) == 8
p power(10, 0) == 1
p power(-5, 3) == -125
p power(-4, 2) == 16
p power(10, 0) == 1
p power(2, 3) == 8
p power(3, 2) == 9
p power(-5, 3) == -125
p power(-4, 2) == 16
p power(8, -2) == nil
```

###### **Example28: Where are my anagrams**

```ruby
=begin
What is an anagram? Well, two words are anagrams of each other if they both contain the same letters. For example:

'abba' & 'baab' == true

'abba' & 'bbaa' == true

'abba' & 'abbba' == false

'abba' & 'abca' == false
For example:
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Write a function that will find all the anagrams of a word from a list. You will be given two inputs a word and an array with words. You should return an array of all the anagrams or an empty array if there are none. 

Input: 2 arguments
string 
array

Output: array of anagrams 

=====> Rules
Explicit Requiremnts:
  - first argument is a sttring
  - second arguments is an array of strings with possible anagrams to the first argument
Implicit Requiremnts:
  - no other datatypes or special characters
  -  all the strings are lowercase
  - case sensitive

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p anagrams('abba', ['aabb', 'abcd', 'bbaa', 'dada']) == ['aabb', 'bbaa']

p anagrams('racer', ['crazer', 'carer', 'racar', 'caers', 'racer']) == ['carer', 'racer']

p anagrams('laser', ['lazing', 'lazy',  'lacer']) == []


=====> Data structure(s):
Input: string, array
Intermediate: array
Output: array

=====> High Level Algorithm:
iterate through the second argument array and and collect all the anagrams into a new array. if no anagram then return an empty array

=====> Optional Implementation (Pseudo-code):
string, array ------> anagrams(str, arr) --------> array
intitlize an empty array final_arr = []
loop through the arr and match the current element with str
if matched 
  arr << current element
return final_arr

=end

# Code With Intent

def anagrams(str, arr)
  final_arr = []
  new_arr = arr.select { |word| word.length == str.length }
  new_arr.each { |ele| final_arr << ele if ele.scan(/[#{str}]/).sort.join == str.chars.sort.join }
  final_arr
end

# Option 2
def anagrams(str, arr)
  arr.select { |w| w.chars.sort == str.chars.sort }
end

p anagrams('abba', ['aabb', 'abcd', 'bbaa', 'dada']) #== ['aabb', 'bbaa']
p anagrams('racer', ['crazer', 'carer', 'racar', 'caers', 'racer']) #== ['carer', 'racer']
p anagrams('laser', ['lazing', 'lazy',  'lacer']) #== []

```

###### **Example29: Split Strings**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Complete the solution so that it splits the string into pairs of two characters. If the string contains an odd number of characters then it should replace the missing second character of the final pair with an underscore ('_').

Input: string

Output: array

=====> Rules
Explicit Requiremnts:
  - split the string into even pairs
  - if last pair is odd then add '_' to the missing second character
  - empty string allowed
Implicit Requiremnts:
  - all lowercase
  - no other datatype

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p solution('abc') == ['ab', 'c_']
ab, c << _

p solution('abcdef') == ['ab', 'cd', 'ef']
ab, cd, ef

p solution("abcdef") == ["ab", "cd", "ef"]

p solution("abcdefg") == ["ab", "cd", "ef", "g_"]

p solution("") == []

=====> Data structure(s):
Input: string
Intermediate: array
Output: array

=====> High Level Algorithm:
split the letters into pairs. insert '_' as the secong letter to the complete the pair if only one letter is present within the pair

=====> Optional Implementation (Pseudo-code):
solution(str) ------> array
initialize an empty array arr
split str into pairs and push them to arr
iterate through arr and transform any odd pair by appending '_' to it to complete the pair
join all the sub arrays 
return arr
=end

# Code With Intent

def solution(str)
  arr = []
  str.chars.each_slice(2) { |pair| arr << pair }
  arr.map { |ele| ele.count == 2 ? ele : ele << "_" }.map(&:join)
end

# Option 2
def solution(str)
  (str + '_').scan(/../)
end

p solution('abc') == ['ab', 'c_']
p solution('abcdef') == ['ab', 'cd', 'ef']
p solution("abcdef") == ["ab", "cd", "ef"]
p solution("abcdefg") == ["ab", "cd", "ef", "g_"]
p solution("") == []
```

###### **Example30: Anagram Difference**

```ruby
=begin
Given two words, how many letters do you have to remove from them to make them anagrams?
Example
First word : c od e w ar s (4 letters removed)
Second word : ha c k er r a nk (6 letters removed)
Result : 10
Hints
A word is an anagram of another word if they have the same letters (usually in a different order).
Do not worry about case. All inputs will be lowercase.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given two words, how many letters do you have to remove from them to make them anagrams?

Input: two strings

Output: integer

=====> Rules
Explicit Requiremnts:
  - given two stringss
  - all lowercase
Implicit Requiremnts:
  - empty string alloweed
  - when no match return the length of the second argument

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p anagram_difference('', '') == 0


p anagram_difference('a', '') == 1

p anagram_difference('', 'a') == 1

p anagram_difference('ab', 'a') == 1

p anagram_difference('ab', 'ba') == 0

p anagram_difference('ab', 'cd') == 4
remove 2 from first argument
remover 2 from the second argument
total 4 removed

p anagram_difference('aab', 'a') == 2
ab removed from first arg

p anagram_difference('a', 'aab') == 2
ab removed from second arg 

p anagram_difference('codewars', 'hackerrank') == 10
common ["d", "o", "s", "w"]
removed first arg = c a r e
removed second arg = ["a", "a", 'c', "e", "h", "k", "k", "n", "r", "r"]


=====> Data structure(s):
Input: strings
Intermediate:array
Output: inTeger

=====> High Level Algorithm:
compare the two strings. remove the letters from the larger string which is present in the smaller string(this is only if all the letters are present in the larger string) to form an anagram. If no letter to compare then remove all the letters. If partly present in both the strings then remove in both  and capture the total count of removed items to make the anagram

=====> Optional Implementation (Pseudo-code):
anagram_difference(str1, str2) ---------> Interger count of the removed letters

=end

# Code With Intent

# def anagram_difference(w1, w2)
#   ("a".."z").sum { |l| (w1.count(l) - w2.count(l)).abs }
# end

def anagram_difference(str1,str2)
  str1_split = str1.chars
  str2_split = str2.chars
  common_chars = ''
  str1_split.each do |outer|
    if str2_split.include?(outer)
      common_chars << outer if common_chars.count(outer) < [str1.count(outer), str2.count(outer)].min
    end
  end
  (str1_split.size - common_chars.size) + (str2_split.size - common_chars.size)
end

p anagram_difference('', '') == 0
p anagram_difference('a', '') == 1
p anagram_difference('', 'a') == 1
p anagram_difference('ab', 'a') == 1
p anagram_difference('ab', 'ba') == 0
p anagram_difference('ab', 'cd') == 4
p anagram_difference('aab', 'a') == 2
p anagram_difference('a', 'aab') == 2
p anagram_difference('codewars', 'hackerrank') == 10
```

###### **Example31: Anagram Detection**

```ruby
=begin
An anagram is the result of rearranging the letters of a word to produce a new word (see wikipedia).

Note: anagrams are case insensitive

Complete the function to return true if the two arguments given are anagrams of each other; return false otherwise.

Examples
"foefet" is an anagram of "toffee"

"Buckethead" is an anagram of "DeathCubeK"
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Complete the function to return true if the two arguments given are anagrams of each other; return false otherwise.

Input: strings

Output: Boolean

=====> Rules
Explicit Requiremnts:
  - case insensitive
  - 
Implicit Requiremnts:
  -
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p is_anagram('Creative', 'Reactive') == true


p is_anagram("foefet", "toffee") == true


p is_anagram("Buckethead", "DeathCubeK") == true


p is_anagram("Twoo", "WooT") == true


p is_anagram("dumble", "bumble") == false


p is_anagram("ound", "round") == false


p is_anagram("apple", "pale") == false



=====> Data structure(s):
Input: strings
Intermediate: array
Output: boolean

=====> High Level Algorithm:
compare the two given strings and find out if they are anagrams case insensitively.

=====> Optional Implementation (Pseudo-code):
is_anagram(str1, str2) -------> Boolean

downcase and split all the letters in  str1 as elements in a newarray arr1 
downcase and split all the letters in  str2 as elements in a newarray arr2
compare the two arrays after sorting them and return the Boolean of the expression
arr1.sort == arr2.sort

=end

# Code With Intent

def split_into_arr(str)
  str.downcase.split("").sort
end

def is_anagram(str1, str2)
  split_into_arr(str1) == split_into_arr(str2)
end

p is_anagram('Creative', 'Reactive') == true
p is_anagram("foefet", "toffee") == true
p is_anagram("Buckethead", "DeathCubeK") == true
p is_anagram("Twoo", "WooT") == true
p is_anagram("dumble", "bumble") == false
p is_anagram("ound", "round") == false
p is_anagram("apple", "pale") == false
```

###### **Example32: highest scoring word**

```ruby
=begin
Given a string of words, you need to find the highest scoring word.

Each letter of a word scores points according to its position in the alphabet: a = 1, b = 2, c = 3 etc.

You need to return the highest scoring word as a string.

If two words score the same, return the word that appears earliest in the original string.

All letters will be lowercase and all inputs wabideill be valid.
=end

def high(str)
  hsh = ("a".."z").to_a.zip((1..26).to_a).to_h
  h = str.split.group_by { |ele| ele.chars.sum { |l| hsh[l] } }
  h.select { |k, v| k == h.keys.max }.values.first.first
end

p high('man i need a taxi up to ubud') == 'taxi'
p high('what time are we climbing up the volcano') == 'volcano'
p high('take me to semynak') == 'semynak'
p high('aaa b') == 'aaa'
```

###### **Example33: Replace alpha position**

```ruby
=begin
In this kata you are required to, given a string, replace every letter with its position in the alphabet.

If anything in the text isn't a letter, ignore it and don't return it.

"a" = 1, "b" = 2, etc.

Example
alphabet_position("The sunset sets at twelve o' clock.")
Should return "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11" (as a string)
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:

In this kata you are required to, given a string, replace every letter with its position in the alphabet.

Input: string
 
Output: string

=====> Rules
Explicit Requiremnts:
  - ignore non alphabets
  -
Implicit Requiremnts:
  - ignore spaces
  - case insensitive

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p alphabet_position("The sunset sets at twelve o' clock.") == "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11"
p alphabet_position("-.-'") == ""

=====> Data structure(s):
Input: string
Intermediate: array
Output: string


=====> High Level Algorithm:
Iterate through the string and replace the current letter by its position in the alphabets

=====> Optional Implementation (Pseudo-code):
create a hash hsh for the alphabet/position key/value association
scan the string and split it to a new array 'arr' ignoring cases
transform the arr repalcing the elements by the corrsponding positions from the hash hsh in string representation
join this new array by " "
return the joined string
=end

# Code With Intent

def alphabet_position(str)
  hsh = ("a".."z").to_a.zip((1..26).to_a).to_h
  arr = str.scan(/[a-z]/i)
  arr.map { |ele| hsh[ele.downcase].to_s }.join(" ")
end

p alphabet_position("The sunset sets at twelve o' clock.") == "20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11"
p alphabet_position("-.-'") == ""
```

###### **Example34: Sherlock on Pockets**

```ruby
=begin
Sherlock has to find suspects on his latest case. He will use your method, dear Watson. Suspect in this case is a person which has something not allowed in his/her pockets.

Allowed items are defined by array of numbers.

Pockets contents are defined by map entries where key is a person and value is one or few things represented by an array of numbers (can be nil or empty array if empty), example:

pockets = { 
  bob: [1],
  tom: [2, 5],
  jane: [7]
} 

Write a method which helps Sherlock to find suspects. If no suspect is found or there are no pockets (pockets == nil), the method should return nil.

=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:

Write a method which helps Sherlock to find suspects. If no suspect is found or there are no pockets (pockets == nil), the method should return nil.

Input: hash, arr

Output: arr

=====> Rules
Explicit Requiremnts:
  - empty array allowed
  - 2 args - hsh, arr
Implicit Requiremnts:
  - no other datatypes
  - 2nd arg is an array of integers

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p find_suspects(pockets, [1, 2]) == [:tom, :jane]
1 is allowed by bob hence he is not a suspect
5 is not there hence Tom is a suspect
1 and 2 is not there hence jane is a suspect

p find_suspects(pockets, [1, 7, 5, 2]) == nil
no suspects

p find_suspects(pockets, []) == [:bob, :tom, :jane]
empty arr so all are suspects

p find_suspects(pockets, [7]) == [:bob, :tom]

=====> Data structure(s):
Input: hash, array
Intermediate: array, hash
Output: array / nil

=====> High Level Algorithm:
iterate through the second argument and select the people whose items are missing from the pockets hash


=====> Optional Implementation (Pseudo-code):
find_suspects(pockets, arr)

return all keys in an array if arr == []
create a new array 'arr1'
loop through pockets
  for eachiteration if the elements in the values are all present in arr 
    ignore the current key/value pair
   otherwise
    arr << current key
if arr1 == [] ? return nil : return arr1

=end

# Code With Intent

def find_suspects(pockets, arr)
  if arr == [] && pockets.empty? 
    return nil
  end
  arr1 = []
  pockets.each do |name, items|
      if items == nil or items == []
        next
      end
    arr1 << name unless items.all? do |item|
      arr.include?(item) 
    end
  end
  arr1.empty? ? nil : arr1
end

pockets = { 
  bob: [1],
  tom: [2, 5],
  jane: [7]
} 

pockets1 = { julia: nil, meg: [] } 

p find_suspects(pockets, [1, 2]) == [:tom, :jane]
p find_suspects(pockets, [1, 7, 5, 2]) == nil
p find_suspects(pockets, []) == [:bob, :tom, :jane]
p find_suspects(pockets, [7]) == [:bob, :tom]
p find_suspects(pockets1, [1, 2]) == nil
```

###### **Example35: Mexican Wave**

```ruby
def wave(str)
  s = []
  arr = str.chars
  counter = 0
  loop do 
    string = ""
    break if counter > arr.length - 1
    arr.each_with_index do |letter, idx|
        idx == counter ? string << arr[idx].capitalize : string << arr[idx] 
    end
    s << string
    counter += 1
  end
  s.select.with_index { |ele, i| arr[i] != " " }
end

### Option 2 (note the exclution range)
def wave(str)
  (0...str.size).map { |i| str[0...i] + str[i].upcase + str[i + 1 .. -1] }.reject { |e| e == e.downcase }
end

p wave("hello") == ["Hello", "hEllo", "heLlo", "helLo", "hellO"]
p wave("codewars") == ["Codewars", "cOdewars", "coDewars", "codEwars", "codeWars", "codewArs", "codewaRs", "codewarS"]
p wave("") == []
p wave("two words") == ["Two words", "tWo words", "twO words", "two Words", "two wOrds", "two woRds", "two worDs", "two wordS"]
p wave(" gap ") == [" Gap ", " gAp ", " gaP "]
```

###### **Example 36: Delete a digit**

```ruby
=begin
Given an integer n, find the maximal number you can obtain by deleting exactly one digit of the given number.

Example
For n = 152, the output should be 52;

For n = 1001, the output should be 101.

Input/Output
[input] integer n

Constraints: 10 ≤ n ≤ 1000000.

[output] an integer
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given an integer n, find the maximal number you can obtain by deleting exactly one digit of the given number.

Input:

Output:

=====> Rules
Explicit Requiremnts:
  - numbers from 10 ≤ n ≤ 1000000.
  - input and output should be integer
Implicit Requiremnts:
  - min no 10,  min 2 digits
  - no other datatypes
  - do not mutate the original data
  - the sequence has to be preserved ??

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
Example
For n = 152, the output should be 52;

For n = 1001, the output should be 101.
0, 0, 1
1, 0, 1
1, 0, 1
1, 0, 0

=====> Data structure(s):
Input: integer
Intermediate: array
Output: integer

=====> High Level Algorithm:
delete the digit from the number which will make it the highest possible number

=====> Optional Implementation (Pseudo-code):
    split the num into an array having the digits `digits`*
    transform all the digits to a string*
    
    for every element in (0...digits.length)
      return a transformed array with each elements in digits transformed by excluding the element at index i
      join 
      to_i
    return the max number from the transformed array 
=end

# Code With Intent
### Option 1
def delete_digit(num)
  digits = num.to_s.chars
  (0...digits.length).map { |i| (digits[0...i] + digits[i + 1..-1]).join.to_i }.max
end

### Option 2
def delete_digit(num)
  (s=num.to_s.chars).combination(s.length - 1).to_a.map(&:join).max.to_i
end

### Option 3
def delete_digit(num)
  (0...num.to_s.size).map do |i|
    digits = num.to_s.chars
    digits.delete_at(i)
    digits.join.to_i
  end.max
end

### Option 4
def delete_digit(num)
  arr = []
  for i in 0...num.to_s.length
    digits = num.to_s.chars
    digits.delete_at(i)
    arr << digits.join.to_i
  end
  arr.max
end

### Option 5
def delete_digit(num)
  arr = [num.to_s.chars] * num.to_s.length
  max_arr = []
  arr.each.with_index do |digits, outer_i|
  new_arr = []
    digits.each_with_index do |digit, inner_i| 
      new_arr << digit unless inner_i == outer_i
    end
  max_arr << new_arr
  end
  max_arr.max.join.to_i
end

### Option 6
def delete_digit(num)
  arr = [num.to_s] * num.to_s.length
  max_arr = []
  arr.each.with_index do |ele, i|
    digits = ele.chars
    digits[i] = ""
    max_arr << digits.join.to_i
  end
  max_arr.max
end

### Option 7
def delete_digit(num)
  arr = [num.to_s] * num.to_s.length
  arr.each_with_object([]).with_index do |(ele ,arr), i|
    digits = ele.chars
    digits[i] = ""
    arr << digits.join.to_i
  end.max
end

p delete_digit(152) #== 52
p delete_digit(1001) #== 101
p delete_digit(10) #== 1
```

###### **Example 37: Multiples of 3 or 5**

```ruby

=begin
#========== THE PEDAC PROCESS ==========

=====> Problem:

If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in.

Note: If the number is a multiple of both 3 and 5, only count it once.

Input: Integer

Output: Integer

=====> Rules
Explicit Requiremnts:
  - choose multiples of 3 adn 5
  - if multiples of 3 and 5 then choose it only once
Implicit Requiremnts:
  - range excludes the number
  - no other datatypes
  - positive numbers only ie > 0

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p solution(10) #== 23
3, 5, 6 and 9.

p solution(16) #== 50
3, 5, 6 and 9. 12 15 #== 50
p solution(20) #== 78
p solution(200) #== 9168

=====> Data structure(s):
Input: Integer
Intermediate: Array
Output: Integer

=====> High Level Algorithm:
create a range of numbers from 1 to the number before the given argument and select the numbers divisible by 3, 5 or both 3 and 5

=====> Optional Implementation (Pseudo-code):
create an array from (1...num)
select num if num % 3 == 0 || num % 5 == 0
add all the numbers and return it
=end

# Code With Intent

def solution(num)
  (1...num).select { |num| num if num % 3 == 0 || num % 5 == 0 }.sum
end

p solution(10) == 23
p solution(20) == 78
p solution(200) == 9168
```

###### **Example 38: String Transformer**

```ruby
=begin
Given a string, return a new string that has transformed based on the input:

Change case of every character, ie. lower case to upper case, upper case to lower case.
Rev
erse the order of words from the input.
Note: You will have to handle multiple spaces, and leading/trailing spaces.

For example:

"Example Input" ==> "iNPUT eXAMPLE"
You may assume the input only contain English alphabet and spaces.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given a string, return a new string that has transformed based on the input:

Change case of every character, ie. lower case to upper case, upper case to lower case.
Rev
erse the order of words from the input.
Note: You will have to handle multiple spaces, and leading/trailing spaces.

Input: string

Output:string

=====> Rules
Explicit Requiremnts:
  - swap all the cases
  -
Implicit Requiremnts:
  - only alphabets allowed
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
"Example Input" ==> "iNPUT eXAMPLE"

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
Swap all the lowercase to uppercase and vice versa. Reverse the order of the words and return the string while maintaining the spaces

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def string_transformer(str)
  str.split(/\b/).reverse.join.swapcase
end

p string_transformer("Example Input") #== "iNPUT eXAMPLE"
p string_transformer("You Know  When  THAT Hotline Bling") #== "bLING hOTLINE  that  wHEN kNOW yOU"
                                                           #== "bLING hOTLINE  that  wHEN kNOW yOU"
```

###### **Example 39: Greatest Product**

```ruby
=begin
Complete the greatestProduct method so that it'll find the greatest product of five consecutive digits in the given string of digits.

For example:

greatestProduct("123834539327238239583") // should return 3240
The input string always has more than five digits.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Complete the greatestProduct method so that it'll find the greatest product of five consecutive digits in the given string of digits.

Input: string

Output: Integer

=====> Rules
Explicit Requiremnts:
  - The input string always has more than five digits.
  - String of integers
Implicit Requiremnts:
  - no other datatypes
  - repeated strings allowed
  - when 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p greatest_product("123834539327238239583") == 3240
p greatest_product("395831238345393272382") == 3240
p greatest_product("92494737828244222221111111532909999") == 5292
p greatest_product("92494737828244222221111111532909999") == 5292
p greatest_product("02494037820244202221011110532909999") == 0
every 5th element is 0 hence the product is always 0 for continuous 

=====> Data structure(s):
Input: string
Intermediate: array 
Output: integer

=====> High Level Algorithm:
iterate and find the greatest product of 5 continuous digits.

=====> Optional Implementation (Pseudo-code):
 - split the string into induviadual string
 - create a new array
      - elements are continuious five consecutive digits
      - transform the array into an array of integers
      - transform the array into the product of the digits.
      
 - return the max value of the array

=end

# Code With Intent
def greatest_product(num_str)
  num_str.chars.each_cons(5).to_a.map { |arr| arr.map(&:to_i).reduce(:*) }.max
end

# Option 2
def greatest_product(n)
  cont_arr = []
  (0...n.length).each do |outer_idx|
    digits = n[outer_idx, 5] 
    cont_arr << digits if digits.length == 5
  end
  cont_arr.map { |digits| digits.chars.map(&:to_i).reduce(:*) }.max
end

p greatest_product("123834539327238239583") == 3240
p greatest_product("395831238345393272382") == 3240
p greatest_product("92494737828244222221111111532909999") == 5292
p greatest_product("92494737828244222221111111532909999") == 5292
p greatest_product("02494037820244202221011110532909999") == 0
```

###### **Example40: Duplicate Encoder**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
The goal of this exercise is to convert a string to a new string where each character in the new string is "(" if that character appears only once in the original string, or ")" if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

Input: string

Output: string

=====> Rules
Explicit Requiremnts:
  - case insensitive
  - input string
Implicit Requiremnts:
  - special chars allowed
  - no other dataypes allowed
  - space is considered as character too

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
Examples
"din"      =>  "(((" 
all new strings

"recede"   =>  "()()()"
e repeated

"Success"  =>  ")())())"
s and c repeated

"(( @"     =>  "))((" 
" and ( repeated. space is considered as character too

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
scan through the characters and replace the characters occuring more than once with ")" and chars occuring once with "("

=====> Optional Implementation (Pseudo-code):
 method duplicate_encode(str) -----> string
 initialize split_arr = split the str.downcase into induvidual chars 
 Iterate over split_arr and transform the elements into a new array
    - If current element `char` occurs more than once in str.downcase
      - replace `char` with "("
      - otherwise relace char with ")"
 join split_arr and return
=end

# Code With Intent
def duplicate_encode(str)
  split_arr = str.downcase.chars
  split_arr.map { |char| str.downcase.count(char) > 1 ? ")" : "(" }.join
end

p duplicate_encode("din") == "((("
p duplicate_encode("recede") == "()()()"
p duplicate_encode("Success") == ")())())"
p duplicate_encode("(( @") == "))(("
```

###### **Example41: Backspaces in string**

```ruby
=begin

========== THE PEDAC PROCESS ==========

=====> Problem:
Assume "#" is like a backspace in string. This means that string "a#bc#d" actually is "bd"

Your task is to process a string with "#" symbols.
Input:

Output:

=====> Rules
Explicit Requiremnts:
  - 
  -
Implicit Requiremnts:
  - return "" when given argumentis an empty string
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

Examples
"abc#d##c"      ==>  "ac"
c
## - deletes d and c
# - delets b
ac

"abc##d######"  ==>  ""

"#######"       ==>  ""

""              ==>  ""


=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
for every hash remove the preceding letter

=====> Optional Implementation (Pseudo-code):
method clean_string(str)

initializr string = []
split str and iterate overthe aray
  - if current element != '#'
      - string << current element
    else
      - remove the last element from the string array
      
string.join

=end

# Code With Intent

def clean_string(str)
  string = []
  str.chars.each { |digit| digit != '#' ? string << digit : string.pop }
  string.join
end

p clean_string('abc#d##c') #== "ac"
p clean_string('abc####d##c#') #== ""
```

###### **Example 42: Sorting arrays**

```ruby
=begin
Sort the given strings in alphabetical order, case insensitive. For example:

["Hello", "there", "I'm", "fine"]  -->  ["fine", "Hello", "I'm", "there"]
["C", "d", "a", "B"])              -->  ["a", "B", "C", "d"]
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Sort the given strings in alphabetical order, case insensitive. For example:

Input: array

Output: array

=====> Rules
Explicit Requiremnts:
  - all are strings
  - case insensitive
Implicit Requiremnts:
  -
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p sortme(["Hello", "there", "I'm", "fine"]) == ["fine", "Hello", "I'm", "there"]
p sortme(["C", "d", "a", "Ba", "be"]) == ["a", "Ba", "be", "C", "d"]
p sortme(["CodeWars"]) == ["CodeWars"]

=====> Data structure(s):
Input: array
Intermediate: array
Output:array

=====> High Level Algorithm:
sort the words case insensitively

=====> Optional Implementation (Pseudo-code):

sortme(arr)

- iterate through arr and sort each element with each other after calling the downcase on each element
=end

# Code With Intent

def sortme(arr)
  arr.sort_by { |word| word.downcase } 
end

p sortme(["Hello", "there", "I'm", "fine"]) == ["fine", "Hello", "I'm", "there"]
p sortme(["C", "d", "a", "Ba", "be"]) == ["a", "Ba", "be", "C", "d"]
p sortme(["CodeWars"]) == ["CodeWars"]
```

###### **Example 43: Transform to prime**

```ruby
=begin
Task :
Given a List [] of n integers , find the minimum number to be inserted in a list, so that the sum of all elements of the list should equal the closest prime number .

Notes
List size is at least 2 .

List's numbers will only have positives (n > 0) .

Repetition of numbers in the list could occur .

The newer list's sum should equal the closest prime number .

Input >> Output Examples
1- minimumNumber ({3,1,2}) ==> return (1)
Explanation:
Since , the sum of the list's elements equal to (6) , the minimum number to be inserted to transform the sum to prime number is (1) , which will make *the sum of the List** equal the closest prime number (7)* .
2-  minimumNumber ({2,12,8,4,6}) ==> return (b, 
5)
Explanation:
Since , the sum of the list's elements equal to (32) , the minimum number to be inserted to transform the sum to prime number is (5) , which will make *the sum of the List** equal the closest prime number (37)* .
3- minimumNumber ({50,39,49,6,17,28}) ==> return (2)
Explanation:
Since , the sum of the list's elements equal to (189) , the minimum number to be inserted to transform the sum to prime number is (2) , which will make *the sum of the List** equal the closest prime number (191)* .
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given a List [] of n integers , find the minimum number to be inserted in a list, so that the sum of all elements of the list should equal the closest prime number.

Input: array

Output: integer

=====> Rules
Explicit Requiremnts:
  - array as argument
  - positive integer
Implicit Requiremnts:
  - no empty array
  - no other datatype

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p minimum_number([3,1,2]) == 1
sum = 6 
6 + 1

p minimum_number([5,2]) == 0
7 + 0

p minimum_number([1,1,1]) == 0
3 + 0

p minimum_number([2,12,8,4,6]) == 5
32 + 5

p minimum_number([50,39,49,6,17,28]) == 2
189 + 2

=====> Data structure(s):
Input: array
Intermediate: 
Output: integer

=====> High Level Algorithm:
add the digits within the array and add to it a number to make it a prime number

=====> Optional Implementation (Pseudo-code):
method ---- >  minimum_number(arr) ----> integer
- Initialize sum = sum all elements in arr 
- Initialize add = 0

- is_prime?(num) SUBPROCESS
 - number is prime if the number is not divisible by any other smaller number but itself
 
- if is_prime?(sum) 
  - return 0
- else sum is not prime
loop
  break when is_prime?(sum + add)
  add += 1
end
return add

=end

# Code With Intent
def is_prime?(sum)
  (2...sum).select { |num| sum % num == 0 } == []
end

def minimum_number(arr)
  sum = arr.sum
  add = 0
  return 0 if is_prime?(sum)
  loop do
    break if is_prime?(sum + add)
    add += 1
  end
  add
end

p minimum_number([3,1,2]) #== 1
p minimum_number([5,2]) #== 0
p minimum_number([1,1,1]) #== 0
p minimum_number([2,12,8,4,6]) #== 5
p minimum_number([50,39,49,6,17,28]) #== 2
```

###### **Example44: Counting Duplicates**

```ruby
=begin

Example
"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabBcde" -> 2 # 'a' occurs twice and 'b' twice (`b` and `B`)
"indivisibility" -> 1 # 'i' occurs six times
"Indivisibilities" -> 2 # 'i' occurs seven times and 's' occurs twice
"aA11" -> 2 # 'a' and '1'
"ABBA" -> 2 # 'A' and 'B' each occur twice
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Count the number of Duplicates
Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits that occur more than once in the input string. 

Input: string

Output: integer

=====> Rules
Explicit Requiremnts:
  - The input string can be assumed to contain only alphabets (both uppercase and lowercase) and numeric digits.
  - case-insensitive
Implicit Requiremnts:
  - empty string allowed
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p duplicate_count("") == 0
none => 0

p duplicate_count("abcde") == 0
no repeat => 0

p duplicate_count("abcdeaa") == 1
a repeated 1


p duplicate_count("abcdeaB") == 2
a and b repeated

p duplicate_count("Indivisibilities") == 2
i and s repeated

=====> Data structure(s):
Input:string
Intermediate: array, hash
Output: integer

=====> High Level Algorithm:
return thte count of the number of alphabets which are repeated

=====> Optional Implementation (Pseudo-code):
duplicate_count(str)

Initialize arr = split the strring into induvidual characters after conveertung them to lower case
hsh = create_hash(arr) sub process
    group the digits by the number of times they occur 
repeat_hsh = select the alphabets that occur more than once
repeat_hsh.empty? ? 0 : repeat.keys.count
=end

# Code With Intent
def create_hash(arr)
  arr.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele] += 1 }
end

def duplicate_count(str)
  arr = str.downcase.chars
  hsh = create_hash(arr)
  repeat_hash = hsh.select { |_, v| v > 1 }
  repeat_hash.empty? ? 0 : repeat_hash.keys.count 
end  

p duplicate_count("") == 0
p duplicate_count("abcde") == 0
p duplicate_count("abcdeaa") == 1
p duplicate_count("abcdeaB") == 2
p duplicate_count("Indivisibilities") == 2
```

###### **Example45: Alphabetized**

```ruby
=begin
The alphabetized kata


The input is restricted to contain no numerals and only words containing the english alphabet letters.

Example:

alphabetized("The Holy Bible") # "BbeehHilloTy"
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Re-order the characters of a string, so that they are concatenated into a new string in "case-insensitively-alphabetical-order-of-appearance" order. Whitespace and punctuation shall simply be removed!

Input: string

Output: string

=====> Rules
Explicit Requiremnts:
  - remove white space and punctuation
  - 
Implicit Requiremnts:
  - empty string allowed
  - no other data type

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p alphabetized("") #== ""


p alphabetized(" ") #== ""

p alphabetized(" a") #== "a"

p alphabetized("a ") #== "a"

p alphabetized(" a ") #== "a"

p alphabetized("A b B a") #== "AabB"

p alphabetized(" a b c d e f g h i j k l m n o p q r s t u v w x y z A B C D E F G H I J K L M N O P Q R S T U V W X Y Z") #== "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ"


=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
scan all the chars and return a new string  ordered alphabetically while being case insensitive

=====> Optional Implementation (Pseudo-code):
mehtod alphabetized(str)

arr = Split all the chars into inviduval chars and ignore any white space and punctuation
sort the array by comparinf the downcase version of them
join the sorted array and return the string
=end

# Code With Intent

def split_char(str)
  str.scan(/[a-z]/i)
end

def alphabetized(str)
  arr = split_char(str)
  arr.sort { |a, b| a.downcase <=> b.downcase }.join
end

p alphabetized("") == ""
p alphabetized(" ") == ""
p alphabetized(" a") == "a"
p alphabetized("a ") == "a"
p alphabetized(" a ") == "a"
p alphabetized("A b B a") == "AabB"
p alphabetized(" a b c d e f g h i j k l m n o p q r s t u v w x y z A B C D E F G H I J K L M N O P Q R S T U V W X Y Z") == "aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ"
```

###### **Example46: Sum of digits**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
A digital root is the recursive sum of all the digits in a number. Given n, take the sum of the digits of n. If that value has more than one digit, continue reducing in this way until a single-digit number is produced. This is only applicable to the natural numbers.

Input: integer

Output: integer

=====> Rules
Explicit Requiremnts:
  - positive numbers
  - keep adding the digits until a single number is reached
Implicit Requiremnts:
  - no othe data types
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
digital_root(16)
=> 1 + 6
=> 7

digital_root(942)
=> 9 + 4 + 2
=> 15 ...
=> 1 + 5
=> 6

digital_root(132189)
=> 1 + 3 + 2 + 1 + 8 + 9
=> 24 ...
=> 2 + 4
=> 6

digital_root(493193)
=> 4 + 9 + 3 + 1 + 9 + 3
=> 29 ...
=> 2 + 9
=> 11 ...
=> 1 + 1
=> 2

=====> Data structure(s):
Input: integer
Intermediate: array
Output: integer

=====> High Level Algorithm:
keep adding induvidual digits untill the final number is < 10

=====> Optional Implementation (Pseudo-code):
method ---- > digital_root(num) -----> integer

 - if num < 10 retun num
 - otherwise 
    digital_root(n.digits.sum)

=end

# Code With Intent

def digital_root(n)
  n < 10 ? n : digital_root(n.digits.sum)
end

p digital_root(16) #== 7 
p digital_root(7) #== 7 
p digital_root(456) #== 6
```

###### **Example47: Array difference**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.

It should remove all values from list a, which are present in list b.
Input: arrays

Output: array

=====> Rules
Explicit Requiremnts:
  - remove all values from the first argument that is present in the second argument
  - 
Implicit Requiremnts:
  - no other datatypes
  -  positive arrays
  - empty arrays allowed

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
array_diff([1,2],[1]) == [2]
If a value is present in b, all of its occurrences must be removed from the other:

array_diff([1,2],[1]) == [2]

p array_diff([1,2], [1]) == [2]
p array_diff([1,2,2], [1]) == [2,2]
p array_diff([1,2,2], [2]) == [1]
p array_diff([1,2,2], []) == [1,2,2]
p array_diff([], [1,2]) == []

=====> Data structure(s):
Input: arrays 
Intermediate: array
Output: array

=====> High Level Algorithm:
remove the elements from the first array tht which is present in the second array

=====> Optional Implementation (Pseudo-code):
array_diff(arr1, arr2)

 return arr1 - arr2

=end

# Code With Intent

def array_diff(arr1, arr2)
  arr1 - arr2
end

p array_diff([1,2], [1]) == [2]
p array_diff([1,2,2], [1]) == [2,2]
p array_diff([1,2,2], [2]) == [1]
p array_diff([1,2,2], []) == [1,2,2]
p array_diff([], [1,2]) == []
```

###### **Example 48: Where's my parent?**

```ruby
=begin
Where's my parent?
6 kyu
Mothers arranged a dance party for the children in school. At that party, there are only mothers and their children. All are having great fun on the dance floor when suddenly all the lights went out. It's a dark night and no one can see each other. But you were flying nearby and you can see in the dark and have ability to teleport people anywhere you want.

Legend:
-Uppercase letters stands for mothers, lowercase stand for their children, i.e. "A" mother's children are "aaaa".
-Function input: String contains only letters, uppercase letters are unique.
Task:
Place all people in alphabetical order where Mothers are followed by their children, i.e. "aAbaBb" => "AaaBbb".
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Place all people in alphabetical order where Mothers are followed by their children, i.e. "aAbaBb" => "AaaBbb".

Input: string

Output: string

=====> Rules
Explicit Requiremnts:
  - String contains only letters, uppercase letters are unique
  - 
Implicit Requiremnts:
  - empty string allowed
  - no other data type allowed

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p find_children("abBA") == "AaBb"

p find_children("AaaaaZazzz") == "AaaaaaZzzz"

p find_children("CbcBcbaA") == "AaBbbCcc"

p find_children("xXfuUuuF") == "FfUuuuXx"

p find_children("") == ""


=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
Place all the alphabets in alphabetical order starting with the capital letters

=====> Optional Implementation (Pseudo-code):
find_children(str)

split the string into an array having elements of induvidual chars
sort the split string array
sort the array again by comparing the current and the next element after downcasing them
join the array and return the value

=end

# Code With Intent

def  find_children(str)
  str.chars.sort.sort { |a, b| a.downcase <=> b.downcase }.join
end

p find_children("abBA") == "AaBb"
p find_children("AaaaaZazzz") == "AaaaaaZzzz"
p find_children("CbcBcbaA") == "AaBbbCcc"
p find_children("xXfuUuuF") == "FfUuuuXx"
p find_children("") == ""
```

###### **Example49: Playing with digits**

```ruby
=begin
Some numbers have funny properties. For example:

89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n.
In other words:

Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

If it is the case we will return k, if not return -1.

Note: n and p will always be given as strictly positive integers.

dig_pow(89, 1) should return 1 since 8¹ + 9² = 89 = 89 * 1
dig_pow(92, 1) should return -1 since there is no k such as 9¹ + 2² equals 92 * k
dig_pow(695, 2) should return 2 since 6² + 9³ + 5⁴= 1390 = 695 * 2
dig_pow(46288, 3) should return 51 since 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: integer

Output: intger

=====> Rules
Explicit Requiremnts:
  - positve integers
  - > 0
Implicit Requiremnts:
  - no otther data types
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p dig_pow(89, 1) == 1
8 ** 1 + 9 ** 2 = 89 ===> 89 / 89

p dig_pow(92, 1) == -1
9 ** 1 + 2 ** 2 = 13---------- 13/92 =====> -1

p dig_pow(46288, 3) == 51
p dig_pow(695, 2) == 2

=====> Data structure(s):
Input: integer
Intermediate: array
Output: integer

=====> High Level Algorithm:
to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n otherwise it is -1

=====> Optional Implementation (Pseudo-code):
mehtod  ------ dig_pow(num, pow) - integer

initialize split_num = array of digits
SUBPROCESS positive_number(split_num, pow)
  - transform split_num into a new array with element ** p(+ index position)
  - sum the array
  - if sum / num > 0 then k = sum / num 
  - otherwise -1
=end

# Code With Intent

def positive_number(split_num, pow)
  arr = []
  split_num.each_with_index { |n, i| arr << n ** (i + pow) }
  arr.sum
end

def dig_pow(num, pow)
  split_num = num.digits.reverse
  k = positive_number(split_num, pow)
  k % num == 0 ? k / num : -1
end

p dig_pow(89, 1) #== 1
p dig_pow(92, 1) #== -1
p dig_pow(46288, 3) #== 51
p dig_pow(695, 2) #== 2
```

###### **Example50: Equal sides of an array**

```ruby
=begin
Problem given an array of ints find the index where the ints to the left summed and the ints to the right summed are equal.
  -If not possible return -1
  -Starting with first index left of it is empty so it is equal to 0
  -return the first one of these from the left
  
examples
find_even_index([20,10,-80,10,10,15,35]),0
[1,2,3,4,3,2,1]),3
[-1,-2,-3,-4,-3,-2,-1]),3

Data: Integers and arrays

Algo
  initilize a leftsum variable set to 0
  initilize a rightsum variable set to 0
  compare the everything past the 0 index to be equal to 0
  iterate through the array
    compare the things to the left of the index to the sum of the right of the index
  return -1 if nothing found
=end


def find_even_index(arr)
  return 0 if arr[1..-1].sum == 0
  return arr.length-1 if arr[0..-2].sum == 0
  (1..arr.length-1).each do |index|
    return index if arr[0...index].sum == arr[index+1..-1].sum
  end
  -1
end

p find_even_index([1,2,3,4,3,2,1]) #== 3
p find_even_index([1,100,50,-51,1,1]) #== 1
p find_even_index([1,2,3,4,5,6]) #== -1
p find_even_index([20,10,30,10,10,15,35]) #== 3
p find_even_index([20,10,-80,10,10,15,35]) #== 0
p find_even_index([10,-80,10,10,15,35,20]) #== 6
p find_even_index(Array(1..100)) #== -1
p find_even_index([0,0,0,0,0]) #== 0
p find_even_index([-1,-2,-3,-4,-3,-2,-1]) #== 3
p find_even_index(Array(-100..-1)) #== -1
```

###### **Example 51: Reverse or Rotate**

```ruby
=begin
Reverse or rotate?
If
sz is <= 0 or if str is empty return ""
sz is greater (>) than the length of str it is impossible to take a chunk of size sz hence return "".
Examples:
revrot("123456987654", 6) --> "234561876549"
revrot("123456987653", 6) --> "234561356789"
revrot("66443875", 4) --> "44668753"
revrot("66443875", 8) --> "64438756"
revrot("664438769", 8) --> "67834466"
revrot("123456779", 8) --> "23456771"
revrot("", 8) --> ""
revrot("123456779", 0) --> "" 
revrot("563000655734469485", 4) --> "0365065073456944"
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
The input is a string str of digits. Cut the string into chunks (a chunk here is a substring of the initial string) of size sz (ignore the last chunk if its size is less than sz).

If a chunk represents an integer such as the sum of the cubes of its digits is divisible by 2, reverse that chunk; otherwise rotate it to the left by one position. Put together these modified chunks and return the result as a string.

Input:string, integer

Output: string

=====> Rules
Explicit Requiremnts:
  - sz is <= 0 or if str is empty return ""
  - return "" if sz > length of the string
Implicit Requiremnts:
  -
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p revrot("1234", 0) == ""

p revrot("", 0) == ""

p revrot("1234", 5) == ""

p revrot("733049910872815764", 5) == "330479108928157"
73304 - 33047 rotate
99108 - 91089 rotate
72815 - 28157 rotate
764********ignore < sz

p revrot("123456987654", 6) == "234561876549"

p revrot("123456987653", 6) == "234561356789"
p revrot("66443875", 4) == "44668753"
4466 - 6644(reversed) result = "6644".chars.map { |a| a.to_i ** 3}.sum.even?
8753 - 3875

p revrot("66443875", 8) == "64438756"
p revrot("664438769", 8) == "67834466"
p revrot("123456779", 8) == "23456771"
p revrot("", 8) == "" 
sz > str.length 

p revrot("123456779", 0) == ""
p revrot("563000655734469485", 4) == "0365065073456944"

=====> Data structure(s):
Input: stirng
Intermediate: array
Output: string

=====> High Level Algorithm:
split the string(first Argument) into chunks of size (second argument). If the sum of the cube of induvidual digits is divisible by 2 then reverse that chunk else rotate the first item to the last

=====> Optional Implementation (Pseudo-code):
takes arguments (str, num)
return "" if num <= 0 or num > str.length*
chunks = split the str into chunk with size == num*
    ignore chunks < num in length
rotate_reverse(chunks) = Subprocess
  iterate through the chunks and transform them based on
    - if (chunk.to_i ** 3).sum is an even number then reverse it
    - else rotate it
    convrt all the chunks to strings 
  Join the transformed array and return it

=end

# Code With Intent

def chunk_str(str, num)
  str.chars.each_slice(num).to_a.select { |string| string.length == num }
end

def rotate_reverse(chunks)
  chunks.map do |chunk|
    chunk.map { |int| int.to_i ** 3 }.sum.even? ? chunk.reverse : chunk.rotate
  end
end

def revrot(str, num)
  return "" if num <= 0 || num > str.length
  chunks = chunk_str(str, num)
  rotate_reverse(chunks).flatten.join
end

p revrot("1234", 0) == ""
p revrot("", 0) == ""
p revrot("1234", 5) == ""
p revrot("733049910872815764", 5) == "330479108928157"
p revrot("123456987654", 6) == "234561876549"
p revrot("123456987653", 6) == "234561356789"
p revrot("66443875", 4) == "44668753"
p revrot("66443875", 8) == "64438756"
p revrot("664438769", 8) == "67834466"
p revrot("123456779", 8) == "23456771"
p revrot("", 8) == ""
p revrot("123456779", 0) == ""
p revrot("563000655734469485", 4) == "0365065073456944"
```

###### **Example52: Decipher This!**

```ruby
=begin
You are given a secret message you need to decipher. Here are the things you need to know to decipher it:

For each word:

the second and the last letter is switched (e.g. Hello becomes Holle)
the first letter is replaced by its character code (e.g. H becomes 72)
Note: there are no special charact,eers used, only letters and spaces

Examples

decipherThis('72olle 103doo 100ya'); // 'Hello good day'
decipherThis('82yade 115te 103o'); // 'Ready set go'
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input:

Output:

=====> Rules
Explicit Requiremnts:
  - there are no special charact,eers used
    , only letters and spaces
  - second and the last leters are switched
  - the first letter is replaced by its character code
Implicit Requiremnts:
  - no other datatype
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
decipherThis('72olle 103doo 100ya'); // 'Hello good day'
72olle = Hello
[72.ord][olle].rotate
"72olle".split(/(?=[a-z])/) = [72 olle]

decipherThis('82yade 115te 103o'); // 'Ready set go'

=====> Data structure(s):
Input: string
Intermediate: array, hash
Output: string

=====> High Level Algorithm:
Convert each word by changing the first letter to its character equivalent and exchanging the first and the last letter of the rest of the word

=====> Optional Implementation (Pseudo-code):
decipher_this(str)

    - words = splt the strings into array of induvidual words
    - correct_word(words)
      - transform each word
        - reassign word to split the words based on numbers and characters
        - replace the first element to the appropriate alphabet
        - swap the second and the last elements
        - join the word
    - join all the words usint " " and return the string
        
=end

# Code With Intent

def correct_word(words)
  words.map.with_index do |word, i|
    word = word.split(/(?=[^\d])/)
    word[0] = word[0].to_i.chr
    word[1], word[-1] = word[-1], word[1] if word.length > 2
    word.join
  end
end

def decipher_this(str)
  words = str.split
  correct_word(words).join(" ")
end

### Option 2
def correct_word(words)
  words.map.with_index do |word, i|
   num, str = word.scan(/\d+|\w+/)
    str[0], str[-1] = str[-1], str[0] if str && str.length > 1
    [num.to_i.chr, str].join
  end
end

def decipher_this(str)
  words = str.split
  correct_word(words).join(" ")
end

p decipher_this("65 119esi 111dl 111lw 108dvei 105n 97n 111ka") == "A wise old owl lived in an oak"
p decipher_this("84eh 109ero 104e 115wa 116eh 108sse 104e 115eokp") == "The more he saw the less he spoke"
p decipher_this("84eh 108sse 104e 115eokp 116eh 109ero 104e 104dare") == "The less he spoke the more he heard"
p decipher_this("87yh 99na 119e 110to 97ll 98e 108eki 116tah 119esi 111dl 98dri") == "Why can we not all be like that wise old bird"
p decipher_this("84kanh 121uo 80roti 102ro 97ll 121ruo 104ple") == "Thank you Piotr for all your help"
p decipher_this("86SE 100ZfZfj 88HdAuyNrsR") == "VES djfZfZ XRdAuyNrsH"
```

###### **Example53********

```ruby
```

###### Example54: Weird string case

```ruby
=begin
Write a function toWeirdCase (weirdcase in Ruby) that accepts a string, and returns the same string with all even indexed characters in each word upper cased, and all odd indexed characters in each word lower cased. The indexing just explained is zero based, so the zero-ith index is even, therefore that character should be upper cased.

The passed in string will only consist of alphabetical characters and spaces(' '). Spaces will only be present if there are multiple words. Words will be separated by a single space(' ').
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: strind

Output: string

=====> Rules
Explicit Requiremnts:
  - all even index upcased
  - only alphabets allowed
Implicit Requiremnts:
  - include space
  -  0 is even

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p weirdcase( "String" ) == "StRiNg"
"S t R i N g"
"0 1 2 3 4 5"

p weirdcase( "Weird string case" ) == "WeIrD StRiNg CaSe"

=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
Scan through the characters and upcase all the even indexed characters

=====> Optional Implementation (Pseudo-code):

weirdcase(str)

arr = split the string based on the space
Loop through arr and for each element
  - split the word into characters array
  - capitalise all the even indexed characters.
  - join all the chars
join arr with a space and return the string


=end

# Code With Intent

def weirdcase(str)
  arr = str.split
  arr.map do |word|
    word.chars.map.with_index { |char, idx| idx.even? ? char.upcase : char }.join 
  end.join(" ")
end

### option 2
def weirdcase string
  string.gsub(/(\w{1,2})/) { |s| $1.capitalize }
end

p weirdcase( "String" ) == "StRiNg"
p weirdcase( "Weird string case" ) == "WeIrD StRiNg CaSe"
```

###### **Example55; Are they the same?**

```ruby
=begin
Given two arrays a and b write a function comp(a, b) that checks whether the two arrays have the "same" elements, with the same multiplicities. "Same" means, here, that the elements in b are the elements in a squared, regardless of the order.

Examples
Valid arrays
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [121, 14641, 20736, 361, 25921, 361, 20736, 361]
comp(a, b) returns true because in b 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write b's elements in terms of squares:

a = [121, 144, 19, 161, 19, 144, 19, 11] 
b = [11*11, 121*121, 144*144, 19*19, 161*161, 19*19, 144*144, 19*19]
Invalid arrays
If we change the first number to something else, comp may not return true anymore:

a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [132, 14641, 20736, 361, 25921, 361, 20736, 361]
comp(a,b) returns false because in b 132 is not the square of any number of a.

a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [121, 14641, 20736, 36100, 25921, 361, 20736, 361]
comp(a,b) returns false because in b 36100 is not the square of any number of a.

Remarks
a or b might be [] (all languages except R, Shell).
a or b might be nil or null or None or nothing (except in Haskell, Elixir, C++, Rust, R, Shell, PureScript).
If a or b are nil (or null or None), the problem doesn't make sense so return false.

Note for C
The two arrays have the same size (> 0) given as parameter in function comp.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: given two arrays

Output: boolean

=====> Rules
Explicit Requiremnts:
  - both the arrays have the same multiplicities
    - ie all the elements in the second array are the squaare of the first one (regardless of the order)
  - 
Implicit Requiremnts:
  - no other data types
  - can be an empty array

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p comp([121, 144, 19, 161, 19, 144, 19, 11], [121, 14641, 20736, 361, 25921, 361, 20736, 361]) == true
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [121, 14641, 20736, 361, 25921, 361, 20736, 361]
comp(a, b) returns true because in b 121 is the square of 11, 14641 is the square of 121, 20736 the square of 144, 361 the square of 19, 25921 the square of 161, and so on. It gets obvious if we write b's elements in terms of squares:

p comp([121, 144, 19, 161, 19, 144, 19, 11] , [132, 14641, 20736, 361, 25921, 361, 20736, 361]) == false
a = [121, 144, 19, 161, 19, 144, 19, 11]  
b = [132, 14641, 20736, 361, 25921, 361, 20736, 361]
comp(a,b) returns false because in b 132 is not the square of any number of a.
p comp(nil, [1, 2, 3]) == false 
nil ----> false

p comp([1, 2], []) == false
empty array ----> false

p comp([1, 2], [1, 4, 4]) == false
have different lengths ----> false

=====> Data structure(s):
Input: arrays
Intermediate: array
Output: array

=====> High Level Algorithm:
Compare the two arrays and check if the two arrays are equal in length and if the second array has elements which are the square of the elements in the first argument array. If yes return true Else return false

=====> Optional Implementation (Pseudo-code):
comp(arr1, arr2)

return false if [arr1, arr2].include?(nil) || arr1.length != arr2.length

SUBPROCESS 
  create_squares(arr1)
    - Iterate through the array arr1 and transforrm all the elements within the array to a new array
      - square each element
      - sort the return array

sort create_square(arr1)
sort arr2

compare if create_squares(arr1) and arr2 are equal?
  if yes then return true
  else return false

=end

# Code With Intent
def create_squares(arr1)
  arr1.map { |num| num ** 2 }
end

def comp(arr1, arr2)
  return false if [arr1, arr2].include?(nil) || arr1.length != arr2.length
  create_squares(arr1).sort == arr2.sort
end

p comp([121, 144, 19, 161, 19, 144, 19, 11], [121, 14641, 20736, 361, 25921, 361, 20736, 361]) == true
p comp([121, 144, 19, 161, 19, 144, 19, 11] , [132, 14641, 20736, 361, 25921, 361, 20736, 361]) == false
p comp(nil, [1, 2, 3]) == false
p comp([1, 2], []) == false
p comp([1, 2], [1, 4, 4]) == false
```

###### **Example56: Grouping and changing**

```ruby
=begin
Your goal is to write the group_and_count method, which should receive and array as unique parameter and return a hash. Empty or nil input must return nil instead of a hash. This hash returned must contain as keys the unique values of the array, and as values the counting of each value.

Example usage:

input = [1,1,2,2,2,3]

group_and_count(input)# == {1=>2, 2=>3, 3=>1}
The following methods were disabled:

Array#count
Array#length
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: given an array of integers

Output: hash 

=====> Rules
Explicit Requiremnts:
  - nil and [] should return nil
  -keys are unique numbers
  - values are their count
Implicit Requiremnts:
  - no other datatypes
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
input = [1,1,2,2,2,3]
1 => 1
2 => 3
3 => 1

group_and_count(input)# == {1=>2, 2=>3, 3=>1}

=====> Data structure(s):
Input: array
Intermediate: array
Output:hash

=====> High Level Algorithm:
iterate through the array and return a hash with keys as the unique elements of the arrays and the valuesa as its count.

=====> Optional Implementation (Pseudo-code):
group_and_count(arr) ---- > hash

return nil if arr == nil or arr == []
creating hash
  create a new Hash object hsh with a default value of 0
  iterate through the array arr and increment hsh[current number] by one everytime you come across them
  return hsh

=end

# Code With Intent
def group_and_count(arr)
  return nil if arr == nil or arr == []
  arr.each_with_object(Hash.new(0)) { |num, hsh| hsh[num] += 1 }
end

input = [1,1,2,2,2,3]
p group_and_count(input) == {1=>2, 2=>3, 3=>1}
```

###### Example57: Nexus

```ruby
=begin
Not to brag, but I recently became the nexus of the Codewars universe! My honor and my rank were the same number. I cried a little.

Complete the method that takes a hash/object/directory/association list of users, and find the nexus: the user whose rank is the closest is equal to his honor. Return the rank of this user. For each user, the key is the rank and the value is the honor.

If nobody has an exact rank/honor match, return the rank of the user who comes closest. If there are several users who come closest, return the one with the lowest rank (numeric value). The hash will not necessarily contain consecutive rank numbers; return the best match from the ranks provided.

Example
         rank    honor
users = {  1  =>  93,
          10  =>  55,
          15  =>  30,
          20  =>  19,    <--- nexus
          23  =>  11,
          30  =>   2 }
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: hsh

Output: integer

=====> Rules
Explicit Requiremnts:
  - return the key with the closest nexus
  - for more than 1 match return the smallest num
  - if matched with the key then return the nexus
Implicit Requiremnts:
  - key/value - integers
  - no other datatype
  - no empty hash

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p nexus({1 => 3, 3 => 3, 5 => 1}) == 3
3 => 3

p nexus({1 => 10, 2 => 6, 3 => 4, 5 => 1}) == 3
 3 => 4
 
p nexus({1 => 10, 2 => 3, 3 => 4, 5 => 1}) == 2
2 => 3, 3 => 4
2 is the smallest of the key

=====> Data structure(s):
Input: hash
Intermediate: hash, array
Output: integer

=====> High Level Algorithm:
given a hash of rank and honor. Select the rank that matches the honor. If no match then select the closest match. If more than one match then return the smallest rank

=====> Optional Implementation (Pseudo-code):
nexus(hsh) ---> Integer

Initialize selected = select_rank(hsh)
Select the rank select_rank(hsh) - SUBPROCESS
  - if key == value for any pair
    select the pair that has teh same key and values
  - else
    select the key/value pair(s) that whose difference is the min of the lot
    ie (value - key) is the minimum out of all
      - convert the hsh into an array
      - transform this new array into another array `difference` with elements as the difference between the second the first value
      - select the key/value pair value - key == difference.min
    
Select the keys of `selected`
  - RETURN  the min value
=end

# Code With Intent

# def select_rank(hsh)
#   return hsh.select { |key, value| key == value }if hsh.any? { |key, value| key == value } 
#   difference = hsh.to_a.map { |arr| arr.max - arr.min  }
#   hsh.select { |key, value| (value - key) == difference.min || (key - value) == difference.min }
# end

# def nexus(hsh)
#   select_rank(hsh).keys.min
# end

def nexus(users)
  users.min_by { |rank, honor| [(rank - honor).abs, rank] }[0]
end

p nexus({1 => 3, 3 => 3, 5 => 1}) == 3
p nexus({1 => 10, 2 => 6, 3 => 4, 5 => 1}) == 3
p nexus({1 => 10, 2 => 3, 3 => 4, 5 => 1}) == 2
p nexus({1=>9999, 10=>999, 100=>99, 1000=>9, 10000=>0}) == 100
```

###### Example58: Count letters in a string

```ruby
=begin
In this kata, you've to count lowercase letters in a given string and return the letter count in a hash with 'letter' as key and count as 'value'. The key must be 'symbol' instead of string in Ruby and 'char' instead of string in Crystal.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: string

Output: hash

=====> Rules
Explicit Requiremnts:
  - output is a hash
  - key => chars converted to symbols
  - value => count
Implicit Requiremnts:
  - all lowercse
  - no special characers or other data types

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p letter_count('arithmetics') ==  {:a=>1, :c=>1, :e=>1, :h=>1, :i=>2, :m=>1, :r=>1, :s=>1, :t=>2}


=====> Data structure(s):
Input: string
Intermediate: array, hash
Output:hash

=====> High Level Algorithm:
Scan throuh the string ans split them into induvidual chars. transform them into symbols. REturn a hash whose keys are the symbols and the values are the count of the symbols

=====> Optional Implementation (Pseudo-code):
letter_count(str)

Initialize arr = split the string into an array of induvudual chars
Initialize new_arr = transform arr into a new array with elements converted into a symbol representation of the chars

create_hash(new_arr) - SUBPROCESS
 - create a HAsh object hsh with a defalut value of 0
 - iterate over new_arr
    - for each element 
      hsh[element] += 1
  - return the hsh
=end

# Code With Intent

def create_hash(new_arr)
  new_arr.each_with_object(Hash.new(0)) { |ele, hsh| hsh[ele] += 1 }
end

def letter_count(str)
  arr = str.chars
  new_arr = arr.map(&:to_sym)
  create_hash(new_arr)
end

p letter_count('arithmetics') ==  {:a=>1, :c=>1, :e=>1, :h=>1, :i=>2, :m=>1, :r=>1, :s=>1, :t=>2}\
```

###### **Example59: Triple Trouble**

```ruby
=begin
Write a function

triple_double(num1, num2)
which takes numbers num1 and num2 and returns 1 if there is a straight triple of a number at any place in num1 and also a straight double of the same number in num2.

If this isn't the case, return 0


=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Input: Integer

Output: Integer

=====> Rules
Explicit Requiremnts:
  - integers
  - 0 if none found, 1 if combination found
Implicit Requiremnts:
  - no empty arguments
  - triple in the first argument, double in the second argument

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

Examples
triple_double(451999277, 41177722899) == 1
# num1 has straight triple 999s and  num2 has straight double 99s

triple_double(1222345, 12345) == 0
# num1 has straight triple 2s but num2 has only a single 2

=====> Data structure(s):
Input: Integers
Intermediate: array
Output: integer

=====> High Level Algorithm:
check if the first argument has the same digit in a sequence of 3
check if the second argument has the same digit in a sequence of 2
if true return 1
if false return 2

=====> Optional Implementation (Pseudo-code):
triple_double(num1, num2)

chunk_arr(num) - SUBPROCESS 
  split num into an array of digits
  split array grouped by the type of digits
  
  
triple = chunk_arr(num1)
  select triple has any sub array whose length > 2  
  
double = chunk_arr(num2)
  select double has any? sub array whose length > 1
  return 0 if triple or double is an empty array
  return 1 if triple.first.length == 3 && double.first.length == 2
  else return 0
  
=end

# Code With Intent

# def triple_double(num1, num2)
#   num1.to_s.scan(/(.)\1\1/).any? { |n| /#{n}{2}/ === num2.to_s } ? 1 : 0
# end

def triple_double(num1, num2)
  num1.to_s.scan(/(.)\1\1/).any? { |n| num2.to_s.scan(/#{n}{2}/) != [] } ? 1 : 0
end

### Option2
def triple_double(num1, num2)
  triples = num1.digits.reverse.each_cons(3).to_a.select do |nums|
    nums.all? { |num| nums[0] == num }
  end.map(&:join)
  
  triples.any? { |trip| num2.to_s.include?(trip.slice(0, 2)) } ? 1 : 0
end

p triple_double(12345, 12345) #== 0
p triple_double(666789, 12345667) #== 1
p triple_double(1112, 122) #== 0
p triple_double(1222345, 12345) #== 0
```

###### **Example60: Which are in**

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given two arrays of strings a1 and a2 return a sorted array r in lexicographical order of the strings of a1 which are substrings of strings of a2.

Input: arrays

Output: arrays

=====> Rules
Explicit Requiremnts:
  - returns a sorted array with elements from a1 which are substtrings in a2
  - no duplicates
  - dont mutate inputs
  - return [] when there is no match
Implicit Requiremnts:
  -
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

#Example 1: a1 = ["arp", "live", "strong"]
a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
returns ["arp", "live", "strong"]

#Example 2: a1 = ["tarp", "mice", "bull"]
a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
returns []

p substrings(["arp", "live", "strong"], ["lively", "alive", "harp", "sharp", "armstrong"]) == ["arp", "live", "strong"]

p substrings(["tarp", "mice", "bull"], ["lively", "alive", "harp", "sharp", "armstrong"]) == []

p substrings(["delta", "gamma", "alpha", "beta"], ["alphabetical", "beta-carotene", "gamma rays", "deltoid"]) == ["alpha", "beta", "gamma"]

p substrings(["albe", "negam"], ["alphabetical", "beta-carotene", "gamma rays", "deltoid"]) == []

=====> Data structure(s):
Input: arrays
Intermediate: array
Output: array

=====> High Level Algorithm:
compare the arrays and select the elements from the first array which are the substrings of any of the second argumnet array

=====> Optional Implementation (Pseudo-code):
def substrings(arr1, arr2)

select the elements in arr1 that is a substring of one or more of the elements in arr2
  - Iterate over arr1
   - check if each element is a substring of any of arr2
   - select them
   sort the selected array and return it

=end

# Code With Intent

def substrings(arr1, arr2)
  arr1.select { |sub| arr2.any? { |string| string.scan(/#{sub}/) != [] } }.sort
end

### Option 2 
def substrings(arr1, arr2)
  arr1.select { |sub| arr2.any? { |string| string.include?(sub) } }.sort
end

p substrings(["arp", "live", "strong"], ["lively", "alive", "harp", "sharp", "armstrong"]) == ["arp", "live", "strong"]
p substrings(["tarp", "mice", "bull"], ["lively", "alive", "harp", "sharp", "armstrong"]) == []
p substrings(["delta", "gamma", "alpha", "beta"], ["alphabetical", "beta-carotene", "gamma rays", "deltoid"]) == ["alpha", "beta", "gamma"]
p substrings(["albe", "negam"], ["alphabetical", "beta-carotene", "gamma rays", "deltoid"]) == []
```

###### Example61: Format a string of names like 'Bart, Lisa & Maggie'

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given: an array containing hashes of names

Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

Input: Hashes

Output:

=====> Rules
Explicit Requiremnts:
  - all the hashes are pre-validated and will only contain A-Z, a-z, '-' and '.'.
  - 
Implicit Requiremnts:
  -
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

Example:

list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ])
# returns 'Bart, Lisa & Maggie'
more than 2 elements

list([ {name: 'Bart'}, {name: 'Lisa'} ])
# returns 'Bart & Lisa'
two hash element within the array hence join using  "&"

list([ {name: 'Bart'} ])
# returns 'Bart'
one element

list([])
# returns ''
empty 

=====> Data structure(s):
Input: Hash, array
Intermediate: array, hash
Output: string

=====> High Level Algorithm:
return a string joined using commas except the last two elements

=====> Optional Implementation (Pseudo-code):
list(arr) ===> string

initialize values = []
return "" if arr is empty

iterate over arr
  - the current element is a hash hsh
    - iterate over the hash and for every iteration pass the value to array values

if length of values < 3
  return values.join(" & ")
if length of values > 3
  return values[0..-2].join(", ") + " & " + hsh.values[-1]
  
=end

# Code With Intent

def list(arr)
  values = []
  return "" if arr.empty?
  arr.each { |hsh| hsh.each {|_, v| values << v}  }
  values.length < 3 ? values.join(" & ") : values[0..-2].join(", ") + " & " + values[-1]
end

p list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ]) #== 'Bart, Lisa & Maggie'
p list([ {name: 'Bart'}, {name: 'Lisa'} ]) #== 'Bart & Lisa'
p list([ {name: 'Bart'} ]) #== 'Bart'
p list([]) #== ''
```

###### Example62: Find the missing letter

```ruby
#Find the missing letter

# Write a method that takes an array of consecutive (increasing) letters as input and that returns the missing letter in the array.

# You will always get an valid array. And it will be always exactly one letter be missing. The length of the array will always be at least 2.
# The array will always contain letters in only one case.

# Example:

# ['a','b','c','d','f'] -> 'e' 
# ['O','Q','R','S'] -> 'P'


# (Use the English alphabet with 26 letters!)

# Have fun coding it and please don't forget to vote and rank this kata! :-)
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
find the missin letter in sequence

Input: array 

Output: string

=====> Rules
Explicit Requiremnts:
  - always leter missing 
  - min length 2
  - same case
  - 
Implicit Requiremnts:
  - always in the middle
  - not first or the last element missing

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
# ["a","b","c","d","f"] -> "e"
# ["O","Q","R","S"] -> "P"

=====> Data structure(s):
Input:array
Intermediate: array
Output: string

=====> High Level Algorithm:
create an array with elements ranging from the first and the last elements of the array. compare this array and the original array and find the missing element. Return it as a string

=====> Optional Implementation (Pseudo-code):
find_missing_letter(arr)

initialize new_arr = arrays ranging from arr[0]..arr[-1]
return the first element in new_arr - arr


=end

# Code With Intent

def find_missing_letter(arr)
  new_arr = (arr[0]..arr[-1]).to_a
  (new_arr - arr).first
end

p find_missing_letter(['a','b','c','d','f']) == 'e' 
p find_missing_letter(['O','Q','R','S']) == 'P' 
```

###### Example63: Who likes it?

```ruby
=begin
You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement a function likes :: [String] -> String, which must take in input array, containing the names of people who like an item. It must return the display text as shown in the examples:

likes [] // must be "no one likes this"
likes ["Peter"] // must be "Peter likes this"
likes ["Jacob", "Alex"] // must be "Jacob and Alex like this"
likes ["Max", "John", "Mark"] // must be "Max, John and Mark like this"
likes ["Alex", "Jacob", "Mark", "Max"] // must be "Alex, Jacob and 2 others like this"
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:

Implement a function likes :: [String] -> String, which must take in input array, containing the names of people who like an item. It must return the display text

Input: array of names

Output: string

=====> Rules
Explicit Requiremnts:
  - empty array allowed
    eg None like this
  - 1 name eg. name1 likes this
  - 2 names seperated by and eg. name1 and name
  - 3 names and a comma eg name1, name2 and name3 likes this
  - 3 + names name1, name2 and count.othenames like this
  - 
Implicit Requiremnts:
  - no special characters or other datatypes
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p likes([]) =="no one likes this"

p likes(["Peter"]) == "Peter likes this"
p likes(["Jacob", "Alex"]) == "Jacob and Alex like this"
p likes(["Max", "John", "Mark"]) == "Max, John and Mark like this"
p likes(["Alex", "Jacob", "Mark", "Max"]) == "Alex, Jacob and 2 others like this"

=====> Data structure(s):
Input: array
Intermediate: array
Output: string

=====> High Level Algorithm:
iterate over the array
  if empty array then return No one likes this
  if array with 1 element then return "name1 likes this"
  if array with 2 element then return "name1 and name 2 likes this"
  if arary with 3 element then return "name1, name2 and name 3 likes this"
  if arary with 4 element then return "name1, name2 and 2 other likes this"

=====> Optional Implementation (Pseudo-code):
likes(names) ----> string

Initialize count = size of names 
if count == 0 
  return "no one likes this"
if count == 1
  return "name1 likes this"
if count == 2
  return "name1 and likes this"
if count == 3
  return "name1, name2 and name3 likes this"
if count == 3+
  return "name1, name2 and count - 2` likes this"
=end

# Code With Intent

def likes(names)
  count = names.length
  
  case count
    when 0 then "no one likes this"
    when 1 then "#{names[0]} likes this"
    when 2 then "#{names[0]} and #{names[1]} like this"
    when 3 then "#{names[0]}, #{names[1]} and #{names[2]} like this"
    else "#{names[0]}, #{names[1]} and #{count - 2} others like this"
  end
end

p likes([]) == "no one likes this"
p likes(["Peter"]) == "Peter likes this"
p likes(["Jacob", "Alex"]) == "Jacob and Alex like this"
p likes(["Max", "John", "Mark"]) == "Max, John and Mark like this"
p likes(["Alex", "Jacob", "Mark", "Max"]) == "Alex, Jacob and 2 others like this"
```

###### Example64: Find the odd one

```ruby
=begin
#========== THE PEDAC PROCESS ==========

=====> Problem:

You are given an array (which will have a length of at least 3, but could be very large) containing integers. The array is either entirely comprised of odd integers or entirely comprised of even integers except for a single integer N. Write a method that takes the array as an argument and returns this "outlier" N.

Input:

Output:

=====> Rules
Explicit Requiremnts:
  - min 3 elements
  - integers
  - wholly odd or even except one
  - return the only odd / even number
Implicit Requiremnts:
  - no otehr datat types
  - negative numbers allowed (classed as odd or even)

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
[2, 4, 0, 100, 4, 11, 2602, 36]
Should return: 11 (the only odd number)

[160, 3, 1719, 19, 11, 13, -21]
Should return: 160 (the only even number)

=====> Data structure(s):
Input:array
Intermediat e: array
Output: number

=====> High Level Algorithm:
iterate over the array and capture the odd and even numbers in two seperate arrays. return the first element of the captured array which has only one element

=====> Optional Implementation (Pseudo-code):
find_outlier(integers) ---> Integer

Initialize odds = odd_numbers(integers) SUBPROCESS
  - select all the numbers that are odd
  
Initialize evens = even_numbers(integers) SUBPROCESS
  - select all the numbers that are even
  
if odds.size == 1 
  - return the first element of odds
  
if evens.size == 1 
  - return the first element of evens

=end

# Code With Intent

def odd_numbers(integers)
  integers.select { |num| num.odd? }
end

def even_numbers(integers)
  integers.select { |num| num.even? }
end

def find_outlier(integers)
  odds = odd_numbers(integers)
  evens = even_numbers(integers)
  odds.length == 1 ? odds.first : evens.first
end

p find_outlier([2, 4, 0, 100, 4, 11, 2602, 36]) == 11
p find_outlier([160, 3, 1719, 19, 11, 13, -21]) == 160
```

###### Example65: Is an integer Array?

```ruby
=begin
Write a function with the signature shown below:

def is_int_array(arr)
  true
end
returns true / True if every element in an array is an integer or a float with no decimals.
returns true / True if array is empty.
returns false / False for every other input.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
returns true / True if every element in an array is an integer or a float with no decimals.
returns true / True if array is empty.
returns false / False for every other input.

Input: array

Output: bool

=====> Rules
Explicit Requiremnts:
  - returns true if arr == [] 
  - returns true / True if every element in an array is an integer or a float with no decimals.
  - returns false / False for every other input.
Implicit Requiremnts:
  - nil, string, [nil] all should return false
  -

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)


=====> Data structure(s):
Input: arr 
Intermediate:arr
Output: bool

=====> High Level Algorithm:
iterate over the array and check if all the elements are an integer or a float with no decimals.
  if yes then return true
if the array is empty then return true
otherwise return false

=====> Optional Implementation (Pseudo-code):

=end

# Code With Intent

def false_case(arr)
  return false if arr == nil || arr == ""
  arr.each do |ele|
    return false if ele == nil
    return false if ele.is_a?(String)
    return false if ele == [nil]
  end  
end

def is_int_array(arr)
  return false if false_case(arr) == false
  return true if arr.empty? 
  arr.all? { |num| num.to_f == num.to_i } ? true : false
end

### Option 2
def is_int_array(arr)
  arr.is_a?(Array) && (arr.empty? || arr.all? { |num| num == num.to_i } )
end

p is_int_array([]) == true
p is_int_array([1, 2, 3, 4]) == true
p is_int_array([-11, -12, -13, -14]) == true
p is_int_array([1, 2, nil]) == false
p is_int_array(nil) == false
p is_int_array("") == false
p is_int_array([nil]) == false
p is_int_array([1.0, 2.0, 3.0001]) == false
p is_int_array(["-1"]) == false
p is_int_array([1.2, 1.8, 3]) == false
```

###### Example66: Reverse and combine the string

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Your task is to Reverse and Combine Words.
Input: String containing different "words" separated by spaces

Output:

=====> Rules
Explicit Requiremnts:
  - More than one word? Reverse each word and combine first with second, third with fourth and so on...
  - odd number of words => last one stays alone, but has to be reversed too
  - Start it again until there's only one word without spaces
  -
Implicit Requiremnts:
  - one word doesnt change
  - odd words are reversed but not joined

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p reverse_and_combine_text("abc def") == "cbafed"
abc def
  - step 1 - cbafed

p reverse_and_combine_text("abc def ghi jkl") == "defabcjklghi"
"abc def ghi jkl"
  - step 1- cbafed ihglkj
  - step 2- defabcjklghi

p reverse_and_combine_text("dfghrtcbafed") == "dfghrtcbafed"
one word so no change

p reverse_and_combine_text("234hh54 53455 sdfqwzrt rtteetrt hjhjh lllll12  44") == "trzwqfdstrteettr45hh4325543544hjhjh21lllll"

p reverse_and_combine_text("sdfsdf wee sdffg 342234 ftt") == "gffds432243fdsfdseewttf"

"sdfsdf wee sdffg 342234 ftt"
  - step -  fdsfdseew gffds432243 ttf
  - step -  weesdfsdf342234sdffg ftt
  - step -  gffds432243fdsfdseewttf
 
=====> Data structure(s):
Input: string
Intermediate: array
Output: string

=====> High Level Algorithm:
if there is a word with no space return the word

REPEAT the following process untill one word is formed
  iterate over the words with spaces
    - reverse the words and jooin the pairs
    - if there is a word with no pair then just reverse it

=====> Optional Implementation (Pseudo-code):
reverse_and_combine_text(s) ---> string

Initialize arr = split the words into a new array
  - words are delimitted by spaces

RETURN arr.join if arr.length == 1

REPEAT until arr.length == 1
arr = reverse_join(arr) SUBPROCESS
  - reverse all the words
  - split the array into sub array of pairs
  - join the pairs and leave the odd word without a pair

RETURN arr.join 

=end

# Code With Intent

def reverse_join(arr)
  arr.map(&:reverse).each_slice(2).to_a.map(&:join)
end

def reverse_and_combine_text(s)
  arr = s.split
  return arr.join if arr.length == 1
  loop do 
    arr = reverse_join(arr)
    break if arr.length == 1
  end
  arr.join
end

p reverse_and_combine_text("abc def") == "cbafed"
p reverse_and_combine_text("abc def ghi jkl") == "defabcjklghi"
p reverse_and_combine_text("dfghrtcbafed") == "dfghrtcbafed"
p reverse_and_combine_text("234hh54 53455 sdfqwzrt rtteetrt hjhjh lllll12  44") == "trzwqfdstrteettr45hh4325543544hjhjh21lllll"
p reverse_and_combine_text("sdfsdf wee sdffg 342234 ftt") == "gffds432243fdsfdseewttf"
```

###### Example67: Integer Reduction

```ruby
=begin
In this Kata, you will be given two integers n and k and your task is to remove k-digits from n and return the lowest number possible, without changing the order of the digits in n. Return the result as a string.
p Let's take an example of solve(123056,4) ==  We need to remove 4 digits from 123056 and return the lowest possible number. The best digits to remove are (1,2,3,6) so that the remaining digits are '05'. Therefore, solve(123056,4) = '05'.
Note also that the order of the numbers in n does not change: solve(1284569,2) = '12456', because we have removed 8 and 9.
=end

=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
In this Kata, you will be given two integers n and k and your task is to remove k-digits from n and return the lowest number possible, without changing the order of the digits in n. Return the result as a string.

Input: two integers

Output: lowest possible number

=====> Rules
Explicit Requiremnts:
  - remover the digits (equal to the second argument)
  - lowest possible number after that
Implicit Requiremnts:
  - no empty args
  - positive no

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)

p Let's take an example of solve(123056,4) ==  We need to remove 4 digits from 123056 and return the lowest possible number. The best digits to remove are (1,2,3,6) so that the remaining digits are '05'. Therefore, solve(123056,4) = '05'.
Note also that the order of the numbers in n does not change: solve(1284569,2) = '12456', because we have removed 8 and 9.

p solve(123056,1) == '12056'
12305
12306
12356
12056 <------
13056
23056

p solve(123056,2) == '1056'

1230
1256
3056
1236
1056 <-----
2305

p solve(123056,3) == '056'
123
126
156
056 <-----
230

p solve(123056,4) == '05'
56
16
12
23
30
05 <------

p solve(1284569,1) == '124569'
p solve(1284569,2) == '12456'
p solve(1284569,3) == '1245'
p solve(1284569,4) == '124'


=====> Data structure(s):
Input: integers
Intermediate: array
Output: string

=====> High Level Algorithm: given 2 arguments: first arg: n, second arg\: k

create a combination of digits by removimng k digits from n. find the lowest possible combination

=====> Optional Implementation (Pseudo-code):
solve(n,k) ---> string

k.times
  Initialize digits = convert n into array of digits in string representation
  Initialize counter = 0
  initialize combo_array = []
  Loop  
    replace digits[counter] with ""
    combo_array << digits.join
    counter += 1
    break when counter == digits.length
  
  n = combo_array.min
  
return n

=end

# Code With Intent

def solve(n,k)
  k.times do 
    counter = 0
    combo_array = []
    loop do 
      digits = n.to_s.chars
      digits[counter] = ""
      counter += 1
      combo_array << digits.join
      break if counter == digits.length 
    end
    n = combo_array.min
  end
  n
end

p solve(123056,1) == '12056'
p solve(123056,2) == '1056'
p solve(123056,3) == '056'
p solve(123056,4) == '05'
p solve(1284569,1) == '124569'
p solve(1284569,2) == '12456'
p solve(1284569,3) == '1245'
p solve(1284569,4) == '124'
```

###### Example68: Divisible sum pairs

```ruby
=begin
========== THE PEDAC PROCESS ==========

=====> Problem:
Given an array (arr) of integers, and a positive integer k. Find the number of pairs (i, j) having the sum (arr[i] + arr[j]) that is divisible by k and i < j.

Input: array and integer

Output: Integer

=====> Rules
Explicit Requiremnts:
  - find the number of pairs (i, j) whose sum is divisible by k and i < j
  - 
Implicit Requiremnts:
  - all numbers are positive
  - 

=====> (Any Questions / Assumptions needing clarification?)
(e.g. return the same string object or an entirely new string???)

=====> Examples, Edge Cases(test rules and boundaries)
p divisible_sum_pairs([1, 3, 2, 6, 1, 2], 3) #== 5
[1, 3, 2, 6, 1, 2]
1, 3
1, 2 * 
1, 6
1, 1
1, 2 * 

3, 2
3, 6 * 
3, 1
3, 2

2, 6
2, 1 
2, 2

6, 1
6, 2

1, 2 * 

p divisible_sum_pairs([8, 10], 2) #== 1
8, 10

p divisible_sum_pairs([5, 9, 10, 7, 4], 2) #== 4
5, 9  * 
5, 10 
5, 7  * 
5, 4

9, 10
9, 7  * 
9, 4  

10, 7
10, 4 * 

7, 4

p divisible_sum_pairs([29, 97, 52, 86, 27, 89, 77, 19, 99, 96], 3) #== 15

=====> Data structure(s):
Input: Arrays, Integer
Intermediate: arrays
Output: integer

=====> High Level Algorithm:
Given two arguments  an array and an Integer

Iterate over the array and create all possible combination of integers in pairs. choose the ones whose sum is divisible by the second argument and tthe ones where the first number is lesser than the second. return the count of such combination

=====> Optional Implementation (Pseudo-code):

divisible_sum_pairs(arr, k) ---- > integer

combo_pair(arr, k) - SUBPROCESS
  - Initialize combo = []
  - create all possible combination of integers in pairs.
  - select the ones whose sum are divisble by k and first num < second num

return the count of combo_pair

=end

# Code With Intent

def combo_pair(arr, k)
  combo = []
  arr.combination(2) { |a| combo << a }
  combo.select { |sub| sub.sum % k == 0 }.count
end

def divisible_sum_pairs(arr, k)
  combo_pair(arr, k)
end

p divisible_sum_pairs([1, 3, 2, 6, 1, 2], 3) #== 5
p divisible_sum_pairs([8, 10], 2) #== 1
p divisible_sum_pairs([5, 9, 10, 7, 4], 2) #== 4
p divisible_sum_pairs([29, 97, 52, 86, 27, 89, 77, 19, 99, 96], 3) #== 15
```



