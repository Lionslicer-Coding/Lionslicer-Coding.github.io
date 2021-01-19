---
layout: post
title:      "Transitioning from C++ to Python"
date:       2021-01-19 10:36:15 +0000
permalink:  transitioning_from_c_to_python
---

## Introduction

"Your C++ is showing."

I was convinced I had totally bombed the technical interview. After a brief period of conversation that I thought had gone well, my interviewer gave me a list of some very basic tasks to perform in Python. The first task was declaring a variable and assigning a value to it. I began:


`int var = 4`



"Mmm… nope." My interviewer waited patiently for me to figure out my mistake, and after a minute or so I realized I had mixed up C++ and Python syntax, fixed it, and moved on. Next task: create a list and iterate through it using a for loop. I begin again:


```
Num_list = [0,1,2,3]

for( i=0; i<4; i++):
    print(num_list[I])
```



Again, a weird mashup of languages that wouldn't work in either. At this point I'm starting to panic a bit, but my interviewer calmly says, "your C++ is showing", and helps me identify my errors and fix them. The rest of the interview went fairly well, and luckily I was accepted into the Data Science bootcamp I had applied for and been so certain I had tanked the interview for. 

Obviously, the purpose of the bootcamp is to learn a new skill and move my career forward. It's been a wonderful, sometimes incredibly stressful journey, and as I near graduation I have been reflecting on the challenges I have faced in the program. One of the most persistent stumbling blocks has been transitioning from what I learned in my C++ classes into Python. Even on my capstone, I found myself wanting to approach problems and documentation as I would have in C++. 

There are hundreds of guides around the internet describing the technical differences between C++ and Python. They do a great job of stating the differences very explicitly, and I made sure to read several before diving into this course. What they didn't prepare me for were some of the culture shock moments when things were just different enough to make me uncomfortable while still generally grasping what was being done. 

With that in mind, I thought I would close out my time in this program by creating a list of these moments, in the hope that someone will see these moments and relate a little too well to some of them!


## How does it know?!

I know it's simple, but after half a decade of working with C++ I'm not sure that I will ever get used to Python inferring data types. The first month or so of coding with Python, I found myself routinely having to back up and remove an "int" or the occasional "string" because I felt compelled to be very explicit with my code. 

## No compile, no problem.

For most of the course I actually had no issues with being able to just type up code and run without compiling. Truthfully it felt amazing being able to see any errors in what was basically real time. I did, however have a mental hang-up when I reached my capstone. For the first time in the course, I housed my functions in a file separate from the main block of code. It was a bit of an adventure, to say the least. Importing the code itself wasn't much of an issue once I had the syntax, but I wanted so much to structure my functions file like I'd been taught to do in C++. 

For those unfamiliar, the common practice in C++ is to "declare" your functions at the top of your file and to define it at the bottom, to make your code more readable. For example, to define a do_thing function:


```
int do_thing(int num1, int existential_crisis);

//Insert your program here

int do_thing(int num1, int existential_crisis){

//Whatever your function does

}
```

This is possible because of C++ needing to be compiled first. In Python, however, you define the function in it's entirety or you don't at all. Having my functions in a separate file and importing them into my main file made it feel more like my old C++ workflow, but the structure of my functions file will probably never look as organized to me as it would in C++. 


