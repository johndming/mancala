#include <iostream>
#include <cmath>
#include <ctime>
#include <string>
#include <iomanip>
#include <vector>
#include <array>

using namespace std;

// Constant Variable for Bead Array.
const int Bead_Array_Size = 14;

// This function initializes the player's starting bins.
void startingArray(int beadArray[Bead_Array_Size]) 
{
	// Both players start off with 4 beads in their respective side bins.
	for (int i = 0; i < Bead_Array_Size; ++i) 
	{
		beadArray[i] = 4; 
	}

	beadArray[6] = 0; // Player 1's end bin.
	beadArray[13] = 0; // Player 2's end bin.
}

// This function allows for one to print the bead array for debugging purposes.
void printArray(int beadArray[Bead_Array_Size])
{
	// This loop prints out only the numbers of of the bead array and their respective bins. 
	for (int i = 0; i < Bead_Array_Size; ++i)
	{
		cout << " " << beadArray[i];
	}
	cout << endl; 
}

// Generating the game board part 1.
void makeDottedLine() 
{
	// This generates a line of stars, which can be used to generate the game board.
	for (int i = 0; i < 8; ++i) 
	{
		cout << "*";
		for (int z = 0; z < 6; ++z)
		{
			cout << " ";
		}
	}
	cout << "*"; 
}

// Generating the game board part 2.
int makeSolidLine(int num) 
{
	// This generates a line of stars, which can be used to generate the game board.
	// The stars are populated based on the number input for "num" in main. 
	for (int i = 0; i < num; ++i)
	{
		cout << "*"; 
	}
	return num;
}

// This generates player 1's side bins and end bin.
void showTopBins(int beadArray[Bead_Array_Size])
{
	cout << "*";
	cout << setw(7) << "*";

	// This puts the beads in the correct bins without labels. 
	for (int i = 0; i < 6; i++) 
	{
		cout << setw(4) << beadArray[i];
		cout << setw(3) << "*";
	}
	cout << setw(7) << "*";
}

// This generates player 2's side bins and end bin.
void showBottomBins(int beadArray[Bead_Array_Size])
{
	cout << "*";

	// This puts the beads in the correct bins without labels. 
	for (int i = 12; i >= 7; --i)
	{
		cout << setw(4) << beadArray[i];
		cout << setw(3) << "*";
	}
}

// This function labels Player 1's bins.
void showTopRowNumbers()
{
	cout << "*"; 
	cout << setw(7) << "*"; 

	// This is the loop that labels the bins.
	for (int i = 0; i < 6; i++) 
	{
		cout << setw(4) << i; 
		cout << setw(3) << "*"; 
	}
	cout << setw(7) << "*";
}

// This function labels Player 2's bins.
void showBottomRowNumbers()
{
	cout << "*";
	cout << setw(7) << "*"; 

	// This is the loop that labels the bins.
	for (int i = 12; i >= 7; --i) 
	{
		cout << setw(4) << i; 
		cout << setw(3) << "*";
	}
	cout << setw(7) << "*";
}

