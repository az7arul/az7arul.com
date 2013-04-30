{{{
	"title" : "Object Like Hash",
	"tags" : ["ruby", "hash"],
	"category" : "ruby",
	"date" : "4-28-2013"
}}}


"My crime is that of curiosity"
---------------------------------

While I was going through the source code of [camping](https://github.com/camping/camping) this piece of code that gives you Object like __Hash__ got my attention. Instead of using Hash['key'] it allows you to use Hash.key hence the name "Object Like Hash".

Code
------
	class H < Hash
		def method_missing(m,*a)
  			m.to_s=~/=$/?self[$`]=a[0]:a==[]?self[m.to_s]:super
  		end

  		undef id, type if ?? == 63
  	end

Usage
--------

<!--more-->
	olh = H.new
	olh.key1 = 'value1'
	olh.key2 = 'value2'
	
	olh.key1 #=> 'value1'
	olh.key2 #=> 'value2'

Explanation
--------------

`H` is our object like hash. It inherits from `Hash`. The interesting part lies in changing its `method_missing` method. What the complex looking one liner does is :

If the method contains `=` at the very end it is an assignment. So, calling 

`olh.key1= "value1"`
 translates to `olh["key1"] = 'value1'`

 Otherwise (when we call `olh.key1`) it returns `olh["key1"]`.

 You may be wondering what does this line do :

	undef id, type if ?? == 63

 Well it undef's id and type when it is not ruby 1.9 or higher.  `?? == 63` returns true if it is not ruby 1.9.* or higher.
