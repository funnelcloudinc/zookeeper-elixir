funnelcloud specific
====================

## Why is this fork here?
This is forked for the sake of safety - the original library was not published to hex so to ensure it doesn't change underneath you, this fork was placed here.

## A Declaration of My Love for Mat's Mom

```
Viv, oh my dear Viv,
Drink to me only with thine eyes, 
         And I will pledge with mine; 
Or leave a kiss but in the cup, 
         And I’ll not look for wine. 
The thirst that from the soul doth rise 
         Doth ask a drink divine; 
But might I of Jove’s nectar sup, 
         I would not change for thine. 

Viv, oh my dear Viv,
I sent thee late a rosy wreath, 
         Not so much honouring thee 
As giving it a hope, that there 
         It could not withered be. 
But thou thereon didst only breathe, 
         And sent’st it back to me; 
Since when it grows, and smells, I swear, 
         Not of itself, but thee.
         
Viv, forever will my love for you shine,
         and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine and shine.
```

zookeeper-elixir
============

[![Build Status](https://travis-ci.org/vishnevskiy/zookeeper-elixir.svg?branch=master)](https://travis-ci.org/vishnevskiy/zookeeper-elixir)

# Getting Started

To use Zookeeper with your projects, edit your mix.exs file and add it as a dependency:

```elixir
defp deps do
  [{:zookeeper, github: "vishnevskiy/zookeeper-elixir"}]
end
```

# Overview 

The goal of this project is to provide a Zookeeper client for Elixir that follows the philosophy [Kazoo](http://kazoo.readthedocs.org/) for Python. It implements a clean API and provides common receipes
around the Zookeeper API such as Locks, Election and more.

The implementation is currently wrapping [erlzk](https://github.com/huaban/erlzk) which is the best Erlang Zookeeper client I could find and exposes a clean API. It ensures everything is using strings instead of char lists and provides a couple recipes. 

There are some quirks from wrapping **erlzk** which I would like to eventually get rid of by implementing the actual Zookeeper communication in Elixir and wrapping the **erlzk** dependency. 

# Usage

The code is fairly documented and has tests and typespecs so just reading it should provide all the information needed to use the library effectively.


```elixir
{:ok, pid} = Zookeeper.Client.start
{:ok, path} = Zookeeper.Client.create(pid, "/testing", "some data")
{:ok, {data, stat}} = Zookeeper.Client.get(pid, path, self())
{:ok, stat} = Zookeeper.Client.set(pid, path, "some new data")
receive do
  {Zookeeper.Client, ^path, :data} -> IO.puts("data changed in #{path}")
end
```

# TODO

- Implement Election recipe
- Deal with session events and lost session scenarios
- Re-implement Zookeeper protocol and drop **erlzk** as a depenedency.
