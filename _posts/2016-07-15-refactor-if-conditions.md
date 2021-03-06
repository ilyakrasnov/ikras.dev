---
layout: post
title: Refactor If Conditions
date: 2016-07-15 09:31:56 +0300
img: rook.jpg
credit: Benjamin Smith
---


Doing a lot of refactoring work myself and guiding a group coding bootcamp students through their final project I came across different steps one could take to make the code much cleaner and the app more readable and understandable.

Oftentimes, especially in more complex applications, there is a need to check different conditions. As an example I would use a chess app my stundents were implementing as their final project.

Here is the concrete example: **Implement valid_move? method for the rook piece**

Thinking through the logic of this method we need to consider following aspects:

1. Check if we are actually moving the piece (new coordinates are not the same as current coordinates)
2. Check if the new coordinates are inside the chess board (1 to 8 or 0 to 7 depending on the implementation of the board)
3. Check if the rook is only moving vertically or horizontally


At this point we don't care so much whether there is another piece at the destination.

Following the three requirements we would come up with the following implementation:

{% highlight ruby %}
class Rook < Piece
  attr_accessible :x_coord, :y_coord

  def valid_move?(new_x, new_y)
    if !(new_x == x && new_y == y) &&
       new_x <= 8 && new_y <= 8 && new_x >=1 && new_y >=1 &&
       (new_x != x_coord && new_y == y_coord || new_x == x_coord && new_y != y_coord
      return true
    else
      return false
    end
  end
end
{% endhighlight %}

I once heard that we should make our code readable and understandable for other developers. *Other developers* is also yourself in two weeks. Now looking at the code I wrote just a few minutes ago it's already hard for me instantly grasp what the actual conditions are.

The main problem with it is that one needs to make a mental shift between the logic and its implementation. Checking *!(new_x == x && new_y == y)*
is the implementation of a concept of *being at different position*. While the concept is understandable for humans, the actual implementation of it is not that important.

In one of the *weekly iteration* episodes of [Upcase](https://thoughtbot.com/upcase/videos/refactoring-extraction-namin://thoughtbot.com/upcase/videos/refactoring-extraction-naming) the Chris and Ian talked exaclty about this topic and discussed different refactoring strategies. Here I want to use one of them claiming that its one of the most important techniques to learn and adopt while being an easy one.

## Exctract method

We are going to pull out the if-conditions and replace them with simple method calls giving each one a name. Here is why its a great way to do it:

> ... if we pull out a chunk of code, then the chunk now needs a name in order to refer to it. [...] The more names we can build into your application, the easier it is to build a mental model of what that code is and does.

By applying this simple technique we end up with the following implementation:
{% highlight ruby %}
class Rook < Piece
  attr_accessible :x_coord, :y_coord

  def valid_move?(new_x, new_y)
    if  move_from_current_position?(new_x, new_y) &&
        on_board?(new_x, new_y) &&
        one_directional_move?(new_x, new_y)
      return true
    else
      return false
    end
  end

  private

  def move_from_current_position?(new_x, new_y)
    !(new_x == x && new_y == y)
  end

  def on_board?(new_x, new_y)
    new_x <= 8 && new_y <= 8 && new_x >=1 && new_y >=1
  end

  def one_directional_move?(new_x, new_y)
    valid_horizontal?(new_x, new_y)  || valid_vertical?(new_x, new_y)
  end

  def valid_horizontal?(new_x, new_y)
    new_x != x_coord && new_y == y_coord
  end

  def valid_vertical?(new_x, new_y)
    new_x == x_coord && new_y != y_coord
  end
end
{% endhighlight %}

## Explain it to a 5 year old child
One of the reasons I love this technique so much is that it makes our code human readable. Imagine explaining to a 5 year old the rules to move the rook. You can just open your editor and read the code out loud:

> You can move the rook to another position than it is now. You can not move outside the board. You can only move up or down (here you can teach the kid what **vertically** means) or left or right (**horizontally**).
