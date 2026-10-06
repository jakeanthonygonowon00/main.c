# main.c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main()
{

    char username[30];
    char password[30];

    int attempts = 0;
    int loginSuccess = 0;

    printf("========================================\n");
    printf("          === SHAKEY'S POS ===\n");
    printf("========================================\n\n");

    printf("Login to continue\n");

    while (attempts < 3)
    {
        printf("\nUsername: ");
        scanf("%29s", username);

        printf("Password: ");
        scanf("%29s", password);

        if (strcmp(username, "jake") == 0 &&
            strcmp(password, "1234") == 0)
        {
            loginSuccess = 1;

            printf("\nLogin successful!\n");
            printf("Cashier: Good day! Welcome to Shakey's!\n");

            break;
        }
        else
        {
            attempts++;

            printf("\nInvalid username or password!\n");

            if (attempts < 3)
            {
                printf("Please try again.\n");
                printf("Attempts remaining: %d\n",
                       3 - attempts);
            }
        }
    }

    if (loginSuccess == 0)
    {
        printf("\nToo many failed attempts.\n");
        printf("Access denied!\n");

        return 0;
    }


    int choice;
    int quantity;
    char again;

    int pepperoniQty = 0;
    int hawaiianQty = 0;
    int chickenQty = 0;
    int spaghettiQty = 0;
    int mojosQty = 0;
    int softdrinkQty = 0;
    int icedTeaQty = 0;

    float pepperoniTotal = 0;
    float hawaiianTotal = 0;
    float chickenTotal = 0;
    float spaghettiTotal = 0;
    float mojosTotal = 0;
    float softdrinkTotal = 0;
    float icedTeaTotal = 0;

    do
    {
        printf("\n========================================\n");
        printf("             SHAKEY'S MENU\n");
        printf("========================================\n");

        printf("\nPIZZAS:\n");
        printf("1 - Pepperoni Pizza       - Php 450\n");
        printf("2 - Hawaiian Pizza        - Php 450\n");

        printf("\nCHICKEN:\n");
        printf("3 - Chicken 'N' Mojos     - Php 350\n");

        printf("\nPASTA:\n");
        printf("4 - Spaghetti              - Php 250\n");

        printf("\nSIDES:\n");
        printf("5 - Mojos                  - Php 180\n");

        printf("\nDRINKS:\n");
        printf("6 - Softdrinks             - Php 80\n");
        printf("7 - Iced Tea               - Php 90\n");

        printf("----------------------------------------\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        if (choice < 1 || choice > 7)
        {
            printf("Invalid menu choice!\n");
        }
        else
        {
            printf("Enter quantity: ");
            scanf("%d", &quantity);

            if (quantity <= 0)
            {
                printf("Invalid quantity!\n");
            }
            else
            {
                switch (choice)
                {
                    case 1:
                        pepperoniQty += quantity;
                        pepperoniTotal += quantity * 450;
                        printf("%d Pepperoni Pizza added.\n",
                               quantity);
                        break;

                    case 2:
                        hawaiianQty += quantity;
                        hawaiianTotal += quantity * 450;
                        printf("%d Hawaiian Pizza added.\n",
                               quantity);
                        break;

                    case 3:
                        chickenQty += quantity;
                        chickenTotal += quantity * 350;
                        printf("%d Chicken 'N' Mojos added.\n",
                               quantity);
                        break;

                    case 4:
                        spaghettiQty += quantity;
                        spaghettiTotal += quantity * 250;
                        printf("%d Spaghetti added.\n",
                               quantity);
                        break;

                    case 5:
                        mojosQty += quantity;
                        mojosTotal += quantity * 180;
                        printf("%d Mojos added.\n",
                               quantity);
                        break;

                    case 6:
                        softdrinkQty += quantity;
                        softdrinkTotal += quantity * 80;
                        printf("%d Softdrinks added.\n",
                               quantity);
                        break;

                    case 7:
                        icedTeaQty += quantity;
                        icedTeaTotal += quantity * 90;
                        printf("%d Iced Tea added.\n",
                               quantity);
                        break;
                }
            }
        }

        printf("\nDo you want to order more? (Y/N): ");
        scanf(" %c", &again);

        again = toupper(again);

    } while (again == 'Y');


    float subtotal;
    float discount = 0;
    float total;

    subtotal = pepperoniTotal +
               hawaiianTotal +
               chickenTotal +
               spaghettiTotal +
               mojosTotal +
               softdrinkTotal +
               icedTeaTotal;


    char discountChoice;

    printf("\n========================================\n");
    printf("              DISCOUNT\n");
    printf("========================================\n");

    printf("Senior Citizen or PWD? (S/P/N): ");
    scanf(" %c", &discountChoice);

    discountChoice = toupper(discountChoice);

    if (discountChoice == 'S')
    {
        discount = subtotal * 0.20;
        printf("Senior Citizen discount applied.\n");
    }
    else if (discountChoice == 'P')
    {
        discount = subtotal * 0.20;
        printf("PWD discount applied.\n");
    }
    else
    {
        discount = 0;
        printf("No discount applied.\n");
    }

    total = subtotal - discount;

    printf("\nSubtotal: Php %.2f\n", subtotal);
    printf("Discount: Php %.2f\n", discount);
    printf("Total:    Php %.2f\n", total);


    int paymentChoice;
    float payment = 0;
    float change = 0;

    printf("\n========================================\n");
    printf("              PAYMENT\n");
    printf("========================================\n");

    printf("Total Amount: Php %.2f\n", total);

    do
    {
        printf("\n1 - Cash\n");
        printf("2 - Card\n");
        printf("3 - E-Wallet\n");

        printf("Enter payment method: ");
        scanf("%d", &paymentChoice);

        if (paymentChoice < 1 || paymentChoice > 3)
        {
            printf("\nInvalid payment method!\n");
            printf("Please choose 1, 2, or 3.\n");
        }

    } while (paymentChoice < 1 || paymentChoice > 3);


    if (paymentChoice == 1)
    {
        do
        {
            printf("\nEnter cash amount: Php ");
            scanf("%f", &payment);

            if (payment < total)
            {
                printf("Insufficient cash!\n");
                printf("Please enter enough money.\n");
            }

        } while (payment < total);

        change = payment - total;

        printf("\nCash payment successful!\n");
        printf("Amount Paid: Php %.2f\n", payment);
        printf("Change:      Php %.2f\n", change);
    }


    else if (paymentChoice == 2)
    {
        char cardNumber[20];

        char validCard[] = "09810103773";

        float cardBalance = 5000.00;

        int cardValid = 0;

        printf("\n========================================\n");
        printf("             CARD PAYMENT\n");
        printf("========================================\n");

        do
        {
            printf("\nEnter card number: ");
            scanf("%19s", cardNumber);

            if (strcmp(cardNumber, validCard) == 0)
            {
                cardValid = 1;

                printf("\nCard accepted!\n");
                printf("Card Number: %s\n", cardNumber);
                printf("Available Balance: Php %.2f\n",
                       cardBalance);
            }
            else
            {
                printf("\nInvalid card number!\n");
                printf("Please enter the correct card number.\n");
            }

        } while (cardValid == 0);

        while (cardBalance < total)
        {
            printf("\nInsufficient card balance!\n");
            printf("Available Balance: Php %.2f\n",
                   cardBalance);

            printf("\nPlease choose another payment method.\n");

            do
            {
                printf("\n1 - Cash\n");
                printf("2 - Try Card Again\n");
                printf("3 - E-Wallet\n");

                printf("Enter choice: ");
                scanf("%d", &paymentChoice);

                if (paymentChoice < 1 || paymentChoice > 3)
                {
                    printf("Invalid choice!\n");
                }

            } while (paymentChoice < 1 || paymentChoice > 3);

            if (paymentChoice == 2)
            {
                do
                {
                    printf("\nEnter card number: ");
                    scanf("%19s", cardNumber);

                    if (strcmp(cardNumber, validCard) == 0)
                    {
                        printf("\nCard accepted!\n");
                        printf("Available Balance: Php %.2f\n",
                               cardBalance);

                        cardValid = 1;
                    }
                    else
                    {
                        printf("\nInvalid card number!\n");
                        cardValid = 0;
                    }

                } while (cardValid == 0);
            }
            else
            {
                break;
            }
        }

        if (paymentChoice == 2 &&
            cardBalance >= total)
        {
            cardBalance = cardBalance - total;

            payment = total;
            change = 0;

            printf("\nCard payment successful!\n");
            printf("Amount Paid: Php %.2f\n", payment);
            printf("Remaining Balance: Php %.2f\n",
                   cardBalance);
        }
    }


    if (paymentChoice == 3)
    {
        float ewalletBalance = 5000.00;

        printf("\n========================================\n");
        printf("           E-WALLET PAYMENT\n");
        printf("========================================\n");

        printf("Available Balance: Php %.2f\n",
               ewalletBalance);

        while (ewalletBalance < total)
        {
            printf("\nInsufficient e-wallet balance!\n");
            printf("Please try another payment method.\n");

            do
            {
                printf("\n1 - Cash\n");
                printf("2 - Card\n");

                printf("Enter choice: ");
                scanf("%d", &paymentChoice);

            } while (paymentChoice != 1 &&
                     paymentChoice != 2);

            if (paymentChoice == 1)
            {
                do
                {
                    printf("\nEnter cash amount: Php ");
                    scanf("%f", &payment);

                    if (payment < total)
                    {
                        printf("Insufficient cash!\n");
                    }

                } while (payment < total);

                change = payment - total;

                break;
            }
            else
            {
                char cardNumber[20];
                char validCard[] = "09810103773";

                float cardBalance = 5000.00;

                int cardValid = 0;

                do
                {
                    printf("\nEnter card number: ");
                    scanf("%19s", cardNumber);

                    if (strcmp(cardNumber, validCard) == 0)
                    {
                        cardValid = 1;

                        printf("\nCard accepted!\n");
                        printf("Available Balance: Php %.2f\n",
                               cardBalance);
                    }
                    else
                    {
                        printf("\nInvalid card number!\n");
                        printf("Please try again.\n");
                    }

                } while (cardValid == 0);

                if (cardBalance >= total)
                {
                    cardBalance -= total;

                    payment = total;
                    change = 0;

                    printf("\nCard payment successful!\n");
                    printf("Remaining Balance: Php %.2f\n",
                           cardBalance);

                    break;
                }
                else
                {
                    printf("\nInsufficient card balance!\n");
                    printf("Returning to payment options.\n");
                }
            }
        }

        if (ewalletBalance >= total)
        {
            ewalletBalance -= total;

            payment = total;
            change = 0;

            printf("\nE-wallet payment successful!\n");
            printf("Amount Paid: Php %.2f\n", payment);
            printf("Remaining Balance: Php %.2f\n",
                   ewalletBalance);
        }
    }


    printf("\n\n========================================\n");
    printf("             SHAKEY'S RECEIPT\n");
    printf("========================================\n");

    if (pepperoniQty > 0)
    {
        printf("Pepperoni Pizza    x%d   Php %.2f\n",
               pepperoniQty, pepperoniTotal);
    }

    if (hawaiianQty > 0)
    {
        printf("Hawaiian Pizza     x%d   Php %.2f\n",
               hawaiianQty, hawaiianTotal);
    }

    if (chickenQty > 0)
    {
        printf("Chicken 'N' Mojos  x%d   Php %.2f\n",
               chickenQty, chickenTotal);
    }

    if (spaghettiQty > 0)
    {
        printf("Spaghetti          x%d   Php %.2f\n",
               spaghettiQty, spaghettiTotal);
    }

    if (mojosQty > 0)
    {
        printf("Mojos              x%d   Php %.2f\n",
               mojosQty, mojosTotal);
    }

    if (softdrinkQty > 0)
    {
        printf("Softdrinks         x%d   Php %.2f\n",
               softdrinkQty, softdrinkTotal);
    }

    if (icedTeaQty > 0)
    {
        printf("Iced Tea           x%d   Php %.2f\n",
               icedTeaQty, icedTeaTotal);
    }

    printf("----------------------------------------\n");

    printf("Subtotal:               Php %.2f\n",
           subtotal);

    printf("Discount:               Php %.2f\n",
           discount);

    printf("TOTAL:                  Php %.2f\n",
           total);

    printf("----------------------------------------\n");

    if (paymentChoice == 1)
    {
        printf("Payment Method: Cash\n");
    }
    else if (paymentChoice == 2)
    {
        printf("Payment Method: Card\n");
    }
    else
    {
        printf("Payment Method: E-Wallet\n");
    }

    printf("Amount Paid:            Php %.2f\n",
           payment);

    printf("Change:                 Php %.2f\n",
           change);

    printf("========================================\n");
    printf("       THANK YOU FOR CHOOSING\n");
    printf("              SHAKEY'S!\n");
    printf("          Have a great day!\n");
    printf("========================================\n");

    return 0;
}
