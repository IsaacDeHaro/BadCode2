# BadCode2
Aquí tienes un ejemplo de un código "badcode" en C# para el problema de una aplicación de tienda en línea que gestiona pedidos. Este código tiene múltiples problemas que pueden beneficiarse de refactorización y patrones de diseño.

### Código C# de "badcode"

```csharp
using System;
using System.Collections.Generic;

namespace OnlineStore
{
    public class Order
    {
        public int OrderId;
        public string CustomerName;
        public string Status;
        public List<string> Products;
        public double TotalPrice;

        public Order(int orderId, string customerName, List<string> products)
        {
            OrderId = orderId;
            CustomerName = customerName;
            Products = products;
            Status = "New";
            CalculateTotalPrice();
        }

        public void CalculateTotalPrice()
        {
            TotalPrice = 0;
            foreach (var product in Products)
            {
                if (product == "Laptop")
                    TotalPrice += 1000;
                else if (product == "Phone")
                    TotalPrice += 500;
                else if (product == "Tablet")
                    TotalPrice += 300;
            }
        }

        public void ApplyDiscount()
        {
            if (CustomerName == "John Doe")
                TotalPrice *= 0.9; // 10% discount for John Doe
        }

        public void PrintInvoice()
        {
            Console.WriteLine($"Order ID: {OrderId}");
            Console.WriteLine($"Customer: {CustomerName}");
            Console.WriteLine($"Status: {Status}");
            Console.WriteLine("Products:");
            foreach (var product in Products)
                Console.WriteLine($"- {product}");
            Console.WriteLine($"Total Price: {TotalPrice}");
        }

        public void ProcessOrder()
        {
            if (Status == "New")
            {
                Console.WriteLine("Processing order...");
                Status = "Processed";
                Console.WriteLine("Order processed.");
            }
            else if (Status == "Processed")
            {
                Console.WriteLine("Order already processed.");
            }
            else if (Status == "Cancelled")
            {
                Console.WriteLine("Cannot process a cancelled order.");
            }
        }

        public void CancelOrder()
        {
            if (Status == "New" || Status == "Processed")
            {
                Console.WriteLine("Cancelling order...");
                Status = "Cancelled";
                Console.WriteLine("Order cancelled.");
            }
            else
            {
                Console.WriteLine("Order is already cancelled.");
            }
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            var products = new List<string> { "Laptop", "Phone", "Tablet" };
            var order = new Order(1, "John Doe", products);
            order.PrintInvoice();
            order.ApplyDiscount();
            order.PrintInvoice();
            order.ProcessOrder();
            order.CancelOrder();
        }
    }
}
```

### Lista de 10 Cuestionamientos a Resolver en el Código

1. **¿Cómo mejorarías la flexibilidad del cálculo de precios?**
   - Actualmente, el cálculo de precios está directamente en el método `CalculateTotalPrice` con condicionales específicos para cada producto. ¿Qué patrón podría utilizarse para delegar este cálculo a otra clase?

2. **¿Cómo podríamos manejar los estados del pedido de manera más robusta?**
   - Los estados están representados como cadenas ("New", "Processed", "Cancelled"). ¿Sería más seguro y claro usar el patrón **State** para encapsular los cambios de estado?

3. **¿De qué manera podríamos eliminar el acoplamiento fuerte del método `ApplyDiscount`?**
   - `ApplyDiscount` está vinculado al nombre del cliente. ¿Cómo podríamos abstraer esta lógica para que el sistema pueda aplicar diferentes descuentos sin condicionales específicos?

4. **¿Cómo se podría mejorar la extensión de los productos sin modificar el código de `Order`?**
   - Actualmente, cada producto se identifica por nombre en `CalculateTotalPrice`. ¿Podríamos utilizar un patrón de creación como **Factory** o **Abstract Factory** para gestionar diferentes productos?

5. **¿Qué técnicas de refactorización podrías aplicar para reducir la complejidad de `PrintInvoice`?**
   - `PrintInvoice` imprime directamente en la consola. ¿Cómo podríamos desacoplar la lógica de impresión para facilitar cambios futuros en el formato de salida?

6. **¿De qué manera podrías desacoplar el código de `ProcessOrder` y `CancelOrder`?**
   - Estos métodos tienen lógica condicional en base al estado. ¿Sería útil aplicar el patrón **State** aquí también para encapsular estas acciones?

7. **¿Cómo mejorarías la reutilización y mantenibilidad del método `ApplyDiscount`?**
   - La implementación actual solo aplica descuentos a un cliente específico. ¿Podríamos mejorar esto usando un patrón como **Strategy** para aplicar diferentes tipos de descuento?

8. **¿Es eficiente y claro el método `CalculateTotalPrice`?**
   - La función depende de nombres de productos hardcoded. ¿Qué técnica de refactorización o patrón de diseño ayudaría a evitar esta dependencia de strings?

9. **¿Cómo podríamos modificar el método `PrintInvoice` para permitir exportar la factura en diferentes formatos?**
   - `PrintInvoice` solo imprime en consola. ¿Cómo podríamos aplicar el patrón **Adapter** o **Decorator** para permitir exportar en formatos como PDF o HTML?

10. **¿Cómo asegurarías que este código cumple con el Principio de Responsabilidad Única (SRP)?**
    - `Order` tiene múltiples responsabilidades (gestión de productos, cálculo de precios, impresión, y gestión de estados). ¿Qué técnicas de refactorización podrías utilizar para dividir estas responsabilidades en clases más específicas?

Estos cuestionamientos están diseñados para guiar el análisis y la refactorización del código, mejorando su claridad, flexibilidad y cumplimiento de principios de diseño y patrones.
