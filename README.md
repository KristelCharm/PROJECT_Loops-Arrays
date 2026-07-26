# 💄 Makeup Product Selection

A Java command-line application that allows users to browse a catalog of makeup products, select specific items, and calculate their total purchase cost.

---

## 📌 Features

* **Product Catalog:** Displays an indexed list of available makeup items with their prices.
* **Flexible Quantity Selection:** Allows customers to select 1, 3, or 6 products.
* **Input Validation:** Ensures selected item numbers and quantities are within valid ranges.
* **Purchase Summary:** Formats and prints an itemized bill along with the total cost and customer name.

---

## 💄 Catalog Items

| Item # | Product Name | Price |
| :---: | :--- | :---: |
| 1 | Lipstick | $15.00 |
| 2 | Eyeshadow | $20.00 |
| 3 | Powder Blush | $18.00 |
| 4 | Foundation | $25.00 |
| 5 | Setting Powder | $22.00 |
| 6 | Setting Spray | $19.00 |

---

## 💡 Code Overview

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class MakeupProductSelection {

    static class Product {
        String name;
        double price;

        Product(String name, double price) {
            this.name = name;
            this.price = price;
        }
    }

    public static void main(String[] args) {

        List<Product> products = new ArrayList<>();

        products.add(new Product("Lipstick", 15.00));
        products.add(new Product("Eyeshadow", 20.00));
        products.add(new Product("Powder Blush", 18.00));
        products.add(new Product("Foundation", 25.00));
        products.add(new Product("Setting Powder", 22.00));
        products.add(new Product("Setting Spray", 19.00));

        System.out.println("Available Makeup Products:");
        for (int i = 0; i < products.size(); i++) {
            System.out.println((i + 1) + ". " + products.get(i).name + " - $" + products.get(i).price);
        }

        Scanner scanner = new Scanner(System.in);

        System.out.print("\nEnter your name: ");
        String buyerName = scanner.nextLine();

        System.out.print("How many products would you like to buy? (1, 3, or 6): ");
        int numberOfProducts = scanner.nextInt();

        if (numberOfProducts != 1 && numberOfProducts != 3 && numberOfProducts != 6) {
            System.out.println("Invalid number of products.");
            scanner.close();
            return;
        }

        List<Product> selectedProducts = new ArrayList<>();
        double totalCost = 0;

        for (int i = 0; i < numberOfProducts; i++) {

            System.out.print("Select product " + (i + 1) + " (1-6): ");
            int productNumber = scanner.nextInt();

            if (productNumber < 1 || productNumber > products.size()) {
                System.out.println("Invalid product number.");
                scanner.close();
                return;
            }

            Product selectedProduct = products.get(productNumber - 1);
            selectedProducts.add(selectedProduct);
            totalCost += selectedProduct.price;
        }

        System.out.println("\n========== PURCHASE SUMMARY ==========");
        System.out.println("Customer: " + buyerName);

        for (Product product : selectedProducts) {
            System.out.println(product.name + " - $" + product.price);
        }

        System.out.printf("Total Cost: $%.2f%n", totalCost);

        scanner.close();
    }
}