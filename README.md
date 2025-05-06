# TCL WORKSHOP

## AGENDA
### DAY 1: TCL Introduction         
### DAY 2: Aotogeneration of Variable and processing Constraints from CSV    
### DAY 3: Generate SDC from CSV, Clock and Input Constraints
### DAY 4: Yosys Synthesis Introduction 
### DAY 5: Advanced Scripting (Proc)

# DAY 1
## TCL Introduction 
### 1. Read csv file using libreoffice 
command : </br> 
![image](https://github.com/user-attachments/assets/46ad534a-77f5-4d17-9ec2-abf3cce1b354)

File contents :</br>
![image](https://github.com/user-attachments/assets/e5af5fc0-d61c-4416-b1bd-86c54cdb302d)

### 2. Generate "yogisynth" command using bash / tcsh script 
genrate a command which will take the csv file path from user, check if path is valid, file exists and then passes that file to the tcl script command also provides help  about command by using `./yogisynth -help`
</br>

Generate a file called yogisynth using linux terminal  `gedit yogisynth` or `gvim yogisynth` and it shall have below segments of coads to  carryout various desired functionality explained below.

Generated file should look like below: <br>
1. First line tells the linux operating system that it is a shell script, other part of the code just informs user about what the command or this shell script does
   ![image](https://github.com/user-attachments/assets/27a401de-0740-4d38-9c09-841eb7f29cac)

2. check number of arguments is one or not, otherwise exit the command </br>
   ![image](https://github.com/user-attachments/assets/6feaf19d-4916-48de-aff9-c63acf63f4e1)

3. check if user has provided -help argument or the file path, if path or file, check if it exists </br>
   ![image](https://github.com/user-attachments/assets/9abc91d4-7d74-494c-98bf-06e84583aa26)

4. provide useful information to user by adding the help for using the command `./yogisynth <csv_filepath>` </br>
   ![image](https://github.com/user-attachments/assets/31aa6272-68fe-4efd-a6ce-600136d9e514)

5. if user provides one argument and it is not '-help' and the file  or path exists, pass that to the tcl script yogisynth.tcl </br>
   ![image](https://github.com/user-attachments/assets/d99692a2-b8f2-424b-87a4-36fb90e1b374)

# DAY 2
## Aotogeneration of Variable and processing Constraints from CSV to generate SDC ( format 1)
Target is to read csv files containing the various file /folder paths and generate the variables and assign the path values to those variable
 1. Create the variables using tcl scrip by reading the CSV file cell containts ( first columns)
 2. Check if the files / folder paths provided by user in a csv file ( second column)  does exists 
 3. convert the csv containt table to the sdc format acceptable by syntheis and PnR tool
 4. Read all .v files from the verilog netlist folder and arange it in Yosys understandable format
 5. Create a syntheis script for converting rtl netlist to gatelvel netlist using yosys tool ( Format 2)
   ![image](https://github.com/user-attachments/assets/1742a785-77c7-44e0-8bed-86b010dc86a4)

   **Remember in tcl :**
   a. echo in shell  = puts
   b. contents in [ ] are the commands
   c. commands can be easily nested and can quickly become complex, once you get the logic correctly its easy
   d. $varibale name is used for accesing its value stored under that varibale name
   e. { } indicate the block of code

**Lets look into the details of each step **
### 1. Create the variables using tcl scrip by reading the CSV file cell containts ( first columns)
 shell script will pass the command argument to the tcl script using `tclsh yogisynth.tcl $argv[1]` where $argv[1] is nothing but a path of the csv file entered in the shell command
 for automatically generating the variables by reading the csv file following steps are involved
 1. pass csv file path to tcl script' inthe shell script </br>
    ![image](https://github.com/user-attachments/assets/5ddfd9a8-7ec8-4a54-8c9a-29cdd13dfa92)
    </br>check the validity of the arguments in tcl script and exit if not correct
    ![image](https://github.com/user-attachments/assets/32f1320d-68e9-44c7-b027-52c28f61bd47)
    
 2. read csv file containts to a matrix using tcl command - this requires csv and struct: : matrix packages to be used, this code below saves the csv file containts to the matrix named 'm'</br>
   ![image](https://github.com/user-attachments/assets/e9274664-d673-4233-b325-c73d77008e06)

 3. conert the matrrix to the indexed array by linking matrix m to the array my_arr</br>
    ![image](https://github.com/user-attachments/assets/910d8eda-21ca-43fa-8427-cfb2f3e899f1)
    </br> assign varible 'columns' and 'rows' with number of columns and rows present in the 'my_array'
 
 4. use while loop to acess  array elements, read row by row and extact first column cell containts and remove the spaces between the strings to make them used as valid variable names. </br>
   ![image](https://github.com/user-attachments/assets/d84d01c0-6773-45a1-889d-2d51446aa32a)
    </br> use map function ( string replace command) to remove spaces from the value of the string in the first row ( row 0)  of csv file / matrix /array </br>
          ![image](https://github.com/user-attachments/assets/bb9c6bbb-e603-47a5-baac-58eb41bc84b7)
    </br>'varname' can be assigned with the value of the 2D 'array' element located at '(col# ,row#)' by using `set varname $array(col#, row#)`
    
    above commands generate the varible name automatically from the string read from the csv files first column ( column0) </br> and assigns the value of the  varibale to the string read from the column 1 of the csv file.
   </br> the normalize function is used for normalizing the paths to absolute paths and not have relative paths ( ./ or ~/)and both the varibale name and t he  value are autogenerated using strings from the column0 and and column 1  of the csv file for second row onwards ( row1) </br>
   ![image](https://github.com/user-attachments/assets/d53f5f0d-10fc-4ce9-bbd3-0d4c32b450af) </br>

here is the output of the script showing autogenerated variables assigned with various paths 
   ![image](https://github.com/user-attachments/assets/1adeacc5-2bb3-4ed7-b6f4-bf2d843414d9)


 

### 2. Check if the files / folder paths provided by user in a csv file ( second column)  does exists 
   Script checks for the correctness of the file paths </br>
   ![image](https://github.com/user-attachments/assets/b6b79f88-36b4-47af-8aed-9843e3ef8c8e)
   
   </br> check that file exists or not the below function returns boolean output ( yes / no) , exit if files do not exist.
   </br> command to check if file exists   `file exists <file_path>`
   
   </br> check if the directory paths are pointing to the directories using `file isdirectory <diectory_path>`
   
   </br> if output directory does not exists crete it using  `file mkdir <directory_path>`</br>
      
### 3. convert the csv containt table to the sdc format acceptable by syntheis and PnR tool
   target of this task is to convert the constraints csv file to the standard sdc file which is understood by the synthesis tool
   the csv file has various sections for he constraints like clock, Input, and output, with various parmaters for it defined like early delay, late_delay, load, rise fall time 
   Each input, output and clock constraints need to be handlled differently. The csv file of the constraints looks like below</br>
   ![image](https://github.com/user-attachments/assets/d7f9f751-be26-4f78-92b6-1afc7875e61d)

   a. Reading csv file to matrix , set variables for the number of rows and columns in the matrix
   ![image](https://github.com/user-attachments/assets/6f2a8038-6a41-4ead-a08d-477af924be30)
   
   b. identify the ( col, row) address of the various key words like CLOCKS, fequency and duty cycle
   search all provides the ( columne , row) address / index of the cells which contains text CLOCKS
   the 'lindex' provid the zeroth element of the list, which is row index provided by search command </br>
   ![image](https://github.com/user-attachments/assets/8b786c23-8002-4763-9d7d-07e5e41dd286)

   c. simillar search operation is done for Inputs and Outputs, this will provide the start address /index / row number 
   for the Input and Outputs in the variables 
   ![image](https://github.com/user-attachments/assets/78d12882-833c-466c-9311-ab68eec00ed0)

   The output of the part of the script is shown below, wheere we now get values for various variables
   ![image](https://github.com/user-attachments/assets/92a6af91-99b7-4186-865b-2ff337fc2443)

# Day3
## Generate SDC from CSV, Clock and Input Constraints
The intention here is to pick the various values from the csv file and  and write a new file with sdc constraints whcih has /port/ signal /variabe names picked from the excel file and corrosponding values of the constraints.
The csv file is input and the sdc constraints on the bottom is the output </br>
![image](https://github.com/user-attachments/assets/a5082b7e-a004-45e1-a6b9-2485dab9bcee)

A Rectangular area is selected for the search in a spreadsheet, the boundries of these rectangle are defined by values of various variables like 'number of columns', 'clock_start', 'input_ports_start 
![image](https://github.com/user-attachments/assets/5b23f42e-d7a2-4c55-892c-969337d16ad0)

The part of the code which does this is shown below </br>
![image](https://github.com/user-attachments/assets/c4918d29-a25d-49c9-8c8a-24648bd4dd29)

Lets see How it works </br>
   a.   Text 'early_rise is searched in a rectangle specified by the digonal co ordinates ( col, row) using the following , this command provides list of the co ordinates {c1,r1} {c2,r2} ... {cn,Rn} at which  the search text 'early_rise_delay' matches to the cell containts </br>
      `[constraints search rect $clock_start_column $clock_start [expr {$number_of_columns-1}] [expr {$input_ports_start-1}]  early_rise_delay]`

   b. out of this list index of the first matched cell is extracted using lindex command which will provide c1 R1 as a output,another  lindex operation will provide c1 as the output and then variable early_clockrise_delay_start is assigned with thei value c1 ( 3 in our case) which is the coumn             number where the early delay entry starts </br>

   c. This  process is repeated to find out the start columns for the other variables

   d. new sdc file is generated and sdc constraints for clock are written to the file using folloing code , $Designname.sdc file is opened in write mode and a variable sdc_file is assigned with the file handler
      various sdc clock constraints like create_clock , set clock_transition, set clock_delay etc are appended to the file with appropriate sdc constraint syntax, using puts  -nonewline $sdcfile "sdc_constraint"
      get cell command is used on the constraints matrix to retive cell values, this is repeated till clock constraints are generated for all clock ports 
      ![image](https://github.com/user-attachments/assets/63fdb306-3297-4734-a264-6e72f50816fa)

   e. similar to  step a &b which was carried on clock ports the input port start indices are assigned with its column number, part of code perfroming this is shown below </br>
        ![image](https://github.com/user-attachments/assets/d4fbd9d3-e4da-45d8-9b73-545aac8db195)

   f. for input and output constraints ,one needs to identify that which port is a bus , and then sdc constraints * postfix ( wildcard) needs to be used to apply constraints to all bits of the bus.
      


 



### 1. Read all .v files from the verilog netlist folder and arange it in Yosys understandable format
### 2. Create a syntheis script for converting rtl netlist to gatelvel netlist using yosys tool ( Format 2)






        