// This function checks to see if the game is over. 
int gameOverCheck(int beadArray[Bead_Array_Size])
{	// Variable used for player 1 side bins.
	int player1bins = beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5]; 

	// Variable used for player 2 side bins.
	int player2bins = beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12];
	
	// Of player 1's bins are equal to zero.
	if (player1bins == 0)
	{
		// Adds beads left in player 2's side bins to player 1's end bin.
		beadArray[6] = beadArray[6] + player2bins;

		// Sets all of player 2's side bins equal to zero. 
		beadArray[7] = 0;  beadArray[8] = 0;  beadArray[9] = 0;  beadArray[10] = 0;  beadArray[11] = 0;  beadArray[12] = 0; //sets bottom bins to zero

		// If player 2 has more beads in their end bin the function returns 2.
		if (beadArray[13] > beadArray[6])
		{
			return 2;
		}

		// if they have equal amount of beads in their end bins the function returns zero.
		else if (beadArray[6] == beadArray[13])
		{
			return 0;
		}

		// otherwise the function returns 1.
		return 1; 
	}

	// Of player 2's bins are equal to zero.
	if (player2bins == 0)
	{
		// Adds beads left in player 1's side bins to player 2's end bin.
		beadArray[13] = beadArray[13] + player1bins;

		// Sets all of player 1's side bins equal to zero. 
		beadArray[0] = 0; beadArray[1] = 0; beadArray[2] = 0; beadArray[3] = 0; beadArray[4] = 0; beadArray[5] = 0;

		// If player 1 has more beads in their end bin the function returns 1.
		if (beadArray[6] > beadArray[13])
		{
			return 1;
		}

		// if they have equal amount of beads in their end bins the function returns zero.
		else if (beadArray[6] == beadArray[13])
		{
			return 0;
		}

		// otherwise the function returns 2.
		return 2;
	}
	else
	{
		// Returns -1 until a player wins. 
		return -1; 
	}
}


// This function Generates the game board.
void showBoard(int beadArray[Bead_Array_Size]) 
{
	makeSolidLine(57);
	cout << endl;
	makeDottedLine();
	cout << endl;
	showTopRowNumbers();
	cout << endl;
	makeDottedLine();
	cout << endl;
	showTopBins(beadArray);
	cout << endl;
	makeDottedLine();
	cout << endl;

	// This outputs the labels for the player's bins. // 
	cout << "*";                                      //
	cout << "  13  ";                                 // 
	makeSolidLine(43);                                //
	cout << "   6  *";                                //
	// This outputs the labels for the player's bins. //

	cout << endl;
	makeDottedLine();
	cout << endl;
	showBottomRowNumbers();
	cout << endl;
	makeDottedLine();
	cout << endl;

	// Keeps board from warping by larger bead numbers and displays beads in end bins.
	cout << "*" << setw(3);
	cout << beadArray[13] << setw(4); 
	showBottomBins(beadArray);
	cout << setw(3);
	cout << beadArray[6] << setw(4)<< "*";
	// Keeps board from warping by larger bead numbers and displays beads in end bins.

	cout << endl;
	makeDottedLine();
	cout << endl;
	makeSolidLine(57);
	cout << endl;
}

