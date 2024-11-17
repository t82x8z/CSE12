java c
CSE12 Lab 3: Looping in RISC-V Assembly 
Submission by due date at 11:59 PM 
Minimum Submission Requirements
Ensure that your Gradescope submission contains the following file:
○           Lab3.asm
Objective This  lab  will  introduce  you  to  the  RISC-V  assembly  language  programming  using  RARS  (RISCV Assembler and Runtime Simulator). You will write a program with nested loops in the provided file Lab3.asm to write a specific pattern to a file by the name of lab3_output.txt (which will be generated by running your submitted Lab3.asm file. lab3_output.txt does not exist prior to this action)Make sure you properly follow the steps mentioned in the RARS site to download and install RARS on your machine. Please approach a TA or tutor in your lab section if you have issues installing RARS on your machine!
Since this is your very first foray into assembly programming, please read this document thoroughly without skipping any sections!
Resources 
Much like how a high-level program has a specific file extension (.c for C, .py for python) RARS based RISC-V programs have a .asm extension.
In the Lab3 folder in the course Google Slide, you will see 7 assembly files. They are meant for you to read (and understand) in sequence:
1. firstRARSprogram.asm – This program just prints “Hello World” on the output console.
2. add.asm – This program accepts two integers as user inputs and prints their addition result on the output console.
3. multiply.asm – This program accepts two integers as user inputs and prints their multiplication result on the output console. This file specifically shows you how to do loops in assembly
4. fileWriteDemo.asm – This program creates a file for writing, and then writes a line of text into the file. Basically, it shows the basics to do a file Write in RARS.
5. fileReadDemo.asm – This program reads the file generated by the above .asm file and reads out its contents on the output console. Basically, it shows the basics to do a file Read in RARS.
6. patternDisplayDemo.asm – This program inputs a number n from user and generates a “*  *  * ….” Pattern depending on the value of n. This pattern is written into a file. Understanding how this code works will help you in writing the pattern required of this lab assignment into a file as well.7. Lab3.asm – Some starter code has already been provided in this file which you will need to complete  and  then  submit  to  your  Gradescope  autograding  portal.  The  starter  code  mainly  revolves around macros that have been created for your benefit to create and write to the file lab3_output.txt.
Please download these files and make sure to open them in the RARS Text editor only. Doing otherwise will cause comments and other important code sections to not be properly highlighted and can be a hindrance to learning assembly language intuitively. Steps for opening, assembling and running a  .asm file are provided later in this document.
These 7 files have enough comments in the source code to jump start your understanding of RISC-V assembly programming if the lectures have not yet covered certain topics in assembly programming.Beyond these three files, you should have all the required resources in the Lecture Slides themselves, in the lecture pages following the topic “Von Neuman and RISC- V”. These lecture slides are very self- explanatory. You are encouraged read ahead even if the instructor hasn’t started discussing them in lecture. You are also encouraged to read the excellent RARS documentation which can be found by clicking “help” on the RARS program, or at these URLs: https://github.com/TheThirdOne/rars/wiki and https://github.com/TheThirdOne/rars For the usage of macros (which are utilized heavily in this lab to generate system calls refererred to as ecalls), please also refer to the RARS documentation on macros and ecalls as well. For lab3, you don’t even need to know what the inside of a macro block looks like so long you know just what it is supposed to do overall. 
Working in RARS Helpful tip: For lab3 and lab4, it is recommended that you create two separate folders in your machine, lab3 and lab4. Make each folder the workspace for your respective lab. So, for the given lab, place all the provided  .asm files in the Lab3 folder along with a copy of the .jar RARS application file, and run RARS from there. This is where you will create your Lab3.asm file as well.

Figure 1 Ideal workspace setup for lab3/lab4 
Henceforth, run all .asm files pertinent to Lab3 on this local copy of the .jar RARS application. Open the RARS application. You should get the window below.

Figure 2 Opening the RARS application 
Let us open firstRARSprogram.asm by clicking File -> Open.
Make sure the comments (which appear in green) are properly indented and haven’t been misaligned when you downloaded the file from the Google Drive. They should appear as shown below:

Figure 3 Opening an asm file on RARS Make sure to thoroughly read the entire contents of this file in the text editor . Verbose comments have been provided to guide you along in explaining each step in the source code. This will be the norm for the other .asm files in the Lab3 folder in Google Drive as well.After you have read and understood the source code, it is time to assemble the program. Before you assemble, go to Settings and make sure you have the exact following options checked (or unchecked). For this course, you are allowed to use pseudo instructions. Pseudo instructions are those instructions which are not native to the RISC-V instruction set but the RARS environment has defined these new ones by a combination of actual RISC-V instructions. Permit pseudo instructions (this actually makes coding easier for you). This should be done for every RARS code in CSE12! 

Figure 4 RARS setting 
Now  click  on  Assemble  (the  Wrench  and  screwdriver  icon).  If correctly  assembled,  your  Messages window should show the following information:

Figure 5 Successful assembly 
Now Click on the Run button to Run the program. You will get the following output:

