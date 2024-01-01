#include <iostream>   //Input Output library
#include<ctime>       //Time library
#include<vector>      //Vector library 
using namespace std; 


int word_guess();         //User defined function for word guessing game
int sum_game();           //User defined function for sum game
int number_guess();       //User defined function for number guessing game
void display_status(vector <char> incorrect, string answer );        //User defined function for displaying hangman
void end_game(string answer, string codeword);               //User defined function for end of game
string generateRandomword();                  //User defined function for generating random words



int main () { 
    int a,b;           //variable initialization
    char choice;    
  
  //Do-While loop for repetition of code until user choose to exit
    do{
   cout<<"=======================\n";
   cout<<"Welcome to Hangman game.\n";
   cout<<"=======================\n";

    //Menu for selecting game
   cout<<"Please choose a module which you want to play. "<<endl;
   cout<<"1. Random Number Guessing game.\n2. Addition. \n3. Guess a Random Word. \n4. Exit.\n"<<endl;
   cin>>a;   //User choice

   //Switch statements for executing game according to user choice
      switch (a)
      {
        //Case 1 for number guessing game
      case 1:
         number_guess();
         break;
         //Case 2 for Sum game
      case 2:
         sum_game();
         break;
         //Case 3 for word guessing game
      case 3:
         word_guess();
         break;
         //exit game
      case 4:
         return 0;;
         break;
      
      default:
         break;
      } 
      //Asking for user choice to continue
      cout<<"Do you want to play it again? (y=yes, n=no): "; cin>>choice;  }while(choice=='y');   
    

    return 0;
}
//Function prototype for generating random words
string generateRandomword()
{
      vector<string> wordList = {        //Word list
        "page",
        "hangman",
        "computer",
        "bottel",
        "umbrella",
        "phone",
        "challenge",
        "solution",
        "curtain",
        "software",
        "shirt",
        "window",
        "lion",
        "mouse",
        "keyboard",
        "laptop",
        "brush",
        "pasta",
        "function",
        "helicopter"
};
// Seed the random number generator with the current time
     srand((time(0)));

    // Generate a random index within the bounds of the wordList vector
    int randomIndex = rand() % wordList.size();

    // Return the randomly selected word
    return wordList[randomIndex];}   
    //Function prototype for ending game
void end_game(string answer, string codeword)
{
 if(answer==codeword)     //Condition for Game win
 {
   cout<<"\n\nHooray! You saved the person from being hanged.\n"<<endl;
   cout<<"Congratulations.\n";
 }
else                      //Lose game
{
   cout<<"\n\nOh no! The person is being hanged.\n\n";
   cout<<"Better luck nex time.\n\n";
}
}
//Fuction prototype for displaying incorrect answer
void display_status(vector <char> incorrect, string answer )
{
  cout<<"Incorrect guesses: \n";
  for(int i=0; i<incorrect.size(); i++)
  {
    cout<<incorrect[i]<<" ";
  }

  cout<<"\ncodeword: \n";
  for(int i=0; i<answer.length();i++)
  {
   cout<<answer[i]<<" ";
  }

}
void display_misses(int misses)
{
  if(misses==0)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==1)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==2)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<"  |   | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==3)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<" /|   | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==4)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<" /|\\  | \n";
    cout<<"      | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==5)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<" /|\\  | \n";
    cout<<" /    | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }
  else if(misses==6)
  {
    cout<<"  +---+ \n";
    cout<<"  |   | \n";
    cout<<"  O   | \n";
    cout<<" /|\\  | \n";
    cout<<" / \\  | \n";
    cout<<"      | \n";
    cout<<" ========= \n";
  }

}
//Function prototype for word guessing words 
int word_guess()
{   
    string codeword = generateRandomword();   //random word generation
    string answer(codeword.length(), '_');    
    int misses=0;
    char letter;
    bool guess=false;
    vector<char> incorrect;
    while(answer!=codeword && misses<6)
    {
      display_misses(misses);
      display_status(incorrect, answer);
      cout<<"\n\nPlease enter your guess: ";
      cin>>letter;
      for(int i=0; i<codeword.length(); i++)
      {
         if(letter==codeword[i])
         {
            answer[i]=letter;
            guess = true;
         }

      }
      if(guess)
      {
         cout<<"\nCorrect!\n";
      }
      else
      {
         cout<<"\nIncorrrect! Another portion of the person has been drawn."; 
         incorrect.push_back(letter);
         misses++;
      }
      guess=false;
     
    }

   end_game(answer , codeword);


}
//Function prototype for sum game
int sum_game()
    
    { 
    int a,b ,c,count=0,answer;
    int misses=0, correct=0;
    cout<<"\n\nWelcome to the sum game. \n\nHere you will be provided with two numbers and you have to calculate their sum mentally.\n\n ";
    cout<<"If you guessed 6 incorrect in 15 turns, your friend will get hung.\n\n ";
    cout<<"if you got less than 6 incorrect in 15 turns, You will save your friend. \n\n";
   
    while(count<12 && misses!=7)
    {    display_misses(misses);
      
       srand(time(0));
         a=rand()%100+1;
         b=rand()%100+1;
         c=a+b;
      cout<<"Enter sum of "<<a<<" + "<<b<<" = ";  
      cin>>answer;
      if(answer==c){cout<<endl<<"Your answer is correct ! "<<endl; correct++;}
      else{cout<<"Your answer is incorrect "; misses++;}
      cout<<endl<<"\nCorrect answers till now: "<<correct<<endl;
      cout<<endl<<"\nincorrect answers till now: "<<misses<<endl<<endl;
      count++;
    }
    if(misses<=6){cout<<"\n\nYou won the game! and saved the person from being hanged. \n"<<endl<<"\n\n Congratulations! \n\n";}
    else{cout<<"\n\nYou loosed! The person is being hanged. \n\n"<<endl<<"\nBetter luck next time\n"<<endl;}
    return 0;
    }
    //function protype for number guessing game
