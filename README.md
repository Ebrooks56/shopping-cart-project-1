# shopping-cart-project-1
Find of programming
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;
int main()
{
// constants to store the customer details
const string CUSTOMERNAME = "Jane Smith", USERNAME = "jsmith", PASSWORD = "blue123",
ACCOUNTNUMBER = "123456789", MEMBERLEVEL = "Gold", ADDRESS = "100 W New Haven Ave, Melbourne, FL, 32901";
double storeCredit = 3000.00; // available store credit
const int ITEMS = 3; // number of products
const double SALES_TAX = 6; // sales tax percentage
// arrays to store the details of items available for purchase
string sku[] = {"HF-342", "LK-322", "KF-231"};
string name[] = {"1/2 in Bolt", "1/4 in Nail", "Hammer"};
int itemsInUnit[] = {50, 25, 1};
double pricePerUnit[] = {20.00, 5.75, 15.23};
int quantityOnHand[] = {200, 76, 100};
// variables 
string input_username, input_password, input_sku;
int input_qty;
int itemIndex;
double amount, salesTax, totalDue;
// login and input the username and password
cout << right << setw(20) << " LOGIN" << endl;
cout << "Username: ";
cin >> input_username;
cout << "Password: ";
cin >> input_password;
// validation of  login 
if(input_username == USERNAME && input_password == PASSWORD)
{
// display available products and the details of the products available
cout << endl << right << setw(30) << "ITEMS" << endl;
cout << left << setw(10) << "SKU" << left << setw(20) << "Name" << right << setw(15) << "Items in unit"
<< right << setw(20) << "Price per unit" << right << setw(20) << "Quantity on hand" << endl;
cout << fixed << setprecision(2);
for(int i=0;i<ITEMS;i++)
{
cout << left << setw(10) << sku[i] << left << setw(20) << name[i] << right << setw(10) << itemsInUnit[i]
<< right << setw(20) << pricePerUnit[i] << right << setw(20) << quantityOnHand[i] << endl;
}
// input the sku of the item to purchase
cout << endl << "Enter the SKU of the item to purchase: ";
cin >> input_sku;
itemIndex = -1;
// loop to get the index of the item user wants to purchase
for(int i=0;i<ITEMS;i++)
{
if(sku[i] == input_sku)
{
itemIndex = i;
break;
}
}
if(itemIndex == -1) // invalid sku and display error and exit
cout << "ERROR: Invalid SKU!!!! Terminating the program..." << endl;
else
{
// input the quantity to purchase
cout << "Enter the quantity to purchase: ";
cin >> input_qty;
// validate quantity is valid, else display error message and exit
if(input_qty < 1 || input_qty > quantityOnHand[itemIndex])
cout << "ERROR: Insufficient quantity. Quantity must be between [1, " << quantityOnHand[itemIndex] << "]. Terminating the program..." << endl;
else
{
// compute the total amount due
amount = input_qty * pricePerUnit[itemIndex]; // amount before taxes
salesTax = (amount * SALES_TAX)/100; // sales tax amount
totalDue = amount + salesTax; // total 
// validate user has enough store credit and if not display error message and exit
if(totalDue > storeCredit)
cout << "ERROR: Insufficient store credit!!! Terminating the program..." << endl;
else
{
// deduct the store credit
storeCredit -= totalDue;
//display receipt
cout << endl << "*********************** RECEIPT **************************" << endl;
cout << left << setw(20) << "Customer Name" << ": " << CUSTOMERNAME << endl;
cout << left << setw(20) << "Account Number" << ": " << ACCOUNTNUMBER << endl;
cout << left << setw(20) << "Member Level" << ": " << MEMBERLEVEL << endl;
cout << left << setw(20) << "Address" << ": " << ADDRESS << endl;
cout << "=========================================================================" << endl;
cout << left << setw(20) << "Item SKU" << ": " << input_sku << endl;
cout << left << setw(20) << "Item Name" << ": " << name[itemIndex] << endl;
cout << left << setw(20) << "Items in unit" << ": " << right << setw(10) << itemsInUnit[itemIndex] << endl;
cout << left << setw(20) << "Price per unit" << ": $" << right << setw(8) << pricePerUnit[itemIndex] << endl;
cout << left << setw(20) << "Quantity" << ":" << right << setw(10) << input_qty << endl;
cout << left << setw(20) << "Gross Amount" << ": $" << right << setw(8) << amount << endl;
cout << left << setw(20) << "Sales Tax" << ": $" << right << setw(8) << salesTax << endl;
cout << left << setw(20) << "Total Amount" << ": $" << right << setw(8) << totalDue << endl;
cout << left << setw(20) << "Store Credit" << ": $" << right << setw(8) << storeCredit << endl;
cout << endl << "**** Thank you for your purchase. Have a nice day! ****" << endl;
}
}
}
}
else // Failed Login and  display error message and exit
cout << "ERROR: Invalid USERNAME and/or PASSWORD. " << endl;
return 0;
}
