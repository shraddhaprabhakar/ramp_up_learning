#include <iostream>    **//used for input (cin) and output (cout) , cin is stream extraction and cout is stream insertion.**
#include <string>      **//use this for dealing with string data type which is used to handle texts.**
 
using namespace std;   **//to avoid conflict we use this namespace, rather than writing std everywhere, it organizes the code.**

struct Product {    **//In C++, when we declare a struct, it becomes a data type, just like an int or float.**
    int id;
    string name;
    string category;
    int quantity;
};

**// Array to store products**
Product products[100];    **//this is an array of structs, products is an array with all user defined datatype as Product which is a struct.**
int productCount = 0;   **// Keeps track of how many products have been added to the inventory.**

**// Function to add a new product**
void addProduct(int id, string name, string category, int quantity) {  **//writing a function called addProduct which adds new product to inventory.**
    products[productCount].id = id;     **//accessing the current position in the array products.**
    products[productCount].name = name;  **//the dot operator (.) is used to access individual fields within a structure.** 
    products[productCount].category = category;
    products[productCount].quantity = quantity;
    productCount++;      **// Increments the productCount after adding a product to track the number of products.**
    cout << "Product added!\n";
}

// Function to update stock quantity
void updateStockQuantity(int id, int quantity) {
    for (int i = 0; i < productCount; i++) {   **//loop to iterate over the array of products.**
        if (products[i].id == id) {        **//This compares the id of the current product with the id passed as a parameter to the function.**
            products[i].quantity = quantity;  **// Assigns the new quantity passed as a parameter to this product's quantity.**
            cout << "Quantity updated!\n";
            return;
        }
    }
    cout << "Product not found!\n";
}

**// Function to search for products by category**
void searchProductsByCategory(string category) {
    bool found = false;  **//Boolean flag found keeps track of whether any matching product is found.**
    for (int i = 0; i < productCount; i++) {
        if (products[i].category == category) { **//if function parameter category matches the current category of iterator.**
            cout << "ID: " << products[i].id << ", Name: " << products[i].name << ", Quantity: " << products[i].quantity << endl;
            found = true;
        }
    }
    if (!found) {
        cout << "No products found in category: " << category << endl;
    }
}

int main() {
    int choice, id, quantity;
    string name, category;

    while (true) {
        cout << "\n1. Add New Product\n";
        cout << "2. Update Stock Quantity\n";
        cout << "3. Search Products by Category\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice == 1) {   **//adding a product**
            cout << "Enter Product ID: ";
            cin >> id;
            cout << "Enter Product Name: ";
            cin.ignore();  **//This line ensures that any newline or remaining characters in the input buffer are ignored before taking the next string input. When we input the id, it ends with a newline ('\n'). If we don't use cin.ignore(), this newline will be captured by the getline() function, and it would result in an empty string.**
            getline(cin, name); **// This reads the entire line of input from the user, including spaces, and stores it in the string name. The getline() function reads everything up to the next newline character (\n), which makes it useful for multi-word inputs like a product name.**

            cout << "Enter Product Category: ";
            getline(cin, category);
            cout << "Enter Stock Quantity: ";
            cin >> quantity;
            addProduct(id, name, category, quantity);
        } else if (choice == 2) {  **//updating stock quantity of product**
            cout << "Enter Product ID to update: ";
            cin >> id;
            cout << "Enter new Stock Quantity: ";
            cin >> quantity;
            updateStockQuantity(id, quantity);
        } else if (choice == 3) {  **//search product by category**
            cout << "Enter Category to search: ";
            cin.ignore();
            getline(cin, category);
            searchProductsByCategory(category);
        } else if (choice == 4) {   **//exit** 
            break;
        } else {
            cout << "Invalid choice. Try again.\n";
        }
    }

    return 0;
}
