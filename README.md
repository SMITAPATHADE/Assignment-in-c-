# Assignment-in-c-
Practical 1


#include <stdio.h>

#include <string.h>

#define MAX 100  

struct Date 

{

    int day, month, year;

};

union Employee 

{

    int id;

    char name[50];

    struct Date joiningdate;

};

int main() 

{

    union Employee employees[MAX];  

    struct Date birthdates[MAX];   
 
    int n, i, searchMonth;

    printf("Enter the number of employees:
");

    scanf("%d", &n);

    for (i = 0; i < n; i++) 

{

        printf("\nEnter details for Employee %d:\n", i + 1);

        printf("Enter Employee ID: ");

        scanf("%d", &employees[i].id);

        printf("Enter Employee Name: ");

        scanf(" %[^\n]s", employees[i].name); 

        printf("Enter Joining Date (DD MM YYYY): ");

        scanf("%d %d %d", &birthdates[i].day, &birthdates[i].month, &birthdates[i].year);

    }

    printf("\nEnter the month to search for employees with the same joining month: ");

    scanf("%d", &searchMonth);

    printf("\nEmployees who joined in month %d:\n", searchMonth);

    for (i = 0; i < n; i++)

 {

        if (birthdates[i].month == searchMonth) 

{

            printf("\nEmployee ID: %d\n", employees[i].id);

            printf("Employee Name: %s\n", employees[i].name);

            printf("Joining Date: %02d-%02d-%d\n", birthdates[i].day, birthdates[i].month, birthdates[i].year);

        }

    }

 return 0;

}



practical 2

#include <stdio.h>

#include <string.h>

#define MAX 100  

struct Movie

 {

    char name[50];

    int releaseYear;

    float duration;

};

void sortMovies(struct Movie movies[], int n) 

{

    int i, j;

    struct Movie temp;

for (i = 0; i < n - 1; i++)

 {

        for (j = 0; j < n - 1 - i; j++)

 {

            if (movies[j].releaseYear > movies[j + 1].releaseYear) 

{

                temp = movies[j];

                movies[j] = movies[j + 1];

                movies[j + 1] = temp;

            }

        }

    }

}

int main() 

{

    struct Movie movies[MAX]; 
 
    int n, i;

    printf("Enter the number of movies: ");

    scanf("%d", &n);

    for (i = 0; i < n; i++) 

{

        printf("\nEnter details for Movie %d:\n", i + 1);

        printf("Enter Movie Name: ");

        scanf(" %[^\n]s", movies[i].name); 

        printf("Enter Release Year: ");

        scanf("%d", &movies[i].releaseYear);

        printf("Enter Duration (in minutes): ");

        scanf("%f", &movies[i].duration);

    }

    sortMovies(movies, n);

    printf("\nMovies Sorted by Release Year:\n");

    for (i = 0; i < n; i++) 

{

        printf("\nMovie Name: %s\n", movies[i].name);

        printf("Release Year: %d\n", movies[i].releaseYear);

        printf("Duration: %.2f minutes\n", movies[i].duration);

    }

  return 0;

}

practical 3

#include <stdio.h>
int main() 
{
    char filename[100], ch, currentChar;
    int count = 0;
    printf("Enter the file name: ");
    scanf("%s", filename);
 printf("Enter the character to count: ");
    scanf(" %c", &ch); 
    FILE *file = fopen(filename, "r");
if (file == NULL)  
{
        printf("Error: Could not open file %s\n", filename);
        return 1;
    }
  while ((currentChar = fgetc(file)) != EOF)
 {
        if (currentChar == ch)
 {
            count++;
        }
    }
    fclose(file);
    printf("The character '%c' appears %d times in the file.\n", ch, count);
return 0;
}

practical 4


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Employee 
{
    int emp_number;
    char emp_name[50];
    float emp_salary;
};
void writeEmployeesToFile(int n)
{
    FILE *file = fopen("employee.txt", "w");
    if (file == NULL) 
{
        printf("Error opening file!\n");
        return;
    }
 struct Employee emp;
    for (int i = 0; i < n; i++)
 {
        printf("\nEnter details for Employee %d:\n", i + 1);
        printf("Employee Number: ");
        scanf("%d", &emp.emp_number);
        printf("Employee Name: ");
        scanf(" %[^\n]", emp.emp_name);
        printf("Employee Salary: ");
        scanf("%f", &emp.emp_salary);
 fprintf(file, "%d %s %.2f\n", emp.emp_number, emp.emp_name, emp.emp_salary);
    }
fclose(file);
    printf("\nEmployee details saved successfully to 'employee.txt'.\n");
}
void searchEmployee(int emp_num) 
{
    FILE *file = fopen("employee.txt", "r");
    if (file == NULL) 
{
        printf("Error: Could not open file!\n");
        return;
    }
 struct Employee emp;
    int found = 0;
while (fscanf(file, "%d %s %f", &emp.emp_number, emp.emp_name, &emp.emp_salary) != EOF) 
{
        if (emp.emp_number == emp_num) 
{
            printf("\nEmployee Found:\n");
            printf("Employee Number: %d\n", emp.emp_number);
            printf("Employee Name: %s\n", emp.emp_name);
            printf("Employee Salary: %.2f\n", emp.emp_salary);
            found = 1;
            break;
        }
    }
 if (!found) 
{
        printf("\nEmployee with Number %d not found.\n", emp_num);
    }
  fclose(file);
}
void findHighestSalary() 
{
    FILE *file = fopen("employee.txt", "r");
    if (file == NULL)
 {
        printf("Error: Could not open file!\n");
        return;
    }
 struct Employee emp, highestEmp;
    highestEmp.emp_salary = 0;
  while (fscanf(file, "%d %s %f", &emp.emp_number, emp.emp_name, &emp.emp_salary) != EOF)
 {
        if (emp.emp_salary > highestEmp.emp_salary) 
{
            highestEmp = emp;
        }
    }
fclose(file);
  if (highestEmp.emp_salary > 0)
 {
        printf("\nEmployee with Highest Salary:\n");
        printf("Employee Number: %d\n", highestEmp.emp_number);
        printf("Employee Name: %s\n", highestEmp.emp_name);
        printf("Employee Salary: %.2f\n", highestEmp.emp_salary);
    } else {
        printf("\nNo employees found in the file.\n");
    }
}
int main() 
{
    int choice, n, emp_num;
while (1) 
{
        printf("\nMenu:");
        printf("\n1. Enter Employee Details");
        printf("\n2. Search Employee by Number");
        printf("\n3. Display Employee with Highest Salary");
        printf("\n4. Exit");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);
 switch (choice) 
{
            case 1:
                printf("Enter the number of employees: ");
                scanf("%d", &n);
                writeEmployeesToFile(n);
                break;
            case 2:
                printf("Enter Employee Number to Search: ");
                scanf("%d", &emp_num);
                searchEmployee(emp_num);
                break;
            case 3:
                findHighestSalary();
                break;
            case 4:
                printf("Exiting program...\n");
                exit(0);
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    }
    return 0;
}

end..........