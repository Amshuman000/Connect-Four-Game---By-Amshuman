# Connect-Four-Game---By-Amshuman

This game has been made for C++ Turbo version<br />
Connect Four is a 2-player connection game in which the players take turns selecting blocks which are marked ‘ X ’ and ‘ O ’ respectively. The players can select a column by entering its number. If any number is repeated the block in the respective column but the row just above the previous one can be selected. The objective of the game is to be first to form a horizontal, vertical, or diagonal line of four blocks, while preventing the opponent from doing the same.

FUNCTIONS USED<br />
•	void scoreboard(char[],char[],int,int)                                         
 To display the final score of the players.<br /><br />

•	void dispfile(void)                                                                           
To display the data file contents<br /><br />

•	void checkname(char[])                                                                 
To check whether a player has already played this game before<br />

•	void printBoard(char* board)                                                        
To display the entire Game Board<br />

•	int takeTurn(char* board, int player, const char* )                  
Allows the player to enter the coordinates<br />

•	int checkWin(char* board)                                                                
To select the winner<br />

•	int checkFour(char*board, int, int, int, int);
<br /><br />

Checks whether 4 nearby columns are filled<br />
•	int horizontalCheck(char*board)  <br />                                                   
To check the 4 horizontal columns are filled or not<br />

•	int verticalCheck(char*board)                                                                    
 To check the 4 vertical columns are filled or not<br />
<br />
•	int diagonalCheck(char*board) <br />                                                         
To check the four diagonal columns are filled or not<br />

•	void filedata(player p1, player p2)                                                
To accept an object of class players and update scores of old players or write details of new players into file <br />
<br />
•	void delay()      <br />                                                                                  
To create a delay during runtime<br />
<br />
•	void animation(char *g, int i)  <br />                                                       
To create an animation like effect<br />
<br />
•	void thank()   <br />                                                                                     
To print Thank You statement on exit from game <br />
<br />
•	int game()    <br />                                                                            
Contains the logic of the game<br />
<br />
