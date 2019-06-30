3 Tic Tac Toe Analyser
Summary: write functions for analysing the game of tic-tac-toe inside a C++ program called tttanalyzer.cpp, and make a tally of all possible games.

3.1 String-representation tttresult
Write a function with the following signature:

char tttresult(string tttboard);
The string tttboard has nine characters representing the current situation in a game of tic tac toe:

x represents x
o represents o
hashtag represents an unplayed space
The first three characters are the top row, the next three the middle row, and the last three are the bottom row.

So the line:

xox#x#xox
represents the board

 x |  o  |  x  
   |     |      
---+-----+-----
   |  x  |
---+-----+----- 
   |     |  
 x |  o  |  x
The program should classify the board as one of the following:

t: tie game and no spaces left
x: valid, x has won
o: valid, o has won
c: valid, game continues
i: invalid
e: error condition (bad shape of board, bad chars)
An invalid game board is one in which there was a rule violation. A game can be invalid for many reasons, such as too many winners, unbalanced number of x’s and o’s, etc.

Do not “anticipate” tie games: a game is considered a tie only if all the spaces are filled.

3.1.1 Examples
tttresult("xox#x#xox") returns i

It is invalid because x played 5 times and o only played 2 times.

tttresult("xoxoxoxox") returns x

3.2 Vector-representation tttresult
Write a function with the following signature:

char tttresult(vector<Move> board);
The function should return the same return codes as the previously defined function with the same name.

Each move is for either player x or player o, and records the row and column of the moves.

The row and column numbers are from 0 to 2.

The order of the Move objects inside the vector is not significant, and in particular, does not represent the order of the moves in a game.

This representation is meant to be equivalent to the nine-letter string representation.

3.2.1 About The Move class
The new class Move is defined as follows:

struct Move {
    int r;
    int c;
    char player;
};
The structure Move is defined in the file movedef.h which must be included in your code using

#include "movedef.h"
3.2.2 Example code using Move:
Here is some example code using the new data structure Move:


#include "movedef.h"

int main() {
  vector<Move> moves;
  bool error;
  char result;

  Move m; // make a move 
  m.r = 0; // fill the data
  m.c = 1;
  m.player = 'x';

  moves.push_back(m); // put the move on the vector representing the board.

  result = tttresult(moves);  // returns 'c'
  result = tttresult("###xxxoo#"); // returns 'x'
  result = tttresult("xxxoooHI!"); // returns 'e'
}
3.3 Function get_all_boards
Write a function get_all_boards which generates all 
3
9
 possible tic-tac-toe boards.

The function signature is

vector<string> get_all_boards();
The vector should contain all possible tic-tac-toe boards. The order is not important.

3.4 Create your Tally
Your program should print a table of the five possible outcomes toxic and the frequency of that result for all 
3
9
 possible tic-tac-toe boards.

The output should look like

x 2213
o 1234
t 1234
i 4524
c 12313
except that the numbers should be the real numbers calculated by analyzing all the boards.

The order is irrelevant: you can print out the table in any order.

You should use get_all_boards and tttresult to generate the tally.

Your program must contain the line

// MAIN
just before your declaration of main() so that I can properly check it.

3.5 Restrictions
You may include the following libraries but no others:

<iostream>
<string>
<array>
<vector>
<map>
"movedef.h"
