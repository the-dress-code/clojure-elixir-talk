# In Clojure, one of the more popular concurrency models is expressed in core.async.

/ GPT Assertions:

// Transition line:
“In Elixir, we model concurrency with isolated processes that communicate via messages — the actor model. In Clojure, a comparable approach is provided by core.async, which implements Communicating Sequential Processes with channels and lightweight go blocks.”

// Optional follow-up clarification:
“Unlike actors, go blocks aren’t OS processes — they’re coroutines that suspend on channel operations, letting you coordinate thousands of concurrent workflows without threads or locks.”

# Define:

chan - creates a channel with an optional buffer (a pipe)

go - asynchronously executes the body, returning immediately to the calling thread

<! (take) - takes a val from port

>! (put) - puts a val into port

thread - Executes the body in another thread, returning immediately to the calling thread. Returns a channel which will receive the result of the body when completed, then close.

alts!! lets you take a thing off a channel randomly

# Summary

chan is the channel / pipe you put data on / send data thru

you take or put things off the channel

go - asynchronously executes the body (putting or taking things off the chan), returning immediately to the calling thread (not sure what the last part means,... whats the thread? thread - Executes the body in another thread, returning immediately to the calling thread. Returns a channel which will receive the result of the body when completed, then close.)

alts!! lets you take a thing off a channel randomly

 --------

robert says
your explanation seems ok
various other cool things in there too
you have the basics though
go loop = create machine that can work on its own
channels = ways to communicate between machines
it’s that simple

# How do you think you could put them together to do something that you could not do otherwise?

i dont know yet

# What do you want to get across in your core.async section?

- it is cool enough to stand up against Elixir Actor model
- some of the components that work together to make the cool stuff happen
    - transmit data on queue-like channels (chan)
    - take data off or put data on the channel: blocking or non blocking depending on what you need
    - ...

# Post diagram exercise summary

- abstractions that let you separate "do" from "here is this thing" and "use this thing"
- queue the process (with channels)
- create the process (with a go block) - u can have tons of go blocks
- 1. (go (>! d (stuff (<! c))))
- 2. (>! c "What's up")
- 3. (<! d)

(go (>! d (stuff (<! c))))
> says go do the following somewhere in space: take what is on channel c > do stuff to whatever is on channel c > put the result of that work onto channel d

(>! c "What's up")
> says put "Whats up" on the c channel

(<! d)
> says take what is on channel d