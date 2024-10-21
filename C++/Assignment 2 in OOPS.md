#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Product {
private:
    int id;
    string name;
    string category;
    int quantity;

public:
    // Constructor to initialize product
    Product(int prodId, string prodName, string prodCategory, int prodQuantity)
        : id(prodId), name(prodName), category(prodCategory), quantity(prodQuantity) {}

    // Getter and Setter for ID
    int getId() const { return id; }
    void setId(int prodId) { id = prodId; }

    // Getter and Setter for Name
    string getName() const { return name; }
    void setName(string prodName) { name = prodName; }

    // Getter and Setter for Category
    string getCategory() const { return category; }
    void setCategory(string prodCategory) { category = prodCategory; }

    // Getter and Setter for Quantity
    int getQuantity() const { return quantity; }
    void setQuantity(int prodQuantity) { quantity = prodQuantity; }

    // Display product details
    void displayProduct() const {
        cout << "ID: " << id << ", Name: " << name << ", Category: " << category << ", Quantity: " << quantity << endl;
    }
};

// Vector to store products
vector<Product> inventory;

// Function to add a product
void addProduct(int id, string name, string category, int quantity) {
    inventory.push_back(Product(id, name, category, quantity));
    cout << "Product added!" << endl;
}

// Function to update stock quantity
void updateStockQuantity(int id, int quantity) {
    for (auto &product : inventory) {
        if (product.getId() == id) {
            product.setQuantity(quantity);
            cout << "Quantity updated!" << endl;
            return;
        }
    }
    cout << "Product not found!" << endl;
}

// Function to search products by category
void searchProductsByCategory(const string &category) {
    bool found = false;
    for (const auto &product : inventory) {
        if (product.getCategory() == category) {
            product.displayProduct();
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

        if (choice == 1) {
            cout << "Enter Product ID: ";
            cin >> id;
            cout << "Enter Product Name: ";
            cin.ignore();
            getline(cin, name);
            cout << "Enter Product Category: ";
            getline(cin, category);
            cout << "Enter Stock Quantity: ";
            cin >> quantity;
            addProduct(id, name, category, quantity);
        } else if (choice == 2) {
            cout << "Enter Product ID to update: ";
            cin >> id;
            cout << "Enter new Stock Quantity: ";
            cin >> quantity;
            updateStockQuantity(id, quantity);
        } else if (choice == 3) {
            cout << "Enter Category to search: ";
            cin.ignore();
            getline(cin, category);
            searchProductsByCategory(category);
        } else if (choice == 4) {
            break;
        } else {
            cout << "Invalid choice. Try again." << endl;
        }
    }

    return 0;
}
