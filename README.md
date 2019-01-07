# Pig-Latin

/* Pig Latin is a game of alterations played on the English language game.
To create the Pig Latin form of an English word the initial consonant sound
is transposed to the end of the word and an ay is affixed (Ex.: "banana" would yield anana-bay).*/

#include <iostream>
#include <string>

using namespace std;

// takes a string argument and returns the pigLatin equivalent
string pigLatin(string);

int main()
{
    string mySentence;
    
    getline(cin, mySentence);
    
    mySentence = pigLatin(mySentence);
    cout << mySentence << endl;
    
    return 0;
}

string pigLatin(string word)
{
    //pigLatWord holds word translated in pig latin.
    //pigLatSentence holds entire translated sentence.
    string pigLatWord, pigLatSentence = "";
    int length = 0, index = 0;
   
    while (word[index] != '\0'){
        
        // .find returns -1 if no match is found
        if (word.find(' ', index) != -1){
            length = word.find(' ', index);
            length -= index;//length - index = the number of characters in a word
            
            pigLatWord = word.substr(index, length);
            
            pigLatWord.insert(length, "ay");
            
            //first letter is inserted at the end of the string
            pigLatWord.insert(length, 1, word[index]);
            
            // erase first letter in string
            pigLatWord.erase(0, 1);
            
            //adding one moves index from 'space' to first letter in the next word
            index += length + 1;
        }
        else{
            pigLatWord = word.substr(index);
            length = pigLatWord.length();
            pigLatWord.insert(length, "ay");
            
            pigLatWord.insert(length, 1, word[index]);
            pigLatWord.erase(0, 1);
            index = word.length();
        }

        pigLatSentence += (pigLatWord + " ");
    }
    return pigLatSentence;
    
}
