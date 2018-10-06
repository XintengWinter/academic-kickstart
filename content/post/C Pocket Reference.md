+++
title = "Lesson 1: Introduction and Program Structure"
date = 2018-03-03T13:23:10+01:00
draft = false
tags = ["C++ Pocket Reference", "C Pocket Reference", "Pocket Reference", "Loudon", "Kyle Loudon", "Lesson 1"]
categories = ["C++ Pocket Reference"]

+++

# Introduction

## *Compatibility with C*

With a few minor exceptions, C++ was developed as an extension, or superset, of C.

1. What this means:
   * Well-written C programs generally will compile and run as C++ programs.
     * *Most incompatibilities stem from the stricter type checking of C++*
   * C++ programs tend to look syntactically similar to C and use a lot of C's original functionality.
   * **On top of** what C has, the C++ language also has support for:
     * Object-oriented programming
     * generic programming using templates
     * namespaces
     * inline functions
     * operator and function overloading
     * better facilities for memory management
     * references
     * safer forms of casting
     * runtime type information
     * exception handing
     * an extended standard library

# Program Structure

At the highest level, a C++ program is composed of one or more *source files* that contain C++ source code. 

1. These files define *only* one starting point, and perhaps various points at which to end. 

C++ source files frequently import, or *include,* additional source code from *header files*. The C++ preprocessor is responsible for including code from these files before each file is compiled. At the same time, the preprocessor can also perform various other operations through the use of *preprocessor directives.* 

{{% alert note %}}
**Note!** A source file after preprocessing has been completed is called a *translation unit.*
{{% /alert %}}

## *Startup*

The function ``main`` is the designated start of a C++ program, which the developer must define. In its standard form, this function accepts zero *or* two arguments supplied by the operating system when the program starts.

{{% alert note %}}
**Note!**  Many C++ implementations allow additional parameters.
{{% /alert %}}

It's return type is ``int``.

* Example:

  ``int main()``

  ``int main(int argc, char *argv[])`` 

  * ``argc`` is the number of arguments specified on the command line
  * ``argv`` is an array of null-terminated (C-style) strings containing the arguments in the order they appear
  * The name of the executable is stored in ``argv[0]``, and may or may not be prefixed by its path. The value of ``argv[argc]`` is 0.
  * The following shows the main function for a simple C++ program that prompts the user for actions to perform on an account:

```C++
#include <iostream>
#include <cmath>
#include <cstdlib>
using namespace std;
#include "Account.h"
int main(int argc, char *argv[])
{
    Account       account(0.0);
    char          action;
    double        amount;
    if (argc > 1)
        account.deposit(atof(argv[1]));
    while (true)
    {
        cout << "Balance is "
             << account.getBalance()
             << endl;
        cout << "Enter d, w, or q: ";
        cin  >> action,
        
        switch (action)
        { 
            case 'd':
        		cout << "Enter deposit: ";
                cin >> amount;
                account.deposit(amount);
                break;
            case 'w':
                cout << "Enter withdrawal: ";
                cin  >> amount;
                account.withdraw(amount);
                break;
            case 'q':
                exit(0);
            default:
                cout << "Bad command" << endl;
        }
    }
    return 0;
}
```

The class for the account is defined in a later example. An initial deposit is made into the account using an account specified on the command line when the program is started.

The function ``atof`` (from the C++ Standard Library) is used to convert the command-line argument from a string to a ``double``.

## *Termination*

A C++ program terminates when you return from ``main``. The value you return is passed back to the operating system and becomes the return value for the executable. If no return is present in ``main``, an implicit return of 0 takes places after falling through the body of ``main``. 

You can also terminate a program by calling the ``exit`` function (from the C++ Standard Library), which accepts the return value for the executable as an argument.

## *Header Files*

This contains source code to be included in multiple files. They usually have a *.h* extension. **Anything to be included in multiple places belongs in a header file.** A header file should ***never*** contain the following:

* Definitions for variables and static data members
* Definitions for functions, except those defined as template or inline functions
* Namespaces that are unnamed.

{{% alert note %}}
**Note!** Headerfiles in the C++ Standard Library do not use the *.h* extension; **they have no extension**
{{% /alert %}}

Often you create one header file for each major class that you define. **For example:** ``Account`` is defined in the header file as *Account.h*, shown below.

Header files are used for other purposes, and not all class definitions need to be in header files (e.g., helper classes are defined simply within the source file in which they will be used).

```c++
#ifndef ACCOUNT_H
#define ACCOUNT_H

class Account
{
public:
    				Account(double b);
    void 			deposit(double amt);
    void			withdraw(double amt);
    double			getBalance() const;
private:
    double			balance;
};
#endif
```

