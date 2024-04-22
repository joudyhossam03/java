package javaapplication107;

import java.util.Scanner;

/**
 *
 * @author joudi
 */
public class JavaApplication107 {

    /**
     * @param args 
     */
   
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the B-Commerce System!");

        System.out.println("Please enter your id");
        int customerId = scanner.nextInt();
        scanner.nextLine(); // Consume newline
        System.out.println("Please enter your name");
        String name = scanner.nextLine();
        System.out.println("Please enter your address");
        String address = scanner.nextLine();
        Customer customer = new Customer(customerId, name, address);

        ElectronicProduct smartphone = new ElectronicProduct(1, "smartphone", 599.9f, "Samsung", 1);
        ClothingProduct tShirt = new ClothingProduct(2, "T-shirt", 19.99f, "Medium", "Cotton");
        BookProduct oopBook = new BookProduct(3, "OOP", 39.99f, "O’Reilly", "X Publications");

        System.out.println("How many products you want to add to your cart?");
        int nProducts = scanner.nextInt();
        Cart cart = new Cart(customer.getCustomerId(), nProducts);

        for (int i = 0; i < nProducts; i++) {
            System.out.println("Which product would you like to add? 1- Smartphone 2- I-Shirt 3- OOP");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    cart.addProduct(smartphone, i);
                    break;
                case 2:
                    cart.addProduct(tShirt, i);
                    break;
                case 3:
                    cart.addProduct(oopBook, i);
                    break;
                default:
                    System.out.println("Invalid choice!");
                    break;
            }
        }

        float totalPrice = cart.calculatePrice();
        System.out.println("Your total is $" + totalPrice + ". Would you like to place the order? 1- Yes 2- No");
        int placeOrderChoice = scanner.nextInt();
        if (placeOrderChoice == 1) {
            cart.placeOrder();
        } else {
            System.out.println("Order placement canceled.");
        }

        scanner.close();
    }
}
  
    package javaapplication107;

/**
 *
 * @author joudi
 */

    class Product {
    private int productId;
    private String name;
    private float price;

    public Product(int productId, String name, float price) {
        this.productId = Math.abs(productId);
        this.name = name;
        this.price = Math.abs(price);
    }

    public int getProductId() {
        return productId;
    }

    public void setProductId(int productId) {
        this.productId = Math.abs(productId);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public float getPrice() {
        return price;
    }

    public void setPrice(float price) {
        this.price = Math.abs(price);
    }
}

package javaapplication107;

/**
 *
 * @author joudi
 */

 class ElectronicProduct extends Product {
    private String brand;
    private int warrantyPeriod;

    public ElectronicProduct(int productId, String name, float price, String brand, int warrantyPeriod) {
        super(productId, name, price);
        this.brand = brand;
        this.warrantyPeriod = Math.abs(warrantyPeriod);
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getWarrantyPeriod() {
        return warrantyPeriod;
    }

    public void setWarrantyPeriod(int warrantyPeriod) {
        this.warrantyPeriod = Math.abs(warrantyPeriod);
    }
}   

package javaapplication107;

/**
 *
 * @author joudi
 */

    class ClothingProduct extends Product {
    private String size;
    private String fabric;

    public ClothingProduct(int productId, String name, float price, String size, String fabric) {
        super(productId, name, price);
        this.size = size;
        this.fabric = fabric;
    }

    public String getSize() {
        return size;
    }

    public void setSize(String size) {
        this.size = size;
    }

    public String getFabric() {
        return fabric;
    }

    public void setFabric(String fabric) {
        this.fabric = fabric;
    }
}


package javaapplication107;

/**
 *
 * @author joudi
 */

    class BookProduct extends Product {
    private String author;
    private String publisher;

    public BookProduct(int productId, String name, float price, String author, String publisher) {
        super(productId, name, price);
        this.author = author;
        this.publisher = publisher;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getPublisher() {
        return publisher;
    }

    public void setPublisher(String publisher) {
        this.publisher = publisher;
    }
}


package javaapplication107;

/**
 *
 * @author joudi
 */

   class Customer {
    private int customerId;
    private String name;
    private String address;

    public Customer(int customerId, String name, String address) {
        this.customerId = Math.abs(customerId);
        this.name = name;
        this.address = address;
    }

    public int getCustomerId() {
        return customerId;
    }

    public void setCustomerId(int customerId) {
        this.customerId = Math.abs(customerId);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
 

package javaapplication107;

/**
 *
 * @author joudi
 */

    class Cart {
    private int customerId;
    private int nProducts;
    private Product[] products;

    public Cart(int customerId, int nProducts) {
        this.customerId = Math.abs(customerId);
        this.nProducts = Math.abs(nProducts);
        this.products = new Product[nProducts];
    }

    public int getCustomerId() {
        return customerId;
    }

    public void setCustomerId(int customerId) {
        this.customerId = Math.abs(customerId);
    }

    public int getNProducts() {
        return nProducts;
    }

    public void setNProducts(int nProducts) {
        this.nProducts = Math.abs(nProducts);
    }

    public Product[] getProducts() {
        return products;
    }

    public void setProducts(Product[] products) {
        this.products = products;
    }

    public void addProduct(Product product, int index) {
        products[index] = product;
    }

    public void removeProduct(int index) {
        products[index] = null;
    }

    public float calculatePrice() {
        float totalPrice = 0;
        for (Product product : products) {
            if (product != null) {
                totalPrice += product.getPrice();
            }
        }
        return totalPrice;
    }

    public void placeOrder() {
        System.out.println("Here's your order's summary:");
        System.out.println("Order ID: 1"); // Hardcoded for simplicity
        System.out.println("Customer ID: " + customerId);
        System.out.println("Products:");

        for (Product product : products) {
            if (product != null) {
                System.out.println(product.getName() + " - $" + product.getPrice());
            }
        }

        System.out.println("Total Price: $" + calculatePrice());
    }
}







