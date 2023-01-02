#include<iostream>  
#include<stack> 
#include<math.h> 
using namespace std;  
// defines the Boolean function for operator, operand, equalOrhigher precedence and the string conversion function.  
bool IsOperator(char);  
bool IsOperand(char);  
bool eqlOrhigher(char, char);  
string convert(string);  


int calculate_Postfix(string  post_exp)
{
    stack <int> stack1;
    int len = post_exp.length();
    // loop to iterate through the expression
    for (int i = 0; i < len; i++)
    {
        // if the character is an operand we push it in the stack
        // we have considered single digits only here
        if ( post_exp[i] >= '0' &&  post_exp[i] <= '9')
        {
            stack1.push( post_exp[i] - '0');
        }
        // if the character is an operator we enter else block
        else
        {
            // we pop the top two elements from the stack and save them in two integers
            int a = stack1.top();
            stack1.pop();
            int b = stack1.top();
            stack1.pop();
            //performing the operation on the operands
            switch (post_exp[i])
            {
                case '+': // addition
                          stack1.push(b + a);
                          break;
                case '-': // subtraction
                          stack1.push(b - a);
                          break;
                case '*': // multiplication
                          stack1.push(b * a);
                          break;
                case '/': // division
                          stack1.push(b / a);
                          break;
                case '^': // exponent
                          stack1.push(pow(b,a));
                          break;
            }
        }
    }
    //returning the calculated result
    return stack1.top();
}
  
int main()  
{  
string infix_expression, postfix_expression;  
int ch;  
do  
{  
cout << " Enter an infix expression: ";  
cin >> infix_expression;  
 postfix_expression = convert(infix_expression);  
 cout << "\n Your Infix expression is: " << infix_expression;  
cout << "\n Postfix expression is: " << postfix_expression; 

//string postfix_expression = "59+33^4*6/-";
    cout<<"\n The answer after calculating the postfix expression is : ";
    cout<<calculate_Postfix(postfix_expression); 
cout << "\n \t Do you want to enter infix expression (1/ 0)?";  
cin >> ch;  
//cin.ignore();   
} while(ch == 1);  
return 0;  
}  
  
// define the IsOperator() function to validate whether any symbol is operator.  
/* If the symbol is operator, it returns true, otherwise false. */  
bool IsOperator(char c)  
{  
if(c == '+' || c == '-' || c == '*' || c == '/' || c == '^' )  
return true;     
return false;  
}  
  
// IsOperand() function is used to validate whether the character is operand.  
bool IsOperand(char c)  
{  
if( c >= 'A' && c <= 'Z')  /* Define the character in between A to Z. If not, it returns False.*/  
return true;  
if (c >= 'a' && c <= 'z')  // Define the character in between a to z. If not, it returns False. */  
return true;  
if(c >= '0' && c <= '9')   // Define the character in between 0 to 9. If not, it returns False. */  
return true;  
return false;  
}  
// here, precedence() function is used to define the precedence to the operator.  
int precedence(char op)  
{  
if(op == '+' || op == '-')                   /* it defines the lowest precedence */  
return 1;  
if (op == '*' || op == '/')  
return 2;  
if(op == '^')  /* exponent operator has the highest precedence */
return 3;       
return 0; 
} 
/* The eqlOrhigher() function is used to check the higher or equal precedence of the two operators in infix expression. */  
bool eqlOrhigher (char top_stack, char incoming)  
{  
int p1 = precedence(top_stack);  
int p2 = precedence(incoming);  
if (p1 == p2)  
{  
if (incoming == '^' )  
return false;  
return true;  
}  
return  (p1>p2 ? true : false);  
}  
  
/* string convert() function is used to convert the infix expression to the postfix expression of the Stack */  
string convert(string infix)  
{  
stack <char> S;  
string postfix ="";    
char ch;  
  
S.push( '(' );  
infix += ')';  
  
for(int i = 0; i<infix.length(); i++)  
{  
ch = infix[i];  
  
if(ch == ' ')  
continue;  
else if(ch == '(')  
S.push(ch);  
else if(IsOperand(ch))  
postfix += ch;  
else if(IsOperator(ch))  
{  
	while(!S.empty() && eqlOrhigher(S.top(), ch))  
	{  
	postfix += S.top();  
	S.pop();  
	}  
	S.push(ch);  
}  
else if(ch == ')')  
{  
	while(!S.empty() && S.top() != '(')  
	{  
	postfix += S.top();  
	S.pop();  
	}  
	S.pop();  
}  
}  
return postfix;  
}  