Figure 6 Successful Runtime 
Now try running the other .asm files.One word of caution when your text editor contains multiple opened files is to make sure of assembling the correct assembly file. For example, in the window below, multiple files are open.  If I want to only assemble and run add.asm, then my tab for add.asm should be highlighted as shown below. Only then can I click Assemble, then Run.

Figure 7 Multiple tabs open 
A Helpful Feature in RARS RARS has a helpful feature where instead of Running the entire program at once, you can Run One Step At A Time. The corresponding button is beside the Run button. This allows you to sequentially execute each line of code and see how it affects the values of the Registers as they appear to the right of your screen.
Regarding Macros The file multiply.asm makes extensive use of macros to help create a more readable main program section (Instructions on how to use macros are provided in the file comments). So does the source code in the files fileWriteDemo.asm, fileReadDemo.asm and patternDisplayDemo.asm (we will discuss more on the aspect of file reads and writes that these .asm files do shortly). Based on how we define a macro in the source code, it is tempting to confuse it with a function. However, macros are NOT functions! Whenever you place multiple instances of the same macro in your code, you are copying the macro’s contents in those code areas for the same number of times.
Naming New Files in RARS When you want to open a new file on RARS, go to File->New. The default file name riscv1.asm shows up on the tab. When you save this file, you MUST make sure that you are explicitly defining the correct extension(.asm) as shown below.

Figure 8 Saving a new file in RARS 
About File Reads and Writes in RARS File creation and manipulation is a very common part of the learning curve whenever you learn of a new high level programming language, be it C or Python. For lab3, we will be writing the display pattern to a file so that it is more convenient for the auto grader. The auto grader within Gradescope will do a file text equality check between files generated by your lab3 source code and expected correctly generated files and accordingly provide you points (or not!).To  give  you  a  demo,  we  have  two  reference  assembly  source  code  files: fileWriteDemo.asm and fileReadDemo.asm. The former file creates a file with the name fileDemo.txt. The following text is written into fileDemo.txt: “These pretzels are making me thirsty!” . The latter file fileReadDemo.asm contains code to  open fileDemo.txt and  extract  out  this  text  to  display  on  the  output  console  of RARS.The following two images shows the results of having run fileWriteDemo.asm and then fileReadDemo.asm. 
Figure 9 A new file generated in my workspace after running fileWriteDemo.asm. Note the file size to be shown as 1KB despite us having written only 38 bytes of data into it. That is because a file also contains metadata and a header generated by your OS as well. 

Figure 10 RARS 代 写CSE12 Lab 3: Looping in RISC-V AssemblyPython
代做程序编程语言output console after running fileReadDemo.asm 
Both fileWriteDemo.asm and fileReadDemo.asm use many macros within the source code to make the main .text section of the code more programmer friendly in terms of writing. For the purposes of lab3,you DO   NOT need to understand WHAT these macros are doing within their definition block. It suffices to know   simply what the result of executing a macro in your source code simply does. However, understanding the   macros does help to build your foundation in RARS programming well.One thing to note is that since lab3 does not focus on proper function coding in RISC-V assembly, it can get very difficult to keep track of random unintentional instances of your registers to change value. For instance, in C or Python, you can define a variable temp, assign it a specific value, and be rest assured that this  variable  does  not  change  from  the  assigned  value  during  code  compilation  or  runtime  unless explicitly told to. However, in a large source code assembly, working with a limited number of registers means that it is very difficult to keep track of each individual register value unless you are very careful.We will deal with register preservation in lab4 but in lab3, you will only be asked to ensure that you do not use specific registers in your Lab3.asm source code. The list of these taboo registers will be highlighted in the section later on Lab3 Besides  the  aforementioned  2  files  related  to  file  write  and  read,  we  also  have  a   3rd     .asm  file, patternDisplayDemo.asm. The source code in this file, once run, asks as input an integer n and then prints the pattern “* “ n number of times horizontally.


Figure 11 Output console after running patternDisplayDemo.asm for user input n=3 and7. In both cases, make sure to check the contents of the created file patternDisplay.txt as well Similar to patternDisplayDemo.asm, Lab3.asm will also make use of loops (nested loops to be precise) to generate a pattern based on the value of n inputted by the user. Thus, you should thoroughly read and understand the working of source code in patternDisplayDemo.asm. 
Lab3 Programming Assignment 
This program will print out a pattern with stars (asterisks, ascii hex code 0x2a) and blank space (ascii hex code 0x20) and the newline character ‘\n’(ascii hex code 0x0a).1.          It will first prompt for the height of the pattern (i.e., the number of rows in the pattern). If the user enters an invalid input such as a negative number or zero, an error message will be printed and the user will be prompted again. These error messages are listed in the starter code in the Lab3.asm file provided.
2.          Then your program  should generate the following pattern, a " right-angled triangle", using the aforementioned characters. Refer to test cases in testCases sub folder in Lab3 folder for examples.
3.          This entire pattern generated from the user input of n is written to the file lab3_output.txt.
The actual task of opening the file lab3_output.txt and writing the contents to it is borne by macros used in starter code included in the Lab3.asm file. Consider the screenshot of the Lab3.asm file below:

