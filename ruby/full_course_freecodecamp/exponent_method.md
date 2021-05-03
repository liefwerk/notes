# exponent_method

An exponent method would take two numbers, the base and power number.
Let's build one.

```ruby
def pow(base_num, pow_num)
  result = 1
  pow_num.times do
      result *= base_num
  end
  return result
end

puts pow(5, 2)
```
