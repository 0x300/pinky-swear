pinky-swear
===========

PinkySwear is a [when.js](https://github.com/cujojs/when) promise wrapper around node's [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter) class. This provides a simple way to get data back from the event listeners after emitting an event.

## Use
### Syncronously running event listeners
```js
const PinkySwear = require('pinky-swear');

class Challenge extends PinkySwear {
    constructor(name) {
        super();
        this.name = name;
    }

    async complete() {
        const result = await this.emit('challenge-completed');

        // result is an array of results from the listeners, so get the first one
        const awards = result[0];

        console.log(`${this.name} completed and awarded ${awards.points} points!`);
    }
}

const visitStore = new Challenge('Visit a store');

// Register an event listener on the thing extending PinkySwear
visitStore.on('challenge-completed', () => {
    // Do something when event is emitted and return some data back to the emitter
    return ({
        points: 10,
    });
});

// Run to see output
visitStore.complete();
```

### Asyncronously running event listeners
TODO: Add async example

## Test

```bash
npm test
```
