/////////////////////////////////  اضخم مشروع حتى اللحظة 11\3\2025 /////////////////////////////////
/////////////////////////////////          مدة العمل 5 ايام        /////////////////////////////////
/////////////////////////////////            Tony jabbour           /////////////////////////////////
/************************* برنامج لتحويل الرقام العشرية و الثنائية فقط *************************/
#include <iostream>
#include <cmath>
#include <string>

int decimal = 0; 
std:: string binary, x, INDEX, text;

void start(){
    using namespace std;
    cout << endl;
    cout << "           hey there! this program helps you convert between decimal and binary numbers!   " << endl;
    cout << "        ***********************************************************************************" << "\n\n";
    cout << "enter // \'dtb\' \\\\ if you want to convert a decimal number to a binary number." << endl;
    cout << "enter \\\\ \'btd\' // if you want to convert a binary number to a decimal number." << endl;
    cout << endl;
}
void print(){
    std:: cout << "but first, choose the kind of converting you want to do ( dtb / btd ) by entering it." <<std:: endl;
    std:: cout << "or you can also exit the program by entering ( x )" << std::endl;
}
void adjust(){
    while(1){
        INDEX = binary.substr(0,1);
        if(INDEX == "0"){
            binary.replace(0,1,"");
        }else{
            break;
        }
    }
}
void reverse1(){
    for(int i =0; i<(binary.size()/2); i++){
        int t = binary[i];
        binary[i] = binary[binary.size()-1-i];
        binary[binary.size()-1-i] = t;
    }
}
void reverse2(std:: string var){
    for(char n : var){
        x = (n == '0')? "1" : "0";
        binary += x;
    }
}
void calculate1(){
    while (decimal != 0){
        if(decimal % 2 == 0) x = "0";
        else                 x = "1";
        binary += x;    decimal /= 2;
    }
    reverse1();
}
void calculate2(){
    std:: string add, Mbinary;       int j = 0;

    for(int i = 0; i< 16 - binary.size(); i++){
        add += "0";
    }
    Mbinary = add + binary;     binary.clear();
    reverse2(Mbinary);
    INDEX = binary.substr(15,1);
    if(INDEX == "0") { binary.replace(15,1,"1");
    }else{
        while(INDEX != "0"){          
            binary.replace(15-j,1,"0");
            j++;
            INDEX = binary.substr(15-j,1);
        }
        binary.replace(15-j,1,"1");
    }
}
void calculate3(){
    reverse1(); 

    int X, k = 0;
    for(char n : binary){
        X = (n == '0')? 0 : 1;
        decimal += X * pow(2,k);
        k++;
    }
}
void calculate4(){
    std:: string storage;             int i = 0;

    INDEX = binary.substr(15,1);
    if(INDEX == "1") { binary.replace(15,1,"0");
    }else{ 
        while(INDEX != "1"){          
            binary.replace(15-i,1,"1");
            i++;
            INDEX = binary.substr(15-i,1);
        }
        binary.replace(15-i,1,"0");
    }
    storage = binary;            binary.clear();
    reverse2(storage);             calculate3();
    decimal = -decimal;
}
void check(){
    bool condition = true;

    while(condition){
        int Condition = 1;
        std:: cin >> binary;
        for(char N : binary){
            if(!(N == '1'|| N == '0')){
                std:: cout << "are you kidding me? does that look binary to you? ";
                std:: cout << "enter a fucking correct form of a binary number." << std:: endl;
                Condition = 0, binary.clear();
                break;
            }
        }
        condition = (Condition == 0);
    }
    adjust();
}
void input(){
    using namespace std;
    cin >> text;

    while(1){
        if(text == "dtb" || text == "dtb "){
            cout << "enter your decimal number to convert it: ";
            while (1){
                if(cin >> decimal){
                    if     (decimal == 0) { binary = "0";  break;
                    }else if(decimal > 0 && decimal < 32768){
                        calculate1();  break;
                    }else if(decimal < 0 && decimal > -32768){
                        decimal = -decimal;
                        calculate1(); calculate2(); break;
                    }else{
                        break;
                    } 
                }else{
                    cout << "what the fuck is this? don't be stupid and enter a correct form of a decimal number.";
                    cout << endl;
                    cin.clear(); fflush(stdin);  // مع استعانة chatgpt
                }
            }
            if(decimal < 32768 && decimal > -32678){
                cout << "the binary number of that decimal number is: " << binary << "\n\n";
            }else if(decimal > 32767){
                cout << "this number is too big to be converted." << "\n\n";
            }else if(decimal < -32767){
                cout << "this number is too small to be converted." << "\n\n";
            }
            cout << "try a different number if you want." << endl;
            decimal = 0; binary.clear(); print(); break;
        }else if(text == "btd"|| text == "btd "){
            cout << "enter your binary number to convert it: ";
            check(); 
            if(binary.size() < 16){
                calculate3();
                cout << "the decimal number of that binary number is: " << decimal << "\n\n";
            }else if(binary.size() == 16){
                if(binary == "1000000000000000"){
                    cout << "this number is actually very unique, it separates between the largest positive decimal number, " << endl;
                    cout << "and the smallest negative decimal number. which mean it can't be converted." << "\n\n";
                }else{
                    calculate4();
                    cout << "the decimal number of that binary number is: " << decimal << "\n\n";
                }
            }else{
                cout << "this binary number is too big to be converted." << "\n\n";
            }
            cout << "try a different number if you want." << endl;
            decimal = 0; binary.clear(); print(); break; // مع استعانة chatgpt
        }else if(text == "x"){
            break;
        }else{
            cout << "don't fuck with me! try again and enter either dtb or btd." << endl;
            cin >> text;
        }
    }
}
int main(){
    start(); while(text != "x") input();
    std:: cout << "thanks for using this program and I hope you like it!" << std:: endl;

    return 0;
}
/////////////////////////////////////////////////////////////////////////////////////////////////////
