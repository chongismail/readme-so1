## COMPUTERIZED TELEPHONE DIRECTORY
By our developed project, we will provide a user friendly system.
our system will display a menu that have several options such as 
search, insert, delete, sort, display and exit.

our system will show some easy instruction to allow some nedeed input from the user. our system apply the concept of quick method in sorting feuture. it sort based on decending alphabets (from A to Z). this program apply concept the __ concept for insert and delete data. 


## Usage/Examples

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_SIZE 100

typedef struct {
    char name[100];
    char number[100];
} PhoneRecord;

PhoneRecord phoneDirectory[MAX_SIZE];
int count = 0;
```
This section of the code include
s the necessary header files and defines some constants and a data structure:

1. `#include <stdio.h>`: This line includes the standard input/output library header file, which provides functions for input and output operations such as reading from and writing to the console.

2. `#include <stdlib.h>`: This line includes the standard library header file, which provides functions for dynamic memory allocation, program termination, and other general-purpose functions.

3. `#include <string.h>`: This line includes the string library header file, which provides functions for string manipulation, such as comparing strings, copying strings, and finding substrings.

4. `#define MAX_SIZE 100`: This line defines a constant `MAX_SIZE` with a value of 100. It represents the maximum number of phone records that can be stored in the phone directory. By using a constant, the code can easily change the maximum size of the directory by modifying this line.

5. `typedef struct { ... } PhoneRecord;`: This line defines a new data type `PhoneRecord` using a struct. The `PhoneRecord` struct has two members: `name` and `number`, each represented by a character array of size 100. This struct represents a single phone record in the directory, containing the name and associated phone number.

By using the `typedef` keyword, the struct definition is associated with the `PhoneRecord` type, allowing us to use `PhoneRecord` as a data type instead of writing `struct PhoneRecord` every time we declare a variable of this type.

The line `PhoneRecord phoneDirectory[MAX_SIZE];` declares an array called `phoneDirectory` of type `PhoneRecord` with a size of `MAX_SIZE`. The `PhoneRecord` type is a struct defined earlier in the code, representing a phone record with a name and a number.

The size of the array is specified by the constant `MAX_SIZE`, which is defined earlier in the code as 100. Therefore, `phoneDirectory` can hold a maximum of 100 phone records.

The line `int count = 0;` declares an integer variable called `count` and initializes it with a value of 0. This variable is used to keep track of the current number of phone records stored in the `phoneDirectory` array.

Initially, when the program starts, the `count` is set to 0 because no records have been added yet. As records are inserted into the `phoneDirectory` array, the `count` variable is incremented. It allows the program to know the number of valid records in the array and prevents accessing or modifying invalid or empty memory locations beyond the actual number of records stored.

By maintaining the `count` variable, the program can easily keep track of the number of records and perform operations accordingly, such as preventing inserting more records when the array is full or avoiding accessing non-existing records during searches or deletions.

for the beginning we will start with function displayMenu(). this function created to display our menu for our user. 
```c
void displayMenu() {
    printf("<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                                                               ****WELCOME TO OUR COMPUTERIZED TELEPHONE DIRECTORY****                                                                           >");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                                                                   Welcome to our computerized telephone directory!                                                                              >");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                                         ur code provides a simple and efficient way to access contact information with just a few clicks.                                                       >");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                                                  Say goodbye to flipping through pages or struggling to find the right number.                                                                  >");
    printf("<                                                                                                                                                                                                                 >");
    printf("<                                       With our user-friendly interface,you'll have instant access to a vast database of phone numbers, making your search quick and hassle-free                                 >");
    printf("<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>");
    printf("                                                                                         _____________________________________");
    printf("\n\t\t\t\t\t\t\t\t\t\t\t||---- Telephone Directory Menu -----||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||1.|Search                          ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||2.|Insert                          ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||3.|Delete                          ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||4.|Sort                            ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||5.|Display                         ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t||6.|Exit                            ||\n");
    printf("\t\t\t\t\t\t\t\t\t\t\t---------------------------------------\n");
```
This is our menu with some design for displaying the menu. we have create a border. we also put some description to welcome our customer. 

