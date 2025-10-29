#include <stdio.h>
#include <cs50.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>

char Bletter[] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
char Sletter[] = {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'};



int smolletter(char smol);
int bigletter(char big);
bool only_digits(string s);
char rotate(char c, int n);
string ptext;
string ctext;

int main (int argc, string argv[]){ 
    if(argc == 2){
        if(only_digits(argv[1])){
            ptext = get_string("plaintext:  ");
            printf("ciphertext: ");
            for(int i = 0; i < strlen(ptext); i++){ //loop a number of times based on the length of ptext
                printf("%c", rotate(ptext[i], atoi(argv[1])));
            }
            printf("\n");
        }
        else{
            printf("Usage: ./caesar key\n");
            return 1;
        }
    }
    else{
        printf("Usage: ./caesar key\n");
        return 1;
    }
}

int bigletter(char big){    //checks if the char matches a letter in the array. If it matches, it returns the 'alphabetical index'
    for(int i = 0; i < strlen(Bletter); i++){
        if(big == Bletter[i]){
            return i;
        }
    }
    return 0;
}

int smolletter(char smol){  //checks if the char matches a letter in the array. If it matches, it returns the 'alphabetical index'
    for(int i = 0; i < strlen(Sletter); i++){
        if(smol == Sletter[i]){
            return i;
        }
    }
    return 0;
}

bool only_digits(string s){
    for(int i = 0; i < strlen(s); i++){
        if(isalpha(s[i])){  //if a function returned a value, like false, the function will stop and not read the 'return true' outside the loop
            return false;   //if s contains a non digit character, it will return false
        }
    }
    return true;
}

char rotate(char c, int n){
    int s;
    if(islower(c)){
        s = (smolletter(c) + n) % 26;
        // s = (int)c + n % 26;
        //s = (7 + n) % 26;
        return Sletter[s];
    }
    else if(isupper(c)){
        s = (bigletter(c) + n) % 26;
        // s = (int)c + n % 26;
        return Bletter[s];
    }
    else{
        return c;
    }
}