int number_guess()
{
  int a,b=0,c;
    srand(time(0));
  c= (rand()%100)+1;

  while (b<4)
  {  display_misses(b);
    cout<<"Enter the guess (1-100):  ";
    cin>>a;
     if (a == c) {
        cout << "YOU GUESSED IT CORRECT. THE NUMBER WAS: " << c << endl;
        return 0;
    }

    int difference = abs(a - c);

    if (difference <= 5 && difference != 0) {
        cout << "\n\nYou are incredibly close to the guessed number!" << endl << endl;
    } else if (difference <= 10) {
        cout << "\n\nYou are very close to the guessed number!" << endl << endl;
    } else if (difference <= 15) {
        cout << "\n\nYou are quite close to the guessed number." << endl << endl;
    } else if (difference <= 20) {
        cout << "\n\nYou are a bit far from the guessed number." << endl << endl;
    } else if (difference <= 30) {
        cout << "\n\nYou are somewhat far from the guessed number." << endl << endl;
    } else if (difference <= 50) {
        cout << "\n\nYou are quite far from the guessed number." << endl << endl;
    } else if (difference <= 70) {
        cout << "\n\nYou are very far from the guessed number." << endl << endl;
    } else if (difference <= 90) {
        cout << "\n\nYou are extremely far from the guessed number." << endl << endl;
    } else {
        cout << "\n\nYou are unbelievably far from the guessed number!" << endl << endl;
    }
    b++;
  }
  if(c%2==0){ cout<<endl<<"Hint:\n Number is even\n"<<endl;}
  else cout<<"Hint:\nNumber is odd\n"<<endl;
  b=3;
   while (b<=6)
  { display_misses(b);
 cout<<"Enter the guess (1-100):  ";
    cin>>a;
   if (a == c) {
        cout << "YOU GUESSED IT CORRECT. THE NUMBER WAS: " << c << endl;
        return 0;
    }

    int difference = abs(a - c);

    if (difference <= 5 && difference != 0) {
        cout << "\n\nYou are incredibly close to the guessed number!" << endl << endl;
    } else if (difference <= 10) {
        cout << "\n\nYou are very close to the guessed number!" << endl << endl;
    } else if (difference <= 15) {
        cout << "\n\nYou are quite close to the guessed number." << endl << endl;
    } else if (difference <= 20) {
        cout << "\n\nYou are a bit far from the guessed number." << endl << endl;
    } else if (difference <= 30) {
        cout << "\n\nYou are somewhat far from the guessed number." << endl << endl;
    } else if (difference <= 50) {
        cout << "\n\nYou are quite far from the guessed number." << endl << endl;
    } else if (difference <= 70) {
        cout << "\n\nYou are very far from the guessed number." << endl << endl;
    } else if (difference <= 90) {
        cout << "\n\nYou are extremely far from the guessed number." << endl << endl;
    } else {
        cout << "\n\nYou are unbelievably far from the guessed number!" << endl << endl;
    }
    b++;
   
  }
  cout<<"You failed! "<<endl<<"number was: "<<c;
  return 0;
  }
