# TCL WORKSHOP

## AGENDA
### DAY 1: TCL Introduction         
### DAY 2: Aotogeneration of Variable and processing Constraints from CSV    
### DAY 3: Generate SCD from CSV, Clock and Input Constraints
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
    assign varible 'columns' and 'rows' with number of columns and rows present in the 'my_array'
 
 4. use while loop to acess  array elements, read row by row and extact first column cell containts and remove the spaces between the strings to make them used as valid variable names. </br>
   ![image](https://github.com/user-attachments/assets/d84d01c0-6773-45a1-889d-2d51446aa32a)
    </br> use map function ( string replace command) to remove spaces from the value of the string in the first row ( row 0)  of csv file / matrix /array </br>
          ![image](https://github.com/user-attachments/assets/bb9c6bbb-e603-47a5-baac-58eb41bc84b7)
    'varname' can be assigned with the value of the 2D 'array' element located at '(col# ,row#)' by using `set varname $array(col#, row#)`</br>
    above commands generate the varible name automatically from the string read from the csv files first column ( column0) </br> and assigns the value of the  varibale to the string read from the column 1 of the csv file.
   </br> the normalize function is used for normalizing the paths to absolute paths and not have relative paths and both the varibale name and t he  value are autogenerated using strings from the column0 and and column 1  of the csv file for second row onwards ( row1)
    

### 2. Check if the files / folder paths provided by user in a csv file ( second column)  does exists 
### 3. convert the csv containt table to the sdc format acceptable by syntheis and PnR tool
### 4. Read all .v files from the verilog netlist folder and arange it in Yosys understandable format
### 5. Create a syntheis script for converting rtl netlist to gatelvel netlist using yosys tool ( Format 2)






        
