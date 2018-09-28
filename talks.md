---
layout: page
title: Talks
permalink: /talks/
---

## [PyOhio 2017](https://www.pyohio.org/2017/schedule/presentation/256/)
### Using Machine Learning to Play Chess

#### Video
<div align="left">
    <iframe width="320" height="180"
        src="https://www.youtube.com/embed/bJfqn4Ysvsk">
    </iframe>
</div>

#### Abstract
How do chess engines work?
If you mean The Turk, a late 18th century automaton chess player who once played Napoleon,
turns out it was a hoax. There was a human chess player hidden inside the whole time.
Thankfully, computer chess has gotten better since then. A modern chess engine consists of several main components,
an evaluation function, and a depth searching algorithm. A depth searching algorithm will look ahead a
few moves and try to get to the best position possible, assuming the opponent plays well.
Commonly an algorithm such as Minimax will be used to accomplish this.
The evaluation function does exactly what the name implies.
It takes a position on the chessboard and evaluates it for how good it is for a certain player.
Basic evaluation functions sum up all the pieces on the board and subtract the sum of the opponent’s pieces, assigning a weight to each piece.
This is where the handcrafted code from a human chess player gets put in.
More complex evaluation functions can have many static lines of code that evaluate the board based on traditional chess strategy.
This is where the hidden man lies in the automaton.

How do we make a chess engine come up with it’s own evaluation function based on its own strategy?
With machine learning, we can do just that.
With Python, we can utilize Tenserflow to create a neural network that takes in each square of the board as inputs and outputs how favorable the position would be to a specific player.
Since chess is a win/loss game, over time, the network will learn what works and what doesn’t to be more effective.
The cost function in this situation would be number of losses, and the algorithm would try to minimize it.

## [PyCon 2017](https://us.pycon.org/2017/schedule/presentation/767/)
### KnightSky: A Chess Engine that Learns

#### Description
When IBM’s Deep Blue beat reigning chess champion Garry Kasparov in 1997, it was established that computers could beat even the best human at chess.
Today, chess engines contain many lines of code handcrafted under the guidance of grandmasters.
Are you interested in being knee deep in chess theory just to crank out a half decent engine? No?
This talk is for you. Why not create an engine that learns to improve itself?
I created KnightSky to do just that.

## [PyGotham 2016](https://2016.pygotham.org/talks/324/abstractions-and-building/)
### Abstractions and building up: A case study with chess_py, an open source chess platform

#### Video
<div align="left">
    <iframe width="320" height="180"
        src="https://www.youtube.com/embed/87vhc96OSFQ">
    </iframe>
</div>

#### Abstract
Programming is complex and can seem disconnected from reality.
Objects, methods of storing data, and following the flow of a project can seem daunting.
The basics of chess is far easier to understand.
There is a well-defined board, containing well-defined pieces that follow well-defined rules.
And it is all in the real world. Chess_py is a platform for chess that converts all of that to code.
A game object is created using player objects. These player objects can either be human, in which case a person must enter moves into the console, or artificial intelligence,
in which case the artificial intelligence returns the move it would make given the position. When a player gives the game object a move,
it is stored as a move object, which is then validated. The board is stored as an object,
and it holds all the piece objects. These piece objects know how they are moved,
and are capable of returning the all of their possible moves in a given position.
If the given move matches one of the possible moves of the piece on the board, it is legal.
The board is changed to reflect the new position. Some external code detects when the game ends and the result.
Data such as the board and player color are stored with standard data types such as lists and booleans.
However, they are built into wrapper classes that allow the rest of chess_py to read and manipulate the data with ease,
especially in the context of chess.
Chess_py is essentially an abstraction of the game of chess, containing abstractions of the components of chess.
Understanding it can help us better understand the nature of Python. This abstraction is also a foundation.
Chess_py allows for a simple way for a chess playing program or any other sort of software to interface with it.
As long as that software can provide legal moves stored in the type of object chess_py uses to store objects, it can play chess without having to worry about any of the lower level work.
This is highly important as it allows software to build on top of each other to do complex tasks relatively simply.
If classes, objects, and functions did not exist in python, creating a program that simply plays chess would be a nightmare.
Abstractions allow us to modularize our code to make it much easier to focus on the task at hand instead of working from the ground up.
