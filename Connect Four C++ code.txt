


// By Amshuman Sashi

/*
Program  to  play  the  game  CONNECT FOUR
The game board consists of 6 rows and 7 columns
The player 1 marks ' X ' and 2 marks ‘O ' which indicates the block selected by the player.
*/

/*
Player   who   connects   4   blocks   first horizontally, vertically or diagonally wins the game.
This data file holds the details of those who played so far.
*/

//The Program starts
//header files and pre-processor statements
#include <iostream.h>
#include <fstream.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
#include <conio.h>
#include <dos.h>
#define BOARD_ROWS 6
#define BOARD_COLS 7
class player
{
	char pname[20];
	int pscore;
		public:
		void getname(char a[])
		{
			strcpy(pname, a);
		}

		void getscore(int a)
		{
			pscore = a;
		}

		char *returnname()
		{
			return pname;
		}

		int returnscore()
		{
			return pscore;
		}
};

int checkname(char *k);
void dispfile(void);
void scoreboard(char[], char[], int, int);
void printBoard(char *board);
int takeTurn(char *board, int player, const char *);
int checkWin(char *board);
int checkFour(char *board, int, int, int, int);
int horizontalCheck(char *board);
int verticalCheck(char *board);
int diagonalCheck(char *board);
void delay()
{
	for (int ii = 0; ii < 10000; ii++)
		for (int jj = 0; jj < 10000; jj++);
}

void animation(char *g, int i)
{
	for (int kk = 0; kk < i; kk++)
	{
		for (int ll = 0; ll < kk; ll++)
			cout << " ";
		cout << g;
		delay();
		if (kk < i - 1)
			clrscr();
	}
	delay();
}

void thank()
{
	for (int kk = 0; kk < 185; kk++)
	{
		cout << "\n\n\n\n\n\n\n\n";
		for (int ll = 0; ll < kk; ll++)
			cout << " ";
		cout << " THANK YOU FOR PLAYING ";
		delay();
		if (kk < 184)
			clrscr();
	}
	delay();
}

void filedata(player p1, player p2)
/*{
	player p;
	int f1 = 0, f2 = 0;
	ifstream fptr;
	fptr.open("SKEAM.dat", ios::binary);
	ofstream off("rename.dat", ios::binary | ios::app);
if (checkname(p1.returnname()) || checkname(p2.returnname()))
	{
		while (fptr.read((char*) &p, sizeof(p)))
		{
	if (strcmpi(p.returnname(), p1.returnname()) == 0)
			{
				p.updatescore(p1.returnscore());
				f1 = 1;
			}
			else if (strcmpi(p.returnname(), p2.returnname()) == 0)
			{
				p.updatescore(p2.returnscore());
				f2 = 1;
			}

			off.write((char*) &p, sizeof(p));
		}
	}

	if (!f1)
		off.write((char*) &p1, sizeof(p1));
	if (!f2)
		off.write((char*) &p2, sizeof(p2));
	remove("SKEAM.dat");
	rename("rename.dat", "SKEAM.dat");
	fptr.close();
	off.close();
}*/

float game()
{
	player p1, p2;
	char f1[20], f2[20];
	int score1 = 0;
	int score2 = 0;
	clrscr();
	//cout<<"\n\t Press any key to start the game";
	//getch();
	const char *PIECES = "XO";
	char board[BOARD_ROWS *BOARD_COLS];
	memset(board, ' ', BOARD_ROWS *BOARD_COLS);
	int turn, done = 0;
	clrscr();
	cout << "\n\n\n\t ENTER FIRST PLAYER'S NAME(X): ";
	gets(f1);
	p1.getname(f1);
	clrscr();
	cout << "\n\n\n\t ENTER SECOND PLAYER'S NAME(O): ";
	gets(f2);
	p2.getname(f2);
	clrscr();
	cout << "\n\n\n\t" << f1 << " and " << f2 << " are the players ";
	if (checkname(f1))
		cout << "\n\n\n\t" << f1 << " HAS PLAYED THIS GAME";
	if (checkname(f2))
		cout << "\n\n\n\t" << f2 << " HAS PLAYED THIS GAME";
	cout << "\n\n\n\n\t PRESS ANY KEY TO START THE GAME ...... ";
	getch();
	clrscr();
	for (turn = 0; turn < BOARD_ROWS *BOARD_COLS && !done; turn++)
	{
		printBoard(board);
		while (!takeTurn(board, turn % 2, PIECES))
		{
			printBoard(board);
			puts("**Column  full !!**\n");
		}

		done = checkWin(board);
	}

	clrscr();
	printBoard(board);
	if (turn == BOARD_ROWS *BOARD_COLS && !done)
	{
		puts("it's a tie!");
		score1 = 1;
		score2 = 1;
		cout << "\n\n" << score1 << "  " << score2;
		cout << "\n\n press any key to continue";
		getch();
	}
	else
	{
		turn--;
		cout << "\n WOW!!!!!. ";
		cout << "Player  " << (turn % 2) + 1 << " (" << PIECES[(turn % 2)] << ")  WINS!\n" << endl;
		if ((turn % 2 + 1) == 1)
		{
			score1 = 1;
			cout << "\n" << f1 << " WINS\n";
		}
		else if ((turn % 2 + 1) == 2)
		{
			score2 = 1;
			cout << "\n" << f2 << " WINS\n";
		}
	}

	cout << "\n PRESS ANY KEY ";
	getch();
	p1.getscore(score1);
	p2.getscore(score2);
	filedata(p1, p2);	//INTO THE FILE
	clrscr();
	scoreboard(f1, f2, score1, score2);
	getch();
	clrscr();
	dispfile();
	return 0;
}

