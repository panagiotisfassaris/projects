#include <stdio.h>
#include <string.h>
#include <stdbool.h>


void welcome(char name[]){
    printf("\nHello '%s'!\n", name);
}

void menu(){
    printf("\n      'PF Bank'");
    printf("\n---------MENU---------\n");
    printf("1. Withdraw Amount ($)\n");
    printf("2. Deposit Amount ($)\n");
    printf("3. View Balance ($)\n");
    printf("4. Exit\n");
    printf("----------------------\n");
}

void inp(){
    printf("> ");
}


int main(){
    int atmOpt;
    char name[25];
    float withdr = 0;
    float depos = 0;
    float bal = 1435;
    char receipt;
    bool menuView = true;
    char optAfter;
    bool notQuit=true;
    char ans;
    
    printf("\nPlease type in your full name: \n");
    inp();
    
    fgets(name, 25, stdin);
    name[strlen(name) -1] = '\0';

    welcome(name);
    menu();
    inp();
    scanf("%d", &atmOpt);
    while (atmOpt<1 ||atmOpt>4){
        printf("\nWrong option, please try again:\n");
        inp();
        scanf("%d", &atmOpt);
    }
    while (notQuit && (atmOpt >= 1 && atmOpt <= 3)){
        if (atmOpt==4){
            notQuit=false;
        }
        //Withdrawal option
        else if (atmOpt==1){
            printf("\nType in the amount for withdrawal:\n");
            inp();
            printf("$");
            scanf("\n%f", &withdr);
        
            while (withdr>bal){
                printf("Amount exceeds available '$':\n");
                inp();
                printf("$");
                scanf(" %f", &withdr);
            }
            
            printf("\nProceed? (Y/N):\n");
            inp();
            scanf(" %c", &ans);
            while (ans!='Y' && ans!='y' && ans!='N' && ans!='n'){
                printf("\nWrong input, please try again (Y/N):\n");
                inp();
                scanf("\n%c", &ans);
            }
            //Subtract from balance.
            bal-=withdr;
            
            if (ans=='Y' || ans=='y'){
                //printf("\n---------MENU---------\n");
                printf("\n-----WITHDRAWING MONEY-----\n");
                printf(">Done. Please grab the money\nfrom the machine.\n");
                printf(">Would you like a receipt\nfor this transaction? (Y/N)\n");
                printf("----------------------------\n");
                inp();
                scanf("\n%c", &receipt);
            
                while(receipt!='Y' && receipt!='y' && receipt!='N' && receipt!='n'){
                    printf("\nWrong input, please try again (Y/N):\n");
                    inp();
                    scanf("\n%c", &receipt);
                }
                if (receipt=='Y' || receipt=='y'){
                    printf("\n---------RECEIPT---------\n");
                    printf(">Withdrawn amount: $%.2f\n", withdr);
                    printf("-------------------------\n");
                }
            }
        //Main Menu/Quit question
        printf("\nPress (Q) to quit:\n");
        printf("Press (M) to get redirected\nto the main menu:\n");
        inp();
        scanf("\n%c", &optAfter);
        if (optAfter=='Q' || optAfter=='q'){
            atmOpt=4;
            menuView=false;
        }
        else if (optAfter=='M' || optAfter=='m'){
            menuView=true;
        }
            
        if (menuView==true){
            menu();
            inp();
            scanf("%d", &atmOpt);
        }
        }
            //Depositing Option
        else if (atmOpt==2){
            printf("\nType in the amount for deposit:\n");
            inp();
            printf("$");
            scanf(" %f", &depos);
        
            while (depos>1000){
                printf("Amount exceeds max deposit value:\n");
                inp();
                printf("$");
                scanf("\n%f", &depos);
            }
            
            printf("\nProceed? (Y/N):\n");
            inp();
            scanf(" %c", &ans);
            while (ans!='Y' && ans!='y' && ans!='N' && ans!='n'){
                printf("\nWrong input, please try again (Y/N):\n");
                inp();
                scanf("\n%c", &ans);
            }
            //Add to balance.
            bal+=depos;
            
            if (ans=='Y' || ans=='y'){
                printf("\n------DEPOSITING MONEY------\n");
                printf(">Please put the money\nin the machine.\n");
                printf(">Would you like a receipt\nfor this transaction? (Y/N)\n");
                printf("----------------------------\n");
                inp();
                scanf("\n%c", &receipt);
            
                while(receipt!='Y' && receipt!='y' && receipt!='N' && receipt!='n'){
                    printf("\nWrong input, please try again (Y/N):\n");
                    inp();
                    scanf("\n%c", &receipt);
                }
                if (receipt=='Y' || receipt=='y'){
                    printf("\n--------RECEIPT--------\n");
                    printf(">Deposited amount: $%.2f\n", depos);
                    printf("-----------------------\n");
                }
            }
            else if (ans=='N' || ans=='n'){
                notQuit=false;
                menuView=false;
            }
        
        else if (atmOpt==3){
            printf("\nBalance: $%.2f", bal);
        }
        
        //Main Menu/Quit question
        printf("\nPress (Q) to quit:\n");
        printf("Press (M) to get redirected\nto the main menu:\n");
        inp();
        scanf("\n%c", &optAfter);
        if (optAfter=='Q' || optAfter=='q'){
            atmOpt=4;
            menuView=false;
        }
        else if (optAfter=='M' || optAfter=='m'){
            menuView=true;
        }
            
        if (menuView==true){
            menu();
            inp();
            scanf("%d", &atmOpt);
        }
    }
    }
    
    printf("\nThank you for using our services.\nBank of 'PF'\nAll rights reserved");
    return 0;
}
    
    
