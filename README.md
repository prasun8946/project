#include <stdio.h>
#include <string.h>
#include <stdlib.h>

struct items
{
    char item[20];
    float price;
    int qty;
};

struct orders
{
    char customer[50];
    char date[50];
    int numOfITems;
    struct items itm[50];
};

// functions to genrate bills
void generateBillHeader(char name[50], char date[30])
{
    printf("\n\n");
    printf("\t               ADV. Restaurant");
    printf("\nDate:%s", date);
    printf("\nInvoice To: %s", name);
    printf("\n");
    printf("--------------------------------\n");
    printf("Items\t\t");
    printf("Qty\t\t");
    printf("Total\t\t");
    printf("\n---------------------------------");
    printf("\n\n");
}
void generateBillBody(char item[15], int qty, float price)
{
    printf("%s\t\t", item);
    printf("%d\t\t", qty);
    printf("%.2f\t\t", qty * price);
    printf("\n");
}

void generateBillFooter(float total)
{
    printf("\n");
    float dis = 0.1*total;
    float netTotal=total-dis;
    float cgst=0.09*netTotal,grandTotal=netTotal + 2*cgst;
    printf("----------------------------------------------------------------\n");
    printf("Sub Total\t\t\t%.2f", total);
    printf("\nDiscount @10%s\t\t\t%.2f","%",dis);
    printf("\n\t\t\t\t-----------");
    printf("\nNet Total\t\t\t%.2f", netTotal);
    printf("\nCGST @9%s\t\t\t%.2f", "%",cgst);
    printf("\nSGST @9%s\t\t\t%.2f", "%",cgst);
    printf("\n----------------------------------------------------------------\n");

    printf("\nGrand Total\t\t\t%.2f",grandTotal);

    printf("\n----------------------------------------------------------------\n");
}
int main()
{
    float total;
    int opt, n;
    struct orders ord;

    // dashboard
    printf("\t========================ADV. RESTAURANT========================");
    printf("\n\nplease select your prefered operation");
    printf("\n\n1.Generate Invoice");
    printf("\n2.Show all  Invoice");
    printf("\n3.Search Invoice");
    printf("\n4..Exit");

    printf("\n\nYour choice:\t");
    scanf("%d", &opt);
    fgetc(stdin);
    switch (opt)
    {
    case 1:
        printf("\nplease enter the name of the customer:\t");
        fgets(ord.customer, 15, stdin);
        ord.customer[strlen(ord.customer) - 1] = 0;
        strcpy(ord.date, __DATE__);
        printf("\nPlese enter the number of items:\t");
        scanf("%d", &n);
        ord.numOfITems = n;
        for (int i = 0; i < n; i++)
        {
            fgetc(stdin);
            printf("\n\n");
            printf("please enter the item %d:\t", i + 1);
            fgets(ord.itm[i].item, 15, stdin);
            ord.itm[i].item[strlen(ord.itm[i].item) - 1] = 0;
            printf("Plesse enter the quantity:\t ");
            scanf("%d", &ord.itm[i].qty);
            printf("Plesse enter the unit price:\t ");
            scanf("%f", &ord.itm[i].price);
            total += ord.itm[i].qty * ord.itm[i].price;
        }

        generateBillHeader(ord.customer, ord.date);
        for (int i = 0; i < ord.numOfITems; i++)
        {
            generateBillBody(ord.itm[i].item, ord.itm[i].qty, ord.itm[i].price);
        }
        generateBillFooter(total);
        
    }

    printf("\n\n");

    return 0;
}
