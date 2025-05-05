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

### 2. Generate "yogisynth" command using bash / tshell script 
genrate a command which will take the csv file path from user, check if path is valid and file exists and then passes that file to the tcl script
script also provides help  about command by using `./yogisynth -help`
</br>
Generated file should look like below: <br>
Generate a file called yogisynth using linux terminal using `gedit yogisynth` or `gvim yogisynth` and it shall have below segments of coads to  carryout various desired functionality

1. check number of arguments is one or not, otherwise exit the command </br>
   ![image](https://github.com/user-attachments/assets/6feaf19d-4916-48de-aff9-c63acf63f4e1)

2. check if user has provided -help argument or the file path, if path or file, check if it exists </br>
   ![image](https://github.com/user-attachments/assets/9abc91d4-7d74-494c-98bf-06e84583aa26)

3. provide useful information to user by adding the help for using the command `./yogisynth <csv_filepath>` </br>
   ![image](https://github.com/user-attachments/assets/31aa6272-68fe-4efd-a6ce-600136d9e514)

4. if user provides one argument and it is not '-help' and the file  or path exists, pass tat to the tcl script yogisynth.tcl </br>
   ![image](https://github.com/user-attachments/assets/d99692a2-b8f2-424b-87a4-36fb90e1b374)






        
