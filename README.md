```java
public class SpendReport {
    public static Table report (Table transactions) {
        Table table = transactions.window(Slide.over(lit(5).minutes())
                .every(lit(1).minutes())
                .on($("transaction time"))
                .as("log_ts"))
                .groupBy($("account id"),$( "log_ts"))
                .select($("account id"),
                        $("log_ts").start().as ("log_ts"),
                        $("amount").avg().as("amount"));
        return table;
    }
}
```
