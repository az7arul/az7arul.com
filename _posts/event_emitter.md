{{{
	"title" : "Node EventEmitter",
	"tags" : ["node", "observer pattern", "events"],
	"category" : "javascript",
	"date" : "4-21-2013"
}}}


"Talk is cheap show me the code"
--------------------------------


	var EventEmitter = require('events').EventEmitter;

	var Ticker = function(){
		var self = this;
		self.startTicking = function(){
			self.emit('tick');
			setTimeout(self.startTicking, 1000);
		}
	}

	Ticker.prototype = new EventEmitter();

	var ticker = new Ticker();

	ticker.startTicking();

	ticker.on('tick', function(){
		console.log('got a tick');
	});
	
<!--more-->
Output
------------

	got a tick
	(1 second delay)
	got a tick
	(1 second delay)
	got a tick
	(1 second delay)
	got a ...

Explanation
------------

First we require `EventEmitter` and  define a `Ticker` class  that has a method `startTicking` which _emits_ an event **tick** every 1 second.

Then we make `Ticker` inherit from it(`EventEmitter`) by setting `Ticker`'s  prototype to an `EventEmitter` object. Note that we could have also used `util` from node like below for inheriting.

	var util = require('util');
	util.inherits(Ticker, EventEmitter);


After that we instansiate a `Ticker` object **ticker** and call __startTicking__ method on it.

Finally, we add a listener for the **tick** event which outputs "got a tick" every time it receives a **tick** event.

