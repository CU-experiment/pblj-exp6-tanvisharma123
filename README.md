# Write a program to sort a list of Employee objects (name, age, salary) using lambda expressions.
    import java.util.*;
    import java.util.stream.Collectors;

    class Employee {
    private String name;
    private int age;
    private double salary;

    public Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    public double getSalary() { return salary; }

    @Override
    public String toString() {
        return "Employee{name='" + name + "', age=" + age + ", salary=" + salary + "}";
    }
}

    public class EmployeeSort {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Employee("Alice", 30, 50000),
            new Employee("Bob", 25, 60000),
            new Employee("Charlie", 35, 40000),
            new Employee("David", 28, 55000)
        );

        // Sorting by name using lambda expression
        List<Employee> sortedByName = employees.stream()
                .sorted(Comparator.comparing(Employee::getName))
                .collect(Collectors.toList());

        System.out.println("Sorted by Name:");
        sortedByName.forEach(System.out::println);

        // Sorting by age using lambda expression
        List<Employee> sortedByAge = employees.stream()
                .sorted(Comparator.comparingInt(Employee::getAge))
                .collect(Collectors.toList());

        System.out.println("\nSorted by Age:");
        sortedByAge.forEach(System.out::println);

        // Sorting by salary using lambda expression
        List<Employee> sortedBySalary = employees.stream()
                .sorted(Comparator.comparingDouble(Employee::getSalary))
                .collect(Collectors.toList());

        System.out.println("\nSorted by Salary:");
        sortedBySalary.forEach(System.out::println);
    }
}
# Create a program to use lambda expressions and stream operations to filter students scoring above 75%, sort them by marks, and display their names.
    import java.util.*;
    import java.util.stream.Collectors;

    class Student {
    private String name;
    private double marks;

    public Student(String name, double marks) {
        this.name = name;
        this.marks = marks;
    }

    public String getName() { return name; }
    public double getMarks() { return marks; }

    @Override
    public String toString() {
        return "Student{name='" + name + "', marks=" + marks + "}";
    }
    }

    public class StudentFilterSort {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
            new Student("Alice", 85),
            new Student("Bob", 72),
            new Student("Charlie", 90),
            new Student("David", 65),
            new Student("Eve", 78)
        );

        // Filtering students with marks above 75%, sorting by marks in descending order
        List<String> filteredAndSortedStudents = students.stream()
                .filter(student -> student.getMarks() > 75) // Filter marks > 75
                .sorted(Comparator.comparingDouble(Student::getMarks).reversed()) // Sort in descending order
                .map(Student::getName) // Extract names
                .collect(Collectors.toList()); // Collect into a list

        // Display the names of students
        System.out.println("Students scoring above 75% (sorted by marks):");
        filteredAndSortedStudents.forEach(System.out::println);
    }
    }

# Write a Java program to process a large dataset of products using streams. Perform operations such as grouping products by category, finding the most expensive product in each category, and calculating the average price of all products
    import java.util.*;
    import java.util.stream.Collectors;

    class Product {
    private String name;
    private String category;
    private double price;

    public Product(String name, String category, double price) {
        this.name = name;
        this.category = category;
        this.price = price;
    }

    public String getName() { return name; }
    public String getCategory() { return category; }
    public double getPrice() { return price; }

    @Override
    public String toString() {
        return "Product{name='" + name + "', category='" + category + "', price=" + price + "}";
    }
    }

    public class ProductStreamOperations {
    public static void main(String[] args) {
        List<Product> products = Arrays.asList(
            new Product("Laptop", "Electronics", 80000),
            new Product("Smartphone", "Electronics", 60000),
            new Product("Headphones", "Electronics", 3000),
            new Product("Refrigerator", "Appliances", 50000),
            new Product("Washing Machine", "Appliances", 40000),
            new Product("Mixer Grinder", "Appliances", 5000),
            new Product("T-shirt", "Clothing", 1500),
            new Product("Jeans", "Clothing", 2500),
            new Product("Jacket", "Clothing", 5000)
        );

        // Grouping products by category
        Map<String, List<Product>> productsByCategory = products.stream()
                .collect(Collectors.groupingBy(Product::getCategory));

        System.out.println("Products grouped by category:");
        productsByCategory.forEach((category, productList) -> {
            System.out.println(category + ": " + productList);
        });

        // Finding the most expensive product in each category
        Map<String, Optional<Product>> mostExpensiveByCategory = products.stream()
                .collect(Collectors.groupingBy(
                        Product::getCategory, 
                        Collectors.maxBy(Comparator.comparingDouble(Product::getPrice))
                ));

        System.out.println("\nMost expensive product in each category:");
        mostExpensiveByCategory.forEach((category, product) ->
                System.out.println(category + ": " + product.get().getName() + " (₹" + product.get().getPrice() + ")"));

        // Calculating the average price of all products
        double averagePrice = products.stream()
                .mapToDouble(Product::getPrice)
                .average()
                .orElse(0.0);

        System.out.println("\nAverage price of all products: ₹" + averagePrice);
    }
    }