The specific line you mentioned is the printf() statement used to display the menu of the telephone directory. It prints a series of strings and characters that form the visual representation of the menu on the console
```c
printf("<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>");
```
This line consists of a long string of angle brackets (< and >) repeated multiple times. It creates a visual border at the top and bottom of the menu, giving it a decorative appearance
```c
printf("\n\t\t\t\t\t\t\t\t\t\t\t||---- Telephone Directory Menu -----||\n");
printf("\t\t\t\t\t\t\t\t\t\t\t||1.|Search                          ||\n");
printf("\t\t\t\t\t\t\t\t\t\t\t||2.|Insert                          ||\n");
printf("\t\t\t\t\t\t\t\t\t\t\t||3.|Delete                          ||\n");
printf("\t\t\t\t\t\t
```
this segment of code is to display a horizontal line of underscores that separates the menu's title from the menu options. It creates a visual distinction between the two sections.

for the next function is to search the record based on user input
```c
void searchRecord(char* name) {
```
This line defines a function named searchRecord that takes a pointer to a character (char*) as a parameter. The parameter represents the name to search for in the phone records
```c
    int found = 0;
```
This line declares an integer variable named found and initializes it to 0. This variable will be used to keep track of whether a record with the given name has been found.
```c
    for (int i = 0; i < count; i++) {
```
This line starts a for loop that iterates over the phone records in the phoneDirectory array. The loop variable i is initialized to 0, and the loop will continue as long as i is less than the count variable.
```c
    if (strcmp(phoneDirectory[i].name, name) == 0) {
```
This line compares the name parameter with the name field of the current phone record (phoneDirectory[i].name). It uses the strcmp() function, which returns 0 if the two strings are equal. If a match is found, the if condition is true.
```c
            printf("Record found:\n");
            printf("Name: %s\n", phoneDirectory[i].name);
            printf("Number: %s\n", phoneDirectory[i].number);
```
These lines print the record details of the found record. It displays a message indicating that the record is found, followed by the name and number of the record.
```c
            found = 1;
            break;
```
These lines set the found variable to 1 to indicate that a record with the given name is found. The break statement is used to exit the loop early since the record has been found.
```c
                if (!found)
        printf("Record not found.\n");
```
This if condition checks if the found variable is still 0 after the loop. If found is 0, it means that no matching record was found in the loop. In that case, it prints a message indicating that the record was not found.

In summary, the searchRecord function takes a name as input and iterates over the phone records stored in the phoneDirectory array. It compares the input name with the names in the records. If a match is found, it prints the record details. If no match is found, it displays a message indicating that the record was not found.

we continue to the next function that is insertRecord(). this function to allow our code to allow user to take the input from user and make sure our system insert feuture perform well.
```c
           void insertRecord(char* name, char* number) {
```
his line declares the insertRecord function, which takes two arguments: name (a pointer to a character array representing the name of the record) and number (a pointer to a character array representing the phone number).
```c
               if (count >= MAX_SIZE) {
        printf("Directory is full. Cannot insert more records.\n");
        return;
    }

```
This if statement checks if the current number of records (count) is equal to or greater than the maximum size of the directory (MAX_SIZE). If this condition is true, it means that the directory is already full and no more records can be inserted. In that case, the function prints an error message using printf() and returns, exiting the function.
```c
    strcpy(phoneDirectory[count].name, name);
    strcpy(phoneDirectory[count].number, number);
```
These two lines use the strcpy() function to copy the name and number strings into the corresponding fields of the phoneDirectory array at the index specified by count. It effectively inserts the new record into the directory.
```c
    count++;
    printf("Record inserted successfully.\n");
```
After successfully inserting the record, the count variable is incremented to reflect the addition of a new record. The function then prints a success message using printf() to indicate that the record was inserted successfully.

Overall, this insertRecord() function checks if the directory has reached its maximum capacity and if so, it returns an error. Otherwise, it inserts a new record into the directory by copying the name and number strings, increments the record count, and provides a success message.