Figure 12 Lab3.asm screenshot 
As you can see, you should write down your code ONLY within the area indicated by the comments. The way this code works regarding file manipulation is as follows:When a file is created in RARS, it is assigned a file descriptor ID, in the form. of an integer number. Future references to this file through macros are then made by referring to this file descriptor ID number. Once we create a file, we first need to set aside memory space within our RISC-V memory where data to be written to the file is kept. This space is referred to as a “memory buffer” . In Lab3.asm, we have defined the memory space starting from address 0x10040000 as our internal memory buffer. Specifically, we hold a doubleword (64 bits) at this address which keeps track of how many bytes we intend to finally write to the file. 0x10040008 onwards, we start collecting the bytes that will be written into the file
lab3_output.txt. In your student code, you can update the file buffer with any character with the macro write_to_buffer. For example, I want to the write the character sequence “****\n” to my memory buffer within Lab3.asm’s student code section. Then I would need to write the following student code as shown next:

Figure 13 Modified Lab3.asm screenshot Run this Lab3.asm file and open the generated lab3_output.txt in a text editor. Specifically, if you are using Notepad++ (which is strongly recommended), make sure to apply the setting: View->Show Symbol ->Show All Characters. This will make characters such as null and newline visible.

Figure 14 lab3_output.txt screenshot from running modified Lab3.asm 
As you can see, the blank space appears as an orange dot, newline as LF (LineFeed) and null as NUL.You can see these characters as they reside in the file buffer in memory too on RARS as shown below. If you go to Execute window after running this modified Lab3.asm, selecting 0x1004000 for view and enabling ASCII view, you will get the following screenshot:

Figure 15 “* ** *\n” data as it resides in file buffer 
Note that within each individual cell in the Data Segment matrix above, we should read the bytes from right to left.
NOTE: For your student starter code, you MUST NOT use any of the registers: t0 to t6, sp.  a0 to a7 should only be temporarilly used to pass parameters or receive parameters from macros.  Using the   registers s0 through s11 should be enough for Lab3 assignment.
Example of running the actual correct Lab3.asm source code
The following is a screenshot showing the runtime of the actual solved Lab3.asm code:

Figure 16 Solved Lab3.asm runtime demo 
When we open the generated lab3_output.txt file, we get the following text:

\Figure 17 lab3_output.txt screenshot Your student code MUST display the prompts and error messages in response to user input EXACTLY as shown in Figure 16. Please make use of the provided strings in the .data section of the starter code in Lab3.asm to make sure you do not use any other type of sentence!
NOTE: Although you are not required to print each row in the pattern on your output console, doing so
(as shown in Figure 16 ) will greatly help in the real time code debugging. So, it is strongly advised to do
so.
Test Cases The Lab3 folder in the Google Drive contains some test cases in testCases  subfolder for the case when user input was n=1, 3, 6, 8, 30. Make sure your code output generates the exact same alignment of characters as provided there for the corresponding n input in your student code.
Automation 
Note that our grading script. is automated, so it is imperative that your program’s output matches the specification exactly. The output that deviates from the spec will cause point deduction.
Files to be submitted to your Lab3 gradescope portal
Lab3.asm 
-This file contains your pseudocode and assembly code. Include a header comment as indicated in the documentation guidelines here. 
A Note About Academic Integrity This  is the  lab  assignment where most  students  start  to  get  flagged  for  cheating.  Please  review  the pamphlet  on Academic  Dishonesty and  look  at  the  examples  in  the  first  lecture  for  acceptable  and unacceptable collaboration.
You should be doing this assignment completely all by yourself! 
Grading Rubric (100 points total) The  following  rubric  applies  provided  you  have  fulfilled  all  criteria  in Minimum Submission Requirements. Failing any criteria listed in that section would result in an automatic grade of zero which cannot be legible for applying for a regrade request. 
20 pt Lab3.asm assembles without errors (thus even if you submit Lab3.asm having written absolutely no student code, you would still get 20 pts!)
80 pt output in file lab3_output.txt matches the specification:
20 pt error check zero and negative heights using the convention shown in Figure 16 
20 pt prompts user until a correct input is entered as shown in Figure 16 
20 pt number of rows match user input (i.e., if n=6, the pattern would have 6 row
20 pt correct sequence of stars and newline characters on each row
Legal Notice All course materials and relevant files located in the Lab3 folder in the course Google Drive must not be shared by the students outside of the course curriculum on any type of public domain site or for financial gain. Thus, if any of the Lab3 documents is found in any type of publicly available site (e.g., GitHub, stack Exchange), or for monetary gain (e.g., Chegg), then the original poster will be cited for misusing CSE12 course-based content and will be reported to UCSC for academic dishonesty.In the case of sites such as Chegg.com, we have been able to locate course material shared by a previous quarter student. Chegg cooperated with us by providing the student's contact details, which was sufficient proof of the student's misconduct leading to an automatic failing grade in the course.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