// This function allows the player to pick a bin based on the games rules. 
void getStartingBin(int beadArray[Bead_Array_Size], int playerNum, int& playerChoice)
{
	int validMove = false;
	cout << "Player " << playerNum << " choose a bin: ";

	// Loops until "validMove" is true. 
	while (validMove == false) 
	{
		// Player inputs bin choice.
		cin >> playerChoice;
		
		// "validMove" is set to true to break loop unless if statements are true.
		validMove = true;

		// player 1's rules.
		if (playerNum == 1)  
		{


			// These if statements keep the player from choosing bins that are equal to zero.
			if (playerChoice == 0)
			{

				if (beadArray[0] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 1)
			{
				if (beadArray[1] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 2)
			{
				if (beadArray[2] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 3)
			{
				if (beadArray[3] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 4)
			{
				if (beadArray[4] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 5)
			{
				if (beadArray[5] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}

			// This keeps the player from picking their end bin.
			if (playerChoice == 6)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}

			//These if statements keep the player from picking player 2's bins. 
			if (playerChoice == 7)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 8)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 9)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 10)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 11)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 12)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 13)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}

			// This keeps the player from choosing numbers that don't exist within the game board. 
			if (playerChoice > 13)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}

			// This keeps the player from choosing negative numbers. 
			if (playerChoice < 0)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
		}

		// Pretty much the same as player 1, except swapped with player 2's bins.
		if (playerNum == 2)
		{
			if (playerChoice == 0)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 1)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 2)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 3)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 4)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 5)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 6)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice == 7)
			{
				if (beadArray[7] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 8)
			{
				if (beadArray[8] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 9)
			{
				if (beadArray[9] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 10)
			{
				if (beadArray[10] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 11)
			{
				if (beadArray[11] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 12)
			{
				if (beadArray[12] == 0)
				{
					validMove = false;
					cout << "Invalid. Choose again: ";
				}
			}
			if (playerChoice == 13)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice > 13)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
			if (playerChoice < 0)
			{
				validMove = false;
				cout << "Invalid. Choose again: ";
			}
		}
	}
}

// This is meat of the game. This moves the beads around and various other game tasks. 
void dropBeads(int beadArray[Bead_Array_Size], int playerNum) //sets bead array and player number variables.
{
	int playerChoice; // This represents the players choice.
	int gameHand = 0; // This is the magical game hand that "moves" the beads.
	int playerTurn = true; // This sets the player's turn to true.
	int player1bins = beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5]; // variable for top bins.
	int player2bins = beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12]; // variable for bottom bins.

	gameOverCheck(beadArray); // checks if the game is over. 

	getStartingBin(beadArray, playerNum, playerChoice); // I call this so that it checks to see if the player choice is valid.
	gameHand = beadArray[playerChoice]; // When the player chooses a bin, the "game hand" grabs the beads from that bin.
	beadArray[playerChoice] = 0; // Sets the bin the player chooses to 0.
	showBoard(beadArray); // Prints out the board so the player can see this happening. 
	system("pause"); // Pauses so its easier for the player to process.
	
	// This adds 1 to player 2's bins and resets the players choice to zero.
	if (playerChoice == 12)
	{
		beadArray[13]++;
		gameHand--;
		showBoard(beadArray);
		system("pause");
		
		// Keeps bin zero from getting beads that don't exist in the game hand.
		if (gameHand > 0)
		{ 
		playerChoice = 0;
		beadArray[0]++;
		showBoard(beadArray); 
		system("pause"); 
		}
	}

	// While the player turn is set to true. This happens. 
	while (playerTurn == true) 
	{
		if (playerNum == 1) // If the player number is 1. This happens.
		{
			if (gameHand > 0) // If game hand is > 0. This happens this if statment is was keeps the beads moving, most of the time.
			{
				playerChoice++; // adds 1 to player choice.
				gameHand--; // subtracts 1 from game hand.
				beadArray[playerChoice]++; // adds 1 to the bead array. 
				showBoard(beadArray);
				system("pause");

				// This helps to end the game if player 1's bins equal zero.
				if (beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5] == 0)
				{
					beadArray[6] = beadArray[6] + gameHand + player2bins;
					showBoard(beadArray);
					system("pause");

					beadArray[7] = 0; beadArray[8] = 0; beadArray[9] = 0; beadArray[10] = 0; beadArray[11] = 0; beadArray[12] = 0;
					playerTurn = false;
					showBoard(beadArray);
					system("pause");
				}
			}
			if (gameHand == 0 && beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5] != 0) // if game hand == 0. This happens.
			{
				if (beadArray[playerChoice] > 0) // if the bead array the player chooses is greater than 0. 
				{
					if (beadArray[playerChoice] == 1) // Keeps weird things from happening. like magic beads that don't exist from apearing into bins. 
					{
						if (playerChoice > 6 || playerChoice < 6)
						{
							gameOverCheck(beadArray);
							playerTurn = false;
							continue;
						}
						else if (playerChoice == 6 && beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5] > 0)
						{
							getStartingBin(beadArray, playerNum, playerChoice); // I call this so that it checks to see if the player choice is valid.
							gameHand = beadArray[playerChoice]; // When the player chooses the game hand grabs the beads from their bin choice.
							beadArray[playerChoice] = 0; // Sets the bin the player chooses to 0
							showBoard(beadArray); 
							system("pause"); 
						}
					}
					else if (playerChoice != 6)
					{
						gameHand = beadArray[playerChoice]; // When the player chooses the game hand grabs the beads from their bin choice.
						beadArray[playerChoice] = 0; // Sets the bin the player chooses to 0
						showBoard(beadArray);
						system("pause");
					}
					else if (playerChoice == 6)
					{
						cout << "Player 1's final bead landed in their end bin.\n"; 
						getStartingBin(beadArray, playerNum, playerChoice); // Has the player choose another bin.
						gameHand = beadArray[playerChoice];
						beadArray[playerChoice] = 0;
						showBoard(beadArray);  
						system("pause"); 
					}
				}

				// ends the turn if the final bead drops into an empty bin. 
				else if (beadArray[playerChoice] == 0 && playerChoice != 6)
				{

					gameOverCheck(beadArray);

					playerTurn = false;

				}

				// This ends their turn if true and helps end the game.
				if (playerChoice <= 6 && beadArray[playerChoice] == 0 && gameHand == 0)
				{
					if (beadArray[0] + beadArray[1] + beadArray[2] + beadArray[3] + beadArray[4] + beadArray[5] == 0)
					{
						beadArray[6] = beadArray[6] + gameHand;
						gameOverCheck(beadArray);
						playerTurn = false;
						continue;
					}
					if (beadArray[playerChoice] == 0)
					{

						getStartingBin(beadArray, playerNum, playerChoice); 
						gameHand = beadArray[playerChoice]; 
						beadArray[playerChoice] = 0;
						showBoard(beadArray); 
						system("pause"); 
					}
				}
			}

			// keeps player 1 from placing beads in their opponents bin. 
			if (playerChoice >= 12)
			{
				playerChoice = 0;
				beadArray[0]++;
				gameHand--;
				showBoard(beadArray);
				system("pause");
			}
		}

		// This is the if statement for player 2, it's mostly the same as player 1. I will only comment on the parts that are very different. 
		if (playerNum == 2)
		{
			if (beadArray[13] < 0)
			{
				beadArray[13] = beadArray[13] * 0;
			}
			if (gameHand > 0)
			{
				playerChoice++;
				gameHand--;
				beadArray[playerChoice]++;
				showBoard(beadArray);
				system("pause");
			}
			if (beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12] == 0)
			{
				beadArray[13] = beadArray[13] + gameHand + player1bins;
				showBoard(beadArray);
				system("pause");
				beadArray[0] = 0; beadArray[1] = 0; beadArray[2] = 0; beadArray[3] = 0; beadArray[4] = 0; beadArray[5] = 0;
				showBoard(beadArray);
				system("pause");
				gameOverCheck(beadArray);
				playerTurn = false;
			}

			// if game hand == 0. This happens only if the side bins do not equal 0. 
			if (gameHand == 0 && beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12] != 0) 
			{
				if (beadArray[playerChoice] > 0 && playerChoice != 6) 
				{
					if (beadArray[playerChoice] == 1)
					{
						if (playerChoice > 6 || playerChoice < 6)
						{
							gameOverCheck(beadArray);
							playerTurn = false;
							continue;
						}
					}
					else if (beadArray[playerChoice] > 1)
					{
						gameHand = beadArray[playerChoice];
						beadArray[playerChoice] = 0; 
						showBoard(beadArray);
						system("pause");
					}
				}
				else if (beadArray[playerChoice] == 0)
				{
					if (playerChoice < 6)
					{
						gameOverCheck(beadArray);
						playerTurn = false;
					}
				}
				if (playerChoice == 13)
				{
					getStartingBin(beadArray, playerNum, playerChoice);
					gameHand = beadArray[playerChoice]; 
					beadArray[playerChoice] = 0; 
					showBoard(beadArray); 
					system("pause");
				}
			}

			// This keeps player 2 from helping their oppenent win. It skips over bin 6.
			if (playerChoice == 5) // if bin 5, then player choice is now 7 and adds and subtracts according to the bin and game hand. 
			{
				playerChoice = 7;
				beadArray[7]++;
				gameHand--;
				gameHand--;
				if (gameHand < 0)
				{
					gameHand = gameHand * 0;
				}
				showBoard(beadArray);
				system("pause");
			}

			// This keeps player 2 from leaving the game board in an endless stream of numbers. 
			if (playerChoice >= 12) 
			{
				playerChoice = 13;
				if (playerChoice == 13)
				{
					if (gameHand == 0 && beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12] != 0)
					{
						getStartingBin(beadArray, playerNum, playerChoice); 
						gameHand = beadArray[playerChoice];
						beadArray[playerChoice] = 0;
						showBoard(beadArray); 
						system("pause"); 
						if (playerChoice != 12)
						{
							continue; 
						}
					}
					if (gameHand > 0)
					{
						playerChoice = 0;
						if (playerChoice == 0)
						{
							beadArray[13]++;
						}
						beadArray[playerChoice]++;
						gameHand--;
					}
					showBoard(beadArray);
					system("pause"); 
				}
				if (gameHand < 0)
				{
					gameHand = gameHand * 0;
				}
				if (gameHand == 0 && beadArray[7] + beadArray[8] + beadArray[9] + beadArray[10] + beadArray[11] + beadArray[12] != 0)
				{
					if (playerChoice == 13)
					{
						getStartingBin(beadArray, playerNum, playerChoice);
						gameHand = beadArray[playerChoice];
						beadArray[playerChoice] = 0;
						showBoard(beadArray);
						system("pause");
					}
					else if (playerChoice < 6 && beadArray[playerChoice] == 0)
					{
						gameOverCheck(beadArray);
						playerTurn = false;
					}
				}
			}
		}
	}
}

