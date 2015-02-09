---
layout: post
title: "Creating Custom Validators in Rails"
date: 2015-02-09 16:01
tags: rails validation code
comments: true
---
Finally, a post about code! I found it odd that I started a 
[blog]({% post_url 2014-10-30-embarking-on-a-new-adventure %}) intended to document my coding
adventures and I have yet document anything related to code at all. So, the other night I was
working on a personal rails project and I ran into a situation where the available rails
validations were not quite what I needed.

###Validation Rules
In my model had an attribute *numbers* which is an array of integers. In this array each number
must be **unique** and must be one of the **valid numbers** allowed.

###Custom Methods
One way to implement these validations is using 
[custom methods](http://guides.rubyonrails.org/active_record_validations.html#custom-methods).
This is a great way to create a custom validation by using a private method in the model class
that adds errors to the model when the attribute is invalid. To do this for our uniqueness
validation rule we simply create a private validation method and call it using `validate`. 

{% highlight ruby %}
class Game < ActiveRecord::Base
  serialize :numbers Array

  validate :numbers_are_unique

  private
  def numbers_are_unique
    # if there are duplicates numbers.uniq.count will be less than the actual count
    unless numbers.uniq.count == numbers.count
      errors.add(:numbers, 'is not a unique array')
    end
end
{% endhighlight %}

While this is great(and what I originally did), I wanted to explore creating a custom validator
I could use across my app since I had another model that had a similar array of numbers that
follows the same validations.

###Custom Validators
The rails documentation has a great example of how to write a
[custom validator](http://guides.rubyonrails.org/active_record_validations.html#custom-validators).
This is what I followed to create two custom validators `UniqueArrayValidator` and
`InclusiveArrayValidator`. Both these validators are not specific to my project and could be used
with any array(even if the values are not integers). I placed them in `app/validators`, but others
recommend putting them in `lib/validators`. If you put them in your lib folder you'll have to make
sure they're loaded when rails starts.

Here's our new UniqueArrayValidator
{% highlight ruby %}
class UniqueArrayValidator < ActiveModel::EachValidator
  def validate_each(record, attribute, value)
    unless value.uniq.count == value.count
      record.errors[attribute] << (options[:message] || 'is not a unique array')
    end
  end
end
{% endhighlight %}

For our InclusiveArrayValidator we want to be able to pass in an array of valid values to check
against. This is easily done by passing a value in the `options` hash.

Here's our InclusiveArrayValidator
{% highlight ruby %}
class InclusiveArrayValidator < ActiveModel::EachValidator
  def validate_each(record, attribute, value)
    valid_values = options[:valid_values]
    if value.any? { |n| !valid_values.include? n }
      record.errors[attribute] << (options[:message] || 'has invalid values')
    end
  end
end
{% endhighlight %}

###Using Custom Validators
Now we alter our model by removing the custom method and calling our new validators just as we 
would any built in rails validator. You can see we pass in the `valid_values` just as we would
any other option needed for validations.

{% highlight ruby %}
class Game < ActiveRecord::Base
  VALID_NUMBERS = [1, 2, 3, 4, 5]

  serialize :numbers, Array

  validates :numbers, unique_array: true,
    inclusive_array: { valid_values: VALID_NUMBERS }
end
{% endhighlight %}

Now our *numbers* array is validated for uniqueness and that it only includes the values we deem
valid for our use case. I hope this was helpful for anyone looking to implement a custom validator
in their rails app. I'm open to suggestions on how to improve the validators, best practices, and
even naming(I'm not sure inclusive is the correct way to describe that validation). Feel free to
leave a comment.