the next function is deleteRecord(). this function is to ensure that our program have ability to delete a record chosen by user.
```c
void deleteRecord(char* name) {
```
This line defines a function named deleteRecord that takes a pointer to a character (char*) as a parameter. The parameter represents the name of the record to be deleted.
```c
    int found = 0;
```
This line declares an integer variable found and initializes it to 0. This variable will be used to track whether a matching record is found or not.
```c
        for (int i = 0; i < count; i++) {
```
This line starts a for loop that iterates over the elements of the phoneDirectory array. The loop variable i is initialized to 0, and the loop continues as long as i is less than the count variable, which represents the number of records stored in the directory.
```c
    if (strcmp(phoneDirectory[i].name, name) == 0) {
```
This line compares the name parameter with the name field of the i-th element in the phoneDirectory array using the strcmp() function. If the comparison returns 0 (indicating a match), the condition is true, and the following block of code is executed.
```c
    found = 1;
```
This line sets the found variable to 1, indicating that a matching record has been found.
```c
   for (int j = i; j < count - 1; j++) {
```
This line starts another for loop with a new loop variable j, which is initialized to the value of i. The loop iterates from j to count - 1, which represents the range of records that need to be shifted to fill the gap left by the deleted record.
```c
  strcpy(phoneDirectory[j].name, phoneDirectory[j + 1].name);      strcpy(phoneDirectory[j].number, phoneDirectory[j + 1].number);
```
These two lines use the strcpy() function to copy the name and number fields from the next record (j+1) to the current record (j). This effectively shifts the records one position to the left, overwriting the record to be deleted.
```c
     count--;
```
This line decrements the count variable to reflect the removal of one record from the directory.
```c
               printf("Record deleted successfully.\n");

```
This line prints a message to indicate that the record has been deleted successfully.
```c
         if (!found)
        printf("Record not found.\n");
```
This if statement checks the value of the found variable. If it is still 0, indicating that no matching record was found, it prints a message to indicate that the record was not found.
```c
    int compareNames(const void* a, const void* b) {
```
This line defines a comparison function named compareNames. The function takes two const void* parameters, a and b, which represent pointers to generic objects.
```c
        const PhoneRecord* recordA = (const PhoneRecord*)a;
    const PhoneRecord* recordB = (const PhoneRecord*)b;
```
These two lines create two pointers to PhoneRecord objects (recordA and recordB) and cast the generic void* pointers to const PhoneRecord*. This allows the function to access the name field of the PhoneRecord objects.
```c
        return strcmp(recordA->name, recordB->name);

```
This line compares the name fields of the PhoneRecord objects pointed to by recordA and recordB using the strcmp() function. It returns the result of the comparison, which will be a negative value if recordA->name is less than recordB->name, 0 if they are equal, or a positive value if recordA->name is greater than recordB->name. This function is used for sorting the phone records based on their names.

for the fourth function is sortRecord(). to sort our data thatvwe have store.
```c
    void sortRecords() {
```
 This line defines a function named sortRecords that takes no arguments and returns void, indicating that it does not return a value.
 ```c
 qsort(phoneDirectory, count, sizeof(PhoneRecord), compareNames);
```
This line calls the qsort() function from the standard library to sort the phoneDirectory array. The arguments passed to qsort() are:

phoneDirectory: The array to be sorted.

count: The number of elements in the array.

sizeof(PhoneRecord): The size of each element in bytes. This is calculated using the sizeof operator and provides the size of the PhoneRecord struct.

compareNames: A pointer to the comparison function that will be used to determine the order of the elements during sorting. This function compares the names of two PhoneRecord structs.
```c
    printf("Records sorted successfully.\n");
```
This line prints a message indicating that the records have been sorted successfully. It uses the printf() function to display the message on the console.

for the next function is displayRecord(). this function is to display all of our data store. it will display the latest data after the execution of some process such as sort, insert or delete some data (that some process happened depend on user).
```c
    void displayRecords() {
```
This line just indicates the start of the function named. displayRecords() which doesn't take any arguments and doesn't return any value.
```c
    printf("|Phone Directory: |\n");
```
This line prints a header indicating the title of the phone directory. The vertical bars (|) are used for visual formatting.
```c
    for (int i = 0; i < count; i++) {
```
This line starts a loop that iterates through each phone record in the phoneDirectory array. The loop variable i is initialized to 0 and continues as long as i is less than the count variable (which represents the number of records in the directory). After each iteration, i is incremented by 1.
```c
   printf("|Name: %s\t\t\t|\n", phoneDirectory[i].name);
```
This line prints the name of the current phone record at index i in the phoneDirectory array. The %s format specifier is used to print a string, and phoneDirectory[i].name provides the actual string value.
```c
    printf("|Phone Number: %s\t|\n", phoneDirectory[i].number);
```
This line prints the phone number of the current phone record at index i in the phoneDirectory array. Similar to the previous line, the %s format specifier is used to print a string, and phoneDirectory[i].number provides the actual string value.

