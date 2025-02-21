`try-with-resources` 是 Java 7 引入的一个特性，它提供了一种简洁的语法来确保每个资源在使用完毕后都被关闭。资源是指那些必须显式关闭的对象，如文件流、数据库连接等。`try-with-resources` 语句确保了即使发生异常，每个资源也会被自动关闭，从而减少了代码中可能出现的资源泄漏问题。

### 语法

`try-with-resources` 的基本语法如下：

```java
try (ResourceType resource1 = new ResourceType(/* ... */);
     ResourceType resource2 = new ResourceType(/* ... */)) {
    // 使用 resource1 和 resource2 的代码
} catch(SomeException e) {
    // 处理异常
}
```

这里 `ResourceType` 必须实现了 `java.lang.AutoCloseable` 接口，该接口定义了一个 `close()` 方法，用于释放资源。`try-with-resources` 语句会在 try 块结束时自动调用 `close()` 方法。

### 示例

下面是一个使用 `try-with-resources` 打开并读取文件的例子：

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class TryWithResourcesExample {

    public static void main(String[] args) {
        // 使用 try-with-resources 语句打开文件和 BufferedReader
        try (FileReader fr = new FileReader("data.txt");
             BufferedReader br = new BufferedReader(fr)) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

在这个例子中，`FileReader` 和 `BufferedReader` 都实现了 `AutoCloseable` 接口，因此它们会在 `try` 块执行完毕后自动关闭，而不需要显式地调用 `close()` 方法。

### 多个资源

如果需要管理多个资源，可以在 `try` 括号内用分号分隔声明多个资源：

```java
try (ResourceType1 resource1 = new ResourceType1(/* ... */);
     ResourceType2 resource2 = new ResourceType2(/* ... */)) {
    // 使用 resource1 和 resource2 的代码
}
```

### 资源初始化表达式

你还可以在资源初始化表达式中使用更复杂的逻辑，比如创建资源时传递参数或调用方法：

```java
String query = "SELECT * FROM users";
try (Connection conn = DriverManager.getConnection(dbUrl, user, password);
     Statement stmt = conn.createStatement();
     ResultSet rs = stmt.executeQuery(query)) {
    // 使用 conn, stmt, rs 的代码
}
```

在这个例子中，数据库连接 (`Connection`)、SQL语句 (`Statement`) 和结果集 (`ResultSet`) 都会被自动关闭。

### 注意事项

- 如果资源的构造函数抛出异常，则后续的资源将不会被初始化。
- 在 `try-with-resources` 中声明的资源变量的作用域仅限于 `try` 块内部。
- 如果资源本身在创建过程中就抛出了异常，那么它的 `close()` 方法可能就不会被调用。对于这种情况，应该考虑使用其他方式来确保资源正确关闭。