# Assignment-in-c-
Practical 
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
    printf("Enter the number of employees: ");
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
