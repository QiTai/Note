# Note
 + [block和yield](http://haoluobo.com/2011/07/ruby-block-yield/)
 + [to_s vs. to_str](http://rubylution.herokuapp.com/topics/17)
 + [to_s vs. inspect](http://rubylution.herokuapp.com/topics/19)
 + [Ruby send vs. \_send\_](http://stackoverflow.com/questions/4658269/ruby-send-vs-send)
 + [Understanding Ruby Singleton Classes](http://www.devalot.com/articles/2008/09/ruby-singleton)
 + Ruby是强类型，动态语言，动态类型语言
 + puts,gets也是有对象的，对象是self
 + The most important thing to take away from all of this is that every method is being done by some object, even if it doesn't have a dot in front it. If you understand that, then you're all set
 + Array的each do方法，是Ruby炫酷之一
 
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
 
