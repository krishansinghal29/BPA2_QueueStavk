/*
// Sample code to perform I/O:

#include <iostream>

using namespace std;

int main() {
	int num;
	cin >> num;										// Reading input from STDIN
	cout << "Input number is " << num << endl;		// Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/

// Write your code here
#include <iostream>
#include <stdio.h>
using namespace std;

class stackk 
{
   public:
      int top=-1;   // Length of a box
      int bot=0;
      //vector<int> st;  // Breadth of a box
      int st[1000000];
      int empty(){
         if((top-bot)==-1){
             return 1;
         }
         else{
             return 0;
         }
      }
      int pop(){
          if((top-bot)==-1){
             printf("Error");
          }
          else{
              top=top-1;
              int out=st[top+1];
              //st.resize(top+1);
              return out;
          }
      }
      int popbot(){
          if((top-bot)==-1){
             printf("Error");
          }
          else{
              bot=bot+1;
              int out=st[bot-1];
              return out;
          }
      }
      void push(int i){
          top=top+1;
          st[top]=i;
          //st.push_back(i);
          return ;
      }
};
int small(stackk A){
    int len=A.top-A.bot+1;
    int ans=A.st[A.bot];
    int j;
    for(int i=1;i<len;i++){
        if(ans>A.st[A.bot+i]){
            ans=A.st[A.bot+i];
            j=A.bot+i;
        }
    }
    return ans;
}
int smallind(stackk A){
    int len=A.top-A.bot+1;
    int ans=A.st[A.bot];
    int j=A.bot;
    for(int i=1;i<len;i++){
        if(ans>A.st[A.bot+i]){
            ans=A.st[A.bot+i];
            j=A.bot+i;
        }
    }
    return j;
}

int main(){
    int cases;
    scanf("%d\n",&cases);
    for(int j=0;j<cases;j++){
        stackk A;
        stackk B;
        stackk C;
        int len;
        scanf("%d\n",&len);
        for(int i=0;i<len;i++){
            int inp;
            scanf("%d\n",&inp);
            //printf("%d\n",inp);
            A.push(inp);
        }
        while(A.empty()!=1||B.empty()!=1){
            //printf("A");
            if(A.empty()!=1&&B.empty()!=1){
                if(small(A)<B.st[B.top]){
                    int m=smallind(A);
                    while(A.bot<=m){
                    int push=A.popbot();
                    B.push(push);
                    }
                }
                else{
                    int push=B.pop();
                    C.push(push);
                }
            }
            //printf("B");
            else if(A.empty()!=1&&B.empty()==1){
                int m=smallind(A);
                while(A.bot<=m){
                int push=A.popbot();
                B.push(push);
                }
            }
            //printf("C");
            else{
                int push=B.pop();
                C.push(push);
            }
            //printf("D");
        }
        //printf("E");
        while(C.top>=C.bot){
            printf("v%d",C.popbot());
        }  
        //printf("F");
    }     
    return 0;
}
