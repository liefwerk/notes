# object_methods

Let's talk about instance methods in Ruby.
We'll come inside a class and give it some methods.

Then once we create an object we'll be able to use that method.

```ruby
class Student
    attr_accessor :name, :major, :gpa
    def initialize(name, major, gpa)
        @name = name
        @major = major
        @gpa = gpa
    end
end

student1 = Student.new("Jim", "Business", 2.6)
student2 = Student.new("Pam", "Art", 3.6)
```

Let's create a method to check if the student has honor (boolean)

```ruby
def has_honors
    if @gpa >= 3.5
        return true
    end
    return false
end
```

That method will be put inside out class, below the initialize method.

```ruby
class Student
    attr_accessor :name, :major, :gpa
    def initialize(name, major, gpa)
        @name = name
        @major = major
        @gpa = gpa
    end
    def has_honors
        if @gpa >= 3.5
            return true
        end
        return false
    end
end

student1 = Student.new("Jim", "Business", 2.6)
student2 = Student.new("Pam", "Art", 3.6)
```

Then if we call that method, each object will have a different output

```ruby
student1.has_honors
student2.has_honors
```

that prints

```ruby
true
false
```
