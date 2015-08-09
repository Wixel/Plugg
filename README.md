## Plugg: A bolt-on Ruby plugin framework

[![Gem Version](https://badge.fury.io/rb/plugg.svg)](https://rubygems.org/gems/plugg)
[![Build Status](https://travis-ci.org/Wixel/Plugg.svg)](https://travis-ci.org/Wixel/Plugg)

Simple, efficient plugin framework for your Ruby applications.

Plugg works by loading all plugin files from a specified path and saving instances of each plugin to a singleton registry which handles dispatching messages to the classes. If the plugin class supports the message, it's response is added to a return buffer.

Any Ruby class can be used as a plugin, there are no external dependencies.

Requirements
-----------------

We recommend that you use Ruby 2.0.0 or higher.

Installation
-----------------

    gem install plugg

Getting Started
-----------------

It's really simple to get Plugg running, after the installation, you simple require it and set the source directory where the plugin classes should be loaded from. You can also specify more than one source directory by passing an array to the *Plugg.source(path)* method. Once caveat is that plugin class names should match the plugin file names exactly.

```ruby
require 'plugg'

Plugg.source('./plugin') # or Plugg.source(['./plugin1', './plugin2'])

result = Plugg.send(:test_method)
```

In the above example, you are sending the *:test_method* message to each plugin class in the loaded registry and returning the output from each of these calls in an array (result).

The *:test_method* message should correspond to a method with the same name in the plugin class:

    cat DemoPlugin.rb

```ruby
class DemoPlugin
  def test_method
    puts "Inside test_method"
  end

  def to_s
    "Demo Plugin"
  end
end
```

You can also pass any number of arguments to the plugin methods when they are called:

```ruby
result = Plugg.send(:test_method, arg1, arg2 arg3, etc)
```

Execution result
-----------------

You can return anything you need from your plugin methods and can easily access the return data inspecting the result from *Plugg.send()* method:

```ruby
[
  {
    :plugin => "Demo Plugin",
    :return => nil,
    :timing => 0.013
  }
]
```

The power of Plugg starts revealing itself when you are running many plugins with many different methods. 

Running the tests
-----------------

To test the current stable version of Plugg, simply run:

    rake test

License
-----------------

Please see [LICENSE](https://github.com/Wixel/Plugg/blob/master/LICENSE) for licensing details.

Author
-----------------

Sean Nieuwoudt, [@seannieuwoudt](https://twitter.com/seannieuwoudt) / [http://isean.co.za](http://isean.co.za) / [https://wixelhq.com](https://wixelhq.com)
