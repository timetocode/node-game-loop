Edit: 2018
==============
JavaScript timers have improved quite a bit since this repo was created in 2014. The following code can test this:
```js
const hrtimeMs = function() {
    let time = process.hrtime()
    return time[0] * 1000 + time[1] / 1000000
}

const TICK_RATE = 20
let tick = 0
let previous = hrtimeMs()
let tickLengthMs = 1000 / TICK_RATE

const loop = () => {
    setTimeout(loop, tickLengthMs)
    let now = hrtimeMs()
    let delta = (now - previous) / 1000
    console.log('delta', delta)
    // game.update(delta, tick) // game logic would go here
    previous = now
    tick++
}

loop() // starts the loop
```
Delta here is in units of seconds (not milliseconds, like it was in the original). The perfect delta at this TICK_RATE would be 0.050000000000. A delta of 0.051 is off by 1 millisecond. If running this code produces satisfactory accuracy on the target machine, then it may be a superior option to the node-game-loop.


node-game-loop (original readme)
==============

A game loop in node.js capable of accurate frame rates. 

This is an alternative to setTimeout/setInterval loops which are accurate to within 16 ms.

This is also an alternative to a pure setImmediate loop which is nice and accurate, but will use 100% CPU (well, 100% of one thread) even while idle.

