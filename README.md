#include<iostream>
#include<conio.h>
#include<windows.h>
using namespace std;
bool gameover;
const int width=20;
const int height=20;
int x,y, fruitx, fruity, score;
int tailx[100]; int taily[100];
int ntail;
enum eDirection{ STOP=0, LEFT, RIGHT,UP,DOWN};
eDirection dir;
void setup(){
  gameover=false;
  dir=STOP;
  x=width/2;
  y=height/2;
  fruitx=rand()% width;
  fruity=rand()% height;
  score=0;
}
void draw(){
  system("cls");
  for(int i=0; i<width+2; i++){
     cout << "#";
  }
  cout << endl;
  for(int i=0; i<height; i++){
     for(int j=0; j<width; j++){
       if(j==0)
        cout << "#";
       if(i==y && j==x)
          cout << "O";
      else if(i== fruity && j==fruitx)
         cout << "F";
       else{
        bool print=false;
        for(int k=0; k<ntail; k++){
            if(tailx[k]==j && taily[k]==i){
            cout << "o";
            print=true;
          }
        }
       if(!print)
       cout << " ";
       }


       if(j==width-1)
        cout << "#";
   }
     cout << endl;
  }
  for(int i=0; i<width+2; i++){
     cout << "#";
  }
  cout << endl;
  cout << "Score:" << score;
}
void Input(){

if(_kbhit())// it checks if the user hit the key
 {

   switch(_getch())// it gets the character
   {
       case 'a':
       dir=LEFT;
       break;
       case 'd':
       dir=RIGHT;
       break;
       case 'w':
       dir=UP;
       break;
       case 's':
       dir=DOWN;
       break;
      case 'x':
       gameover=true;
       break;
     }
   }
}
void logic(){
  int pvsx=tailx[0];
   int pvsy=taily[0];
   int pvx; int pvy;
   tailx[0]=x; taily[0]=y;
   for(int i=1; i<ntail; i++){
        pvx=tailx[i];
        pvy=taily[i];
        tailx[i]=pvsx;
        taily[i]=pvsy;
        pvsx=pvx;
        pvsy=pvy;
   }
  switch(dir){
    case LEFT:
     x--;
    break;

    case RIGHT:
     x++;
       break;

    case UP:
    y--;
       break;

    case DOWN:
    y++;
       break;

    default:
      break;
   }
   //if(x>width || x<0 || y>height || y<0)
    //gameover=true;
    if(x>=width){x=0;}else if(x<0){x=width-1;}
    if(y>=height){y=0;}else if(y<0){y=height-1;}
   if(x== fruitx && y== fruity){
    score+=10;
    fruitx=rand() %height;
    fruity=rand() %width;
    ntail++;
}
}

int main(){
  setup();
  while(!gameover){
    draw();
    Input();
    logic();
     Sleep(70);
  }
}
