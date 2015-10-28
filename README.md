# Bouts de code

## Camel

```java
public class TestCamel {
    public static void main(String[] args) throws Exception {
        CamelContext ctx = new DefaultCamelContext();
        ctx.addRoutes(new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                onException(Throwable.class).log(LoggingLevel.ERROR, "${exception}");
                from("direct:test").throwException(new Exception("Argh !"));
            }
        });

        ProducerTemplate producer = ctx.createProducerTemplate();
        ctx.start();
        producer.sendBody("direct:test", "Hello");
    }
}
```
