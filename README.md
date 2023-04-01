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
- As we discussed we have 4 types of input viz. C, del, = and operator/digit. All these need to handled separately. Lets use _if else_ to handle these cases.
 ```
   buttonPressed(String input) {
    if(input=='C'){

    }else if(input=='Del'){

    }else if(input=='='){
      
    }else{
      
    }
  }
 ```
 - For the first part i.e. the input is 'C', we just need to clear out our expression and output. For that we will add the following code to the first part i.e. if statement of the function.
 ```
     if (input == 'C') {
      setState(() {
        expression = '';
        output = '';
      });
    } 
 ```
 - For the second part i.e when we the 'Del' button is clicked, we need to first check whether our string is emply or not. If the string length is greater than 0, we will remove the last character of the string which can be done by selecting substring of expression from 0 to length-1. For the same we will add the following code in the first else if part of the function.
 ```
 else if (input == 'Del') {
      if(expression.length>0){
        setState(() {
          expression=expression.substring(0,expression.length-1);
        });
      }
    }
 ```
 - When the = button is pressed we need to calculate the expression right. So for that we will call a function evalExpression, which we will create afterwards.
  - Since in the last part, we are just adding the character inputed to the expression we just need to add input to the expression. Since we also need to show that it changes expression shown in container we need to use setState.
 - So we will add the follwing code to the else statement of the function.
 ```
 else {
      setState(() {
        expression += input;
      });
    }
 ```
 - Now that we are ready with the working of the buttons lets add this feature to the button. For that we need to pass the function to the MyButton class. For the same we will create a new variable that takes this function as input and also add this to its constructor. The MyButton class will look like this afterwards.

 ![image](https://user-images.githubusercontent.com/76885050/229315831-8b3b090d-4bbe-4dee-bc15-c81e3bf750f4.png)
- Now we will add this to our GestureDetector. As we discussed it has many attributes from which one is onTap which takes a function as an input. We call our buttonPressed function here.
- The GestureDetector will look like this afterwards.
- ![image](https://user-images.githubusercontent.com/76885050/229315899-4f7cc927-d123-4dfd-ae87-450c740bf1bc.png)
- Now we will need to pass this function everywhere we used MyButton.
- For example a call will look like:
```
                        MyButton(
                            buttonText: 'C',
                            buttonColor: Colors.orange,
                            buttonPressed: buttonPressed),
```
- Now that we are only left with the evaluation part of the calculation, for which lets add a dependency, so that we get an idea how to do that too. For the same we will open [pub.dev](https://pub.dev/) and there we will search for math expression.
- On searching something like below comes up
![image](https://user-images.githubusercontent.com/76885050/229316355-92430787-a156-44ff-bd08-122ef752602f.png)
- These are the dependencies that we can add to our app and use their functionalities.
- Open the first dependency i.e. math_expressions.
- ![image](https://user-images.githubusercontent.com/76885050/229316452-e30a978f-965a-4553-b7f9-725ea8f87abb.png)
- click the copy option near the name.
- Now in our project we will open the pubspec.yaml file and paste the copied text to **Line 38** of the file.Here what we did was added a dependency. Incase the IDE does not run flutter pub get on its own, you can run it using the command flutter pub get.
- the pubspec.yaml files will look like this:
```
dependencies:
  flutter:
    sdk: flutter


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2
  math_expressions: ^2.3.1

dev_dependencies:
  flutter_test:
    sdk: flutter
```
- Now that we have our dependency installed we can use its functionalities in our code.
- For the evaluation part of the calculator we will use this dependency.
- For the evaluation part lets create a new function evalExpression which will be called when = is pressed.
- adding evalExpression to if else statement of =
```
else if (input == '=') {
      evalExpression();
    }
```
- Now we will add new function after the buttonPressed function.
```
  evalExpression(){
    
  }
```
- In this function we will create a parser which will be used for parsing the string expression that the user inputed. If it shows any error then import the math_expression package. To make it working add the following code to the evalExpression function.
```
  evalExpression() {
    Parser p = Parser();
    Expression exp = p.parse(expression);
    ContextModel cm = ContextModel();
    setState(() {
      output = '${exp.evaluate(EvaluationType.REAL, cm)}';
    });
  }
```
If you didn't understand what the above code meant, refer to pub.dev at [maths_expression](https://pub.dev/packages/math_expressions) and see examples there. If you are not getting any line, feel free to contact.