for the last explanation we will explain our main() function
```c
   int main() {
```
This line marks the beginning of the main function, which is the entry point of the program.
```c
   int choice;, char name[50];, char number[15];
```
Declares an integer variable named choice to store the user's menu choice.  Declares a character array named name with a size of 50. It is used to store the name entered by the user. Declares a character array named number with a size of 15. It is used to store the phone number entered by the user.
```c
    do {
```
Starts a do-while loop. The loop will continue until the user chooses to exit the program.
```c
   displayMenu();
```
Calls the displayMenu() function to show the menu options to the user.
```c
   switch (choice) {
```
Starts a switch statement to determine the action based on the user's choice.
```c
    case 1:  
```
If the value of choice is 1, execute the following block of code
```c
  printf("Enter name to search: ");
```
Displays a prompt asking the user to enter a name for searching.
```c
  scanf("%s", name);
```
Reads a string input from the user and stores it in the name variable.
```c
 searchRecord(name);
```
Calls the searchRecord() function, passing the name variable as an argument.
```c
  break;
```
Ends the current case and exits the switch statement.
```c
    case 2:  
```
If the value of choice is 2, execute the following block of code.
```c
    printf("Enter name to insert: "); 
```
Displays a prompt asking the user to enter a name for insertion.
```c
   scanf("%s", name);
```
Reads a string input from the user and stores it in the name variable.
```c
   printf("Enter number: ");
```
Displays a prompt asking the user to enter a phone number.
```c
   scanf("%s", number);
```
Reads a string input from the user and stores it in the number variable.
```c
    insertRecord(name, number);
```
 Calls the insertRecord() function, passing the name and number variables as arguments.
```c
    break;  
```
 Ends the current case and exits the switch statement.
```c
   case 3:  
```
 If the value of choice is 3, execute the following block of code.
```c
   printf("Enter name to delete: ");
```
Displays a prompt asking the user to enter a name for deletion.
```c
   scanf("%s", name);
```
Reads a string input from the user and stores it in the name variable.
```c
    deleteRecord(name); 
```
 Calls the deleteRecord() function, passing the name variable as an argument.
```c
    break; 
```
Ends the current case and exits the switch statement.
```c
   case 4:
```
 If the value of choice is 4, execute the following block of code.
```c
    sortRecords();
```
 Calls the sortRecords() function to sort the phone records.
 ```c
    break;
```
Ends the current case and exits the switch
```c
    case 5:
```
If the value of choice is 5, execute the following block of code.
```c
    displayRecords();
```
Calls the displayRecords() function to display the phone records.
```c
   break;
```
```c
    case 6:
```
If the value of choice is 6, execute the following block of code.
```c
   printf("Exiting program.\n");
```
Displays a prompt telling the user that they are exiting the program.
```c
   break;
```
Ends the current case and exits the switch.
```c
   default;
```
if user insert other than options provided.they will directly assumed to choose this default option.
```c
  printf("Invalid choice. Please try again.\n");
```
program will automaticly display this sentence if user insert input other than number in the menu.
```c
   break;
```
Ends the current case and exits the switch.
```c
    } while (choice != 6);
```
if input not same with 6. program will execute the defult case.
```c
    return 0;
}
```
represent that the program was completely done run their task.

## Running Instruction

1. First step is user should select the insert function at least two times

2. Select what function that you either want to search, delete, sort, display or exit.

3. Insert all of the inputs that ask by the program. 

4. Continue step 2 and 3 until you finish and select option number 6 to exit the program.

5. make sure to select options that available at the menu.