int main()
{
	i: 
	clrscr();
	char lop[] = "*****CONNECT FOUR *****";
	animation(lop, 15);
	cout << endl << "    ___________________________________________\n\n\n";
	delay();
	cout << "\t\t 1. Play Game \n\n\t ";
	delay();
	cout << "\t 2. Instruction \n\n\t ";
	delay();
	cout << "\t 3. Scoreboard \n\n\t ";
	delay();
	cout << "\t 4. Exit \n\n\t";
	delay();
	cout << "\t Choice : ";
	int a = 0;
	cin >> a;
	switch (a)
	{
		case 1:
			{
				game();
				goto i;
				break;
			}

		case 2:
			{
				clrscr();
				cout << "\n\n\t\t INSTRUCTIONS ";
	cout << endl << "    __________________ _________________________\n\n";
	cout << "\n1. The game board consists of 6 rows and 7 columns.\n\n2. The player 1 marks \' X \' and 2 marks \' O \' which \n   indicates the block selected by the player.\n\n3. Player  who  connects  4  blocks  first horizontally, \n   vertically or diagonally wins the game.";
	cout << "\n\n\n\t\t PRESS ANY KEY TO CONTINUE";
				getch();
				goto i;
				break;
			}

		case 3:
			{
				dispfile();
				goto i;
				break;
			}

		case 4:
			{
				clrscr();
				thank();
				return 0;
				break;
			}

		default:
			{
				cout << "\n\n\t Wrong entry try again";
				goto i;
			}
	}
}

void printBoard(char board[])
{
	int row, col;
	clrscr();
	puts("\n    ****CONNECT FOUR ****\n");
	for (row = 0; row < BOARD_ROWS; row++)
	{
		for (col = 0; col < BOARD_COLS; col++)
		{
		cout << " " << board[BOARD_COLS *row + col] << " |";
		}

		cout << endl;
		puts("----------------------------");
		//puts("____________________________");
	}

	puts(" 1   2   3   4   5   6   7 \n");
}

int takeTurn(char *board, int players, const char *PIECES)
{
	int row, col = 0;
	cout << "Player " << players + 1 << " (" << PIECES[players] << ") \n" << endl << " Enter number coordinate : ";
	while (1)
	{
		cin >> col;
		if (col < 1 || col > 7)
		{
			puts("number out of bounds! Try again.");
		}
		else
		{
			break;
		}
	}

	col--;
	for (row = BOARD_ROWS - 1; row >= 0; row--)
	{
		if (board[BOARD_COLS *row + col] == ' ')
		{
	board[BOARD_COLS *row + col] = PIECES[players];
			return 1;
		}
	}

	return 0;
}

int checkWin(char *board)
{
	return (horizontalCheck(board) || verticalCheck(board) || diagonalCheck(board));
}

int checkFour(char *board, int a, int b, int c, int d)
{
	return (board[a] == board[b] && board[b] == board[c] && board[c] == board[d] && board[a] != ' ');
}

int horizontalCheck(char *board)
{
	int row, col, idx;
	for (row = 0; row < BOARD_ROWS; row++)
	{
		for (col = 0; col < BOARD_COLS; col++)
		{
			idx = BOARD_COLS *row + col;
	if (checkFour(board, idx, idx + 1, idx + 2, idx + 3))
				return 1;
		}
	}

	return 0;
}

int verticalCheck(char *board)
{
	int row, col, idx;
	for (row = 0; row < BOARD_ROWS - 3; row++)
	{
		for (col = 0; col < BOARD_COLS; col++)
		{
			idx = BOARD_COLS *row + col;
	if (checkFour(board, idx, idx + BOARD_COLS, idx + 2 *BOARD_COLS, idx + 3 *BOARD_COLS))
				return 1;
		}
	}

	return 0;
}

int diagonalCheck(char *board)
{
	int row, col, idx, count = 0;
	const int DIAG_RGT = 6,
		DIAG_LFT = 8;
	for (row = 0; row < (BOARD_ROWS - 3); row++)
	{
		for (col = 0; col < BOARD_COLS; col++)
		{
			idx = BOARD_COLS *row + col;
			if (count <= 3 && checkFour(board, idx, idx + DIAG_LFT, idx + DIAG_LFT *2, idx + DIAG_LFT *3) || count >= 3 && checkFour(board, idx, idx + DIAG_RGT, idx + DIAG_RGT *2, idx + DIAG_RGT *3))
				return 1;
			count++;
		}

		count = 0;
	}

	return 0;
}

int checkname(char *k)
{
	ifstream ptrl;
	player p;
	ptrl.open("SKEAM.dat", ios::binary);
	while (ptrl.read((char*) &p, sizeof(p)))
	{
		if (!strcmpi(p.returnname(), k))
			return 1;
	}

	ptrl.close();
	return 0;
}

void dispfile()
{
	ifstream ptr;
	player p;
	clrscr();
	ptr.open("SKEAM.dat", ios::binary);
	cout << "\n\n\t\t PLAY HISTORY ";
	cout << endl << "   ___________________________________________\n\n";
	while (ptr.read((char*) &p, sizeof(p)))
	{
		cout << "\t\t";
		p.printdetails();
		delay();
		delay();
		cout << endl << endl;
	}

	cout << "\n\n\n\t\t PRESS ANY KEY TO CONTINUE";
	getch();
	ptr.close();
}

void scoreboard(char *p1, char *p2, int a, int b)
{
	cout << "\n  THE CONNECT FOUR";
	cout << "\n------------------------------------------------\n\n";
	cout << "\n" << p1 << "  " << a;
	cout << "\n" << p2 << "  " << b;
	cout << "\n\n    press any key";
	getch();
}

