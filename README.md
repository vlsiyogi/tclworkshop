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
genrate a command which will take the csv file path from user, check if path is valid and file exists and then passes that file to the tcl script
script also provides help  about command by using `./yogisynth -help`
</br>

Generate a file called yogisynth using linux terminal using `gedit yogisynth` or `gvim yogisynth` and it shall have below segments of coads to  carryout various desired functionality
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

Lets look into the details of each step 

### 1. Create the variables using tcl scrip by reading the CSV file cell containts ( first columns)
### 2. Check if the files / folder paths provided by user in a csv file ( second column)  does exists 
### 3. convert the csv containt table to the sdc format acceptable by syntheis and PnR tool
### 4. Read all .v files from the verilog netlist folder and arange it in Yosys understandable format
### 5. Create a syntheis script for converting rtl netlist to gatelvel netlist using yosys tool ( Format 2)






        
