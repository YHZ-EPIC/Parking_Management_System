# Project : Parking Management System
    Vehicle Parking Management System

# Subject : Computer Organization and Assembly Language
    COAL | MASM x86 Assembly Language Project

<font style="color:#fff; font-family: 'Bebas Neue'; font-size: 3.5ch">

<b> By Yasir Hussain </b> 

### Note : Source.asm file contains all the code.

## Introduction

Working on projects is the best way to finalize and refine, what we learnt so far throughout the 
semester. \
Initially i couldn’t come up with any ideas so I decided to go the traditional way of 
doing projects for any programming language and that is creating a Management system. So I
finalized parking management system to be the project written in x86 assembly language.
Doing it alone means I can work on my projects whenever and however I see fit and don’t need 
to wait for response from project partners and that’s why I decided to do it alone.

## Background

I selected this project because it was easy to be found on internet as a sample project upon which 
I can build my own variation of it , the problem I faced was that (MASM + Irvine Library) isn’t
used much in the world , majority people use either NASM assembly or x86 assembly without 
any linked libraries , so it was almost impossible to find a decent code to be used as sample for 
my project. I found a code written in NASM assembly and I needed to convert it to MASM 
equivalent of it , it took me some time to build the foundations then I kept adding features and 
improve my project due to built-in Irvine library functions and wrappers.

## Project Specifications

My Project provides basic and decent functionality for a Parking Management System , it can

    1) Add Vehicles into Parking.
    2) Remove Vehicles from Parking
    3) It can count Vehicles as you Park them
    4) It handles exceptions very well
    5) It can Display the Record
    6) It can delete all Records.
    7) It can perform basic filling by storing the user name in a file.

    *NOTE: User may experience Lag throughout the Program due to extensive use of Clrscr()
    function in different scenarios of code.
    Problem Analysis

A good Parking Management System would be able to add different types of Vehicle and Charge 
different amounts for each Vehicle. It should also keep track of Total Parking lots available so 
that User can’t exceed the Parking limit. Vehicles may depart too so it should also be able to 
Free up Parking place according to the scenario. It should be able to Display complete record 
including count of different vehicle types and Total amount to be charged for all Vehicles.

## Solution Design

I took modular approach of programming for my project because assembly is a procedural 
language. I tried to make my code as maintainable as I could by adding comments and provide 
necessary spacing where needed. It performs all the functionalities and handles all kind of 
exceptions I mentioned above.

## Implementation and Testing

I implemented my Project in Visual Studio 2019 (Community Edition) linked with Irvine Library 
which contains advanced functions and wrappers to make my job easy as it is quite hard to make 
a project in pure assembly code. I kept testing my project at different steps of its production. As 
the code grew large and large, more time was spent in its debugging and bug fixing. But in the 
end I was able to fix all types of crashes and bugs that I experienced and my finalized project is 
working great. I would not call my Project in any ways the most optimized or even optimized 
code. Now a days, compilers have become so advanced that they generate far superior and most 
optimized code in assembly language then a human being could ever write. So aiming for most 
optimized code while working in assembly language is an almost impossible task if done by 
human.

## Project Breakdown Structure

To be honest, I initiated and completed the project in just span of Two days. The reason for that 
being the availability of sample code in NASM assembly which acted as a base for my project 
then I found motivation to keep improving the code and adding new features. It wasn’t easy at all 
but not so hard either.

## Results

After I finished working on my project. It ran smoothly and without any crashes at all. It guides 
the user on different steps of its execution, also I learnt that despite adding so much functionality
The final size of my program was just 8.86KB which was insanely small. For the first time I felt 
like 1KB is a lot of memory, it is not hard to realize that the size of modern day programs are 
fairly justified for the amount of functionalities they provide. My code is open source and subject 
to improvement too, I will soon upload it on GitHub and take part in Open Source Community.

## Conclusion

In the end, it was a great experience. I enjoyed it and got the chance to apply the 
basics of assembly into my project. I still need to practice a lot and learn regarding 
assembly language and its advanced topics. I hope that this project report gets read 
because I spent almost half an hour preparing it. That’s all for my concluding 
thoughts regarding this project

## Reference

For Detailed Installation Steps, Kindly Refer to this Official Documentation,

http://asmirvine.com/gettingStartedVS2022/index.htm

</font>