# tttanalyzer.cpp
Assignment 5
Tic Tac Toe Game Analyzer

EC327 Summer 2019

1 Introduction
1.1 Assignment Goals
1.2 Group Size
1.3 Due Date
1.4 Assignment Value
1.5 Late policy
1.6 Submission Link
2 Background
2.1 Rules of Tic Tac Toe
3 Tic Tac Toe Analyser
3.1 String-representation tttresult
3.2 Vector-representation tttresult
3.3 Function get_all_boards
3.4 Create your Tally
3.5 Restrictions
3.6 Program structure
3.7 Example starting file
4 Hints and suggestions
4.1 Using map
4.2 All the boards
5 Downloads
5.1 Move class
5.2 Checker
6 Grading Scheme
1 Introduction
1.1 Assignment Goals
The assignment goals are to help you learn about

game logic
data structures and vectors
error handling
1.2 Group Size
The maximum group size is 3 students.

1.3 Due Date
This assignment is due Tuesday June 11th at 23:59 (i.e. 11:59pm) (extended by 4 days).

1.4 Assignment Value
This assignment is worth 10 points.

Style counts for 20% of the grade.

1.5 Late policy
Late assignments will be accepted until the beginning of the lecture immediately following the due date (lectures are Monday through Thursday mornings.)

If the natural grade on the assignment is 
g
, the number of hours late is 
h
, and the number of hours between the assignment due time and the next class is 
H
, the new grade will be

(h > H) ? 0 : g * (1- h/(2*H))
If the same assignment is submitted ontime and late, the grade for that component will be the maximum of the ontime submission grade and the scaled late submission grade.

1.6 Submission Link
You can submit here: tttanalyzer submit link

2 Background
2.1 Rules of Tic Tac Toe
Player x and player o alternately place their symbols on a 3x3 board, starting with x. The first player to get three symbols in a row wins, and the game is over. If all nine squares are full and no player has three symbols in a row, the game ends in a tie.

3 Tic Tac Toe Analyser
Summary: write functions for analysing the game of tic-tac-toe inside a C++ program called tttanalyzer.cpp, and make a tally of all possible games.

3.1 String-representation tttresult
Write a function with the following signature:

char tttresult(string tttboard);
The string tttboard has nine characters representing the current situation in a game of tic tac toe:

x represents x
o represents o
# represents an unplayed space
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
3.6 Program structure
Your program will be tested as follows:

cpplint and astyle will be run on it.
it will be compiled and run, to check for the proper tallies
the following line and everything after it
// MAIN
will be replaced by my own main(), which will check the proper operation of the three functions defined above.

3.7 Example starting file
Here is an example starting file: tttanalyzer_original.cpp

4 Hints and suggestions
4.1 Using map
You can use map to make the tally. Here is some partial code to illustrate:

string keys ="xotic";
map <char,int> tally;

for each board:  // this is pseudo-code, not C++
   result = tttresult(board);
   tally[result] += 1;
4.2 All the boards
What are all the ttt boards?

Here are the first few:

#########
########o
########x
#######o#
#######oo
#######ox
...
xxxxxxxxx
Compare this pattern to the 3-digit binary numbers:

000
001
010
011
100
101
110
111
Think about what convertbase does.

5 Downloads
5.1 Move class
Download movedef.h which defines the Move class

5.2 Checker
The completed checker is available here:

tttanalyzer_checker.py
Use it by typing

python tttanalyzer_checker.py
in the directory that has your programs in it.

6 Grading Scheme
Out of 100 total points, the grade is determined as follows:

40 points for passing the specifications of tttresult(string)
20 points for passing the specifications of tttresult(vector)
20 points for passing the specifications of get_all_boards()
10 points for program brevity (penalty for longer than 453 lines + words, not counting comments)
5 points for astyle (% file unchanged by astyle)
5 points for cpplint, -1 deduction for each problem