// Main allows for the game to be played in full.
int main()
{
	
	// Allows for me to call the bead Array.
	int beadArray[Bead_Array_Size];

	// Sets a variable for the player number.
	int currentPlayerNumber = 0;

	// Initialized the beads for the game board.
	startingArray(beadArray);

	// Welcomes the user to the game. 
	cout << "Welcome to Mancala!\n"; 
	system("pause");
	cout << "\nGame Rules:\n";
	cout << "Player 1 picks first. Player 1 can only pick bins 0-5 and Player 2 can only pick bins 7-12.\n";
	cout << "The player can only pick a bin that has 1 or more beads in it. Once the player picks a bin\n";
	cout << "the beads in that bin will be distributed across all the bins including that players end bin.\n";
	cout << "If the last bead lands in a bin with 0 beads the turn ends. If the last bead lands in that\n"; 
	cout << "players end bin then they get to choose gain. Once one of the players empties all of their\n";
	cout << "side bins the game is over. Whoever has the most beads in their end bin wins. Good Luck!\n";
	system("pause");
	cout << "\n"; 


	// This is done while the game isn't over.
	do
	{
		// Checks if the game is over. 
		gameOverCheck(beadArray);
		
		//Shows the game board.
		showBoard(beadArray);

		//Allows for the user to manipulate the beads.
		dropBeads(beadArray, 1);
		gameOverCheck(beadArray);

		// breaks while loop if no equal to -1
		if (gameOverCheck(beadArray) != -1)
		{
			break; 
		}
		dropBeads(beadArray, 2);
		gameOverCheck(beadArray);

		// breaks while loop if no equal to -1
		if (gameOverCheck(beadArray) != -1)
		{
			break;
		}
	} while (gameOverCheck(beadArray) == -1);


	if (gameOverCheck(beadArray) != -1)
	{
		if (gameOverCheck(beadArray) == 2) // Player 2 wins
		{
			currentPlayerNumber = 2;
		}
		if (gameOverCheck(beadArray) == 0) // Players tie.
		{
			cout << "It's a Draw! \n";
		}
		if (gameOverCheck(beadArray) == 1) // Player 1 wins. 
		{
			currentPlayerNumber = 1;
		}
	}

	cout << "Congrats, player " << currentPlayerNumber << ", you won!\n";
	system("pause"); 
}
