# phone_book

#include <stdio.h>
#include <conio.h>
#include <windows.h>
#include <string.h>

void options(void)
{
    printf("1. Create contact\n2. Delete Contact\n3. Show All Contact\n4. Search Contact\n5. Exit\n");
}

void write(){
    char name[30];
    long long number;

    FILE *fp = fopen("Contacts.txt","a");

    if(fp == NULL){
        printf("Error opening file\n");
        exit(0);
    }

    printf("Enter number : ");
    scanf("%lld", &number);

    fflush(stdin);

    printf("Enter Name: ");
    scanf("%[^\n]", name);

    fprintf(fp, "%s\t%lld\n", name, number);
    printf("Creating Please wait!\n");
    Sleep(2000);
    printf("Contact created succesfully\n");
    fclose(fp);
}

void display(){
    char name[30];
    long long number;

    FILE *ptr = fopen("Contacts.txt","r");

    if(ptr == NULL){
        printf("Error opening file\n");
        exit(0);
    }

    printf("loading...\n\n");
    Sleep(5000);

    while(!feof(ptr)){
        fscanf(ptr,"%s\t%lld\n",name,&number);
        printf("%s\t%lld\n",name,number);
    }
}

void search(){
    int choice;
    char sear_name[30];
    long long sear_number;
    char name[30];
    long long number;

    FILE *fp = fopen("Contacts.txt","r");

    if(fp == NULL){
        printf("Error opening file\n");
        exit(0);
    }

    printf("1) Search by number\n2) Search by name\n");
    scanf("%d",&choice);

    switch(choice){
        case 1:{
            int flag=0;
            printf("Enter the number: ");
            scanf("%lld",&sear_number);

            printf("Searching please wait!\n\n");
            Sleep(3000);

            while(!feof(fp)){
                fscanf(fp,"%s\t%lld\n",name,&number);
                if(number == sear_number){
                    printf("%s\t%lld\n",name,number);
                    flag=1;
                    break;
                }
            }

            if(flag == 0){
                printf("Not found\n");
            }
            break;
        }

        case 2:{
            int flag1=0,res;

            printf("Enter name: ");
            fflush(stdin);
            scanf("%[^\n]",sear_name);

            printf("Searching please wait!\n\n");
            Sleep(3000);

            while(!feof(fp)){
                fscanf(fp,"%s\t%lld\n",name,&number);
                res = strcmp(sear_name,name);

                if(res == 0){
                    printf("%s\t%lld\n",name,number);
                    flag1=1;
                }
            }

            if(flag1 == 0){
                printf("Not found\n");
            }
            break;
        }

        default:{
            printf("Wrong Input\n");
            break;
        }
    }
}
//void delete();

void main(){
    int opt;
    char again = 'y';
    printf("\n\n\n.....Welcome....\n\n");
    while(again == 'y'){
        options();

        printf("\nEnter your choice: ");
        scanf("%d", &opt);

        switch(opt)
        {
        case 1:
        {
            write();
            break;
        }
        /*case 2:
        {
            delete();
            break;
        }*/
        case 3:{
            display();
            break;
        }
        case 4:{
            search();
            break;
        }
        case 5:{
            exit(0);
            break;
        }
        default:{
            printf("Wrong choice!Try again\n");
        }
        }

        fflush(stdin);

        printf("Want to run again y/n: ");
        scanf("%c", &again);
    }
}
