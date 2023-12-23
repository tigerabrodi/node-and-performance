# Node, JavaScript and Performance

## Regex shorter strings

Each time a regex is executed, there's a certain amount of overhead. This includes compiling the regex (if it's not pre-compiled), setting up the search, and then performing the search. When you run a regex on many short strings, this overhead is incurred each time the regex is executed, which can add up to a significant cost.

## Express things in numbers

As a general rule of thumb a good chunk of optimizations are about expressing things in numbers, the main reason being that CPUs are crazy good at working with numbers.

CPUs are designed to perform arithmetic and logical operations very efficiently. These operations include addition, subtraction, multiplication, division, and bitwise operations, which are fundamental to numerical processing.

## Use existing methods of JS

In JS, we have many methods like .slice, use them over regex if possible.
