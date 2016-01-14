# Note
 + [block和yield](http://haoluobo.com/2011/07/ruby-block-yield/)
 + [to_s vs. to_str](http://rubylution.herokuapp.com/topics/17)
 + [to_s vs. inspect](http://rubylution.herokuapp.com/topics/19)
 + [Ruby send vs. \_send\_](http://stackoverflow.com/questions/4658269/ruby-send-vs-send)
 + [Understanding Ruby Singleton Classes](http://www.devalot.com/articles/2008/09/ruby-singleton)
 
# Grammar

```Ruby
//subclass can invoke parent behavior via super, like:
def bark
	super + ",GROWL"
end

//inside a class function, self refers to the object not the class. like :

class Dog
	def get_self
		self
	end
end

fido = Dog.new
assert_equal fido, fido.get_self

// yield占位符

//next类似continue

//unless是if的另外一种实现方式，但是取值false
 
first_name, *last_name = ["John", "Smith", "III"]
assert_equal "John", first_name
assert_equal ["Smith", "III"], last_name

```
 
