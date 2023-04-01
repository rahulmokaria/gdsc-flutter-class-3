# gdsc-flutter-class-3

## Aim
To finish our calculator application. We already covered the UI(User Interface) part in the last lecture which can be found [here](https://github.com/rahulmokaria/gdsc-flutter-class-2). If you didn't create the UI part then we suggest to go through it and create it step by step. For use, the UI part can also be found [here](https://github.com/rahulmokaria/flutter_calculator_ui).
- Just for recap what we did was created three containers, first for user input or the mathematical expression, second for the output of the expression and lastly the third one for creating the grid like structure.
- In the grid we created a column in which we had 5 rows and each row had 4 buttons , each specifying a certain digit or operator.
- Then we gave it some colors and sizes to make it look more eye pleasing.

We will now continue with the functionslity part i.e. the working of the calculator app.
- Since for calculating the expression we need to store it somewhere, we will create new variables of type String(as we have used Text widget to display our expression and output.) for our expression and output.
- For the same we will add the following code to **Line 14** of **calc.dart** i.e inside the CalculatorPage class.
```
  String expression = "";
  String output = "";
```
- The code will look something like this:
![image](https://user-images.githubusercontent.com/76885050/229313280-b904a49f-2e9c-42da-9c3e-3f59681bca26.png)
- Now we will show the expression and output in the first and the second container respectively.
- For the same we will change the expression "0+0" to expression and output "0" to output.
- The first two containers will look as follows:
![image](https://user-images.githubusercontent.com/76885050/229313429-f9a90074-6766-484d-a76e-6c371a5316ad.png)
- Now what we want is that when the buttons are clicked, if operator or digit then added to the expression and if C, del or = then remove the expression, remove the last character and calculate the expression respectively. First we will add digits and operator to the expression, for that we will need to create a function that adds that specific digit/opeartor to the expression.
- We will create a new function buttonPressed to do the functioning. Since we need to know which button was pressed we need to take input i.e. pass a String variable to the function.
- We will add the following code to our **calc.dart** file at **Line 16**.
```
 buttonPressed(String input) {
    
  }
```
