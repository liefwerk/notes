# case_expressions

Very useful when we want to check a lot of different situations.
Here's how we construct one.

```ruby
def get_day_name(day)
  day_name = ""

  case day
  when "mon"
    day_name = "Monday"
  when "tue"
    day_name = "Tuesday"
  when "wed"
    day_name = "Wednesday"
  when "thu"
    day_name = "Thursday"
  when "fri"
    day_name = "Friday"
  when "sat"
    day_name = "Saturday"
  when "sun"
    day_name = "Sunday"
  else
    day_name = "Fuck! An error!"
  end

  return day_name
end

puts get_day_name("tu")
```

Very appropriate when checking the same value against a lot of situations.
