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

