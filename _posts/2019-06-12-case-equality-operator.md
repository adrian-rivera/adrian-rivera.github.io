---
title: The Case Equality Operator
tags: [ruby]
---
Here we will review the mechanism that ruby uses to solve
a `case-when` statement.

```ruby
test_string = 'This option'

case test_string
when 'Not this option'
  puts 'Wrong'
when 'This option'
  puts 'Correct'
end
```

It is easy to figure the result from the last snippet, but the question is: what
is the logic that ruby is using behind the `case-when` statement?

The answer to that is the `===` operator, to prove that, let's rewrite the
previous snippets using an `if-else` statements:

```ruby
test_string = 'This option'

if 'Not this option' === test_string
  puts 'Wrong'
elsif 'This option' === test_string
  puts 'Correct'
end
```

Usually behind the scenes `===` is using the `==` operator to compare the values,
but as any other method in ruby this can be overriden.

Let's see how we can use `===` with a simple example:
```ruby
class Odd
  def self.===(other)
    other % 2 == 0
  end
end

class Even
  def self.===(other)
    other % 2 == 1
  end
end

def is_odd?(value)
  case value
  when Odd
    true
  when Even
    false
  else
    raise
  end
end

value_0 = 8
value_1 = 7

is_odd? value_0
is_odd? value_1

Odd == value_0
Even == value_0

Odd == value_1
Even == value_1
```

Then we would have the following output:
```ruby
> is_odd? value_0
=> true
> is_odd? value_1
=> false
> Odd == value_0
=> false
> Even == value_0
=> false
> Odd == value_1
=> false
> Even == value_1
=> false
```

See how `is_odd?` function is able to differentiate between an odd or an even
number, but that doesn't mean that `Odd` is equal to `value_0`, the comparison
in the `case` statement is done using `===`.

## Finally
To summarize this post just remember:
* `case-when` statement will use the method `===` to do the comparison between
   values.
* Generally `===` will use `==` to make a comparison between values, but you can
  override this behavior.

## Source
* David A. Black & Joseph Leo III, _The Well-Gounder Rubyist, Third Edition_,
  Manning Publications
