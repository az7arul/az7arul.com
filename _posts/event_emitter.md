{{{
	"title" : "Node EventEmitter",
	"tags" : ["node", "observer pattern", "events"],
	"category" : "javascript",
	"date" : "4-21-2013"
}}}



Talk is cheap lets code
-----------------------


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
	

Explanation
------------

First we require EventEmitter and make Ticker inherit from it by setting Ticker's 
prototype to an EventEmitter object.

Then we define a `startTicking` function which _emits_ an event **tick** every second.

After that we instansiate a ticker object and call startTicking method.

Finally, we add a listener for the **tick** event.

