Welcome to this lesson in our Design Patterns series. In this video we’ll be
going over the DAO or Data Access Object pattern. DAO is a commonly used
pattern that you’ll see in many projects and will be helpful in any future
programming assignments where you need to access a database. Before beginning
this lesson you should have familiarity with how to create classes and
interfaces as well as how to perform basic database operations within your
code. 

The examples in this lesson will be written in Java, but the style will be the
same for other languages. First and foremost, the reason why we use the DAO
pattern is to decouple your business logic code from the code that accesses the
database. This pattern is useful in making your code flexible enough to make
room for changes later down the lines. Say, for example, you get the
requirement to switch from a MySQL database to an Oracle database, then the
only classes that you need to touch are a simple configuration class and the
class that defines the methods that hit the database. 

To implement a DAO pattern, you will need three types of java files:

- One.  An interface that declares the data access methods that your business
  classes will use. This interface will typically have CRUD style methods. For
  example, you’ll have methods to create data, retrieve data, update it and
  delete it as well. 
- You will also need a concrete class that implements this interface for the
  specific data source that you are sending commands to.
- Lastly, you will need a model class that represents the data. For example, if
  you want to retrieve a list of products, then you’ll most likely have a
  Product class that defines the properties of a product. 
- Additionally, you may want to create a utility class that manages some of the
  repetitive operations that you perform for any database access such as
  establishing a connection. 
 
So, let’s get into a quick example. Imagine we have a database already setup
and it has the following table representing products that a user will manage.
The products table is defined as follows: It has an id that is an integer, a
product name and a product description. 

The first thing we can do is setup our model class. Now, again, the syntax will
vary, depending on the programming language that you are implementing this
pattern with, but the principles remain consistent. For our example here, we’ll
use the Java language.  So, our model class will look as follows:

```java
// Product.java
package model;

public class Product {
  long productID;
  String productName;
  String productDescription;
}
```

Next we’ll define the DAO interface that we’ll use to declare the type of
operations that we’ll need for our application. Let’s say we’ll need an
operation to add a product, update a product, get a list of products, and
delete a product. We’ll define our interface as follows.  

ProductDAO and methods getProducts, addProduct, updateProduct and
deleteProduct. 

```java
// ProductDAO.java
package dao;
import java.util.List;
import modelProduct;

public interface ProductDAO {

  List<Product> getProducts();
  
  void addProduct(Product product);
  void deleteProduct(Product product);
  void updateProduct(Porduct product);
}
```

Okay next we’ll create our implementation class for our ProductDAO interface.
We’ll define our class ProductDAOImpl and declare our first method getProducts
which will return a list of products. In Java, the most basic of database
operations involves using the JDBC API and the first task is to get a
connection. 

Now since we’ll always need to get a Connection for any operation, we’ll go
ahead and define that in a different method. This method will return a
connection everytime it is called.  Here is one way that you can do this in
Java. Now, we’ll return to our getProducts method and call getConnection().
Then we’d setup our SQL to execute and perform the JDBC-specific steps and
finally return the list of products. 

```java
// ProductDAOImpl.java
package dao;
import java.util.List;

public class ProductDAOImpl implements ProductDAO {

  private Connection getConnection() {
    Class.forName("oracle.jdbc.OracleDriver");
    return DeriverManager.getConnection("url", "revature", "password");
  }
  
  @Override
  public List<Product> getProducts() {
    List<Product> products = new ArrayList<Product>();
    
    try {
      Connection conn = getConnection();
      String sql = "SELECT * FRROM PRODUCTS";
      PreparedStatement ps = conn.prepareStatement(sql);
      ResultSet rs = ps.executeQuery();
      
      while(rs.next()) {
        long id = rs.getLong(1);
        String name = rs.getString(2);
        String desc = rs.getString(3);
        
        Procuct p = new Product();
        p.setProductId(id);
        p.setProductName(name);
        p.setProductDescription(desc);
        products.add(p);
      }
    } catch (ClassNotFoundException | SQLException e) {
      e.printStackTrace();
    }
    
    return products;
  }
  
  /*
  I’ll show you one more operation so that you get a better grasp of the concept.
  We’ll add a product for our next example. First, we’ll get a connection, define
  the SQL to execute. Since this is a parameterized statement we’ll set the
  individual properties of the SQL statement using the getter methods from our
  product class. We’ll lastly execute the statement and our database well exhibit
  the updated data. 
  */
  
  @Override
  public void addProduct (Product product) {
    try {
      Connection conn = getConnection();
      String sql = "INSERT INTO products VALUES(?,?,?)";
      PreparedStatement ps = conn.prepareStatement(sql);
      ps.setLong(1, product.getProductId());
      ps.setString(2, product.getProductName());
      ps.setString(3, product.getProductDescription());
      ps.executeUpdate();
      System.out.println("Product added successfully!");
    } catch (ClassNotFoundException | SQLException e) {
      e.printStackTrace();
    }
    
  }
  @Override
  public void deleteProduct (Product product) {
    // TODO Auto-generated method stub
  }
  @Override
  public void updateProduct (Product product) {
    // TODO Auto-generated method stub
  }
}
```

The last thing you can do is a little bit of refactoring and place the
getConnection() method in a utility class that is used to manage connections to
a database thereby keeping the ProductDAOImpl free of any other methods that
don’t focus on CRUD style operations. 

```java
// ConnectionUtility.java
package dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConnectionUtility {
  public static Connection getConnection() throws SQLException, ClassNotFoundException {
    Class.forName("oraclejdbc.OracleDriver");
    return DriverManager.getconnection("url", "revature", "password");
  }
}
```

This concludes our lesson on the DAO Pattern. Feel free to explore other
patterns and even combine some with the DAO. For example, the Factory Pattern
is a commonly used one with DAO to further decouple your data access classes of
your application from the business logic. 
