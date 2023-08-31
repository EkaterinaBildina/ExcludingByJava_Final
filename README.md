# ExcludingByJava_Final

Создайте иерархию классов для интернет-магазина, как в примере .
Реализуйте методы для обработки покупок и доступа к данным о продуктах.

В РЕЗУЛЬТАТЕ ПРИМЕНЕНИЯ ИСКЛЮЧЕНИЙ
для примера (используя наглядный пример): productId = 1, Product("Product 1", 10, 5.99);
- ProductIDIncorrectInput (реализован на уровне пользователя в бизнес-классе OnlineShopUI)
 : Enter product ID: введем число отличное от 1
 // throw new ProductIDIncorrectInput("Input error of product ID");
 : получим "Input error of product ID"

- QuantityException (реализован внутри Класса ShopManager в методе purchaseProduct)
  : Enter product ID: 1
  : Enter quantity: введем число больше 10
// throw new QuantityException("Quantity isn't enough");
  : получим "Quantity isn't enough"

  В случае успешного выполнения запроса, пользователь получит:
  Good choice! Pay money and enjoy!
  Product 1 with Total price: $11.98
  // Product.getName() + " with Total price: $" + totalPrice

---------------------------------------
Исходный файл:
import java.util.Scanner;

public class OnlineShopUI {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter product ID: ");
        int productId = scanner.nextInt();
        System.out.print("Enter quantity: ");
        int quantity = scanner.nextInt();

        double totalPrice = ShopManager.purchaseProduct(productId, quantity);
        System.out.println("Total price: $" + totalPrice);
    }
}
public class ShopManager {
    public static double purchaseProduct(int productId, int quantity) {
        Product product = ProductDatabase.getProduct(productId);
        double totalPrice = product.getPrice() * quantity;
        return totalPrice;
    }
}
public class ProductDatabase {
    public static Product getProduct(int productId) {
        // Подразумевается обращение к базе данных или хранилищу товаров
        // и получение информации о товаре по его ID
        // В данном примере мы используем заглушку
        if (productId == 1) {
            return new Product("Product 1", 10, 5.99);
        }
        return null;
    }
}
public class Product {
    private String name;
    private int availableQuantity;
    private double price;

    public Product(String name, int availableQuantity, double price) {
        this.name = name;
        this.availableQuantity = availableQuantity;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public int getAvailableQuantity() {
        return availableQuantity;
    }

    public double getPrice() {
        return price;
    }
}
------------------------------------------------------
