# EventManager

A simple java event manager.

## Creating an event

```java
    // Normal event
    public class TestEvent extends Event  {
    }
```

```java
    // Cancellable event
    public class TestEvent extends Event implements Cancellable {

    private boolean cancelled;

    @Override
    public boolean isCancelled() {
        return cancelled;
    }

    @Override
    public void setCancelled(boolean cancelled) {
        this.cancelled = cancelled;
    }
    
```

```java
    // Type event, can be PRE or POST
    public class TestEvent extends Event implements Type {

        private EventType type;

        public TestEvent(EventType type) {
            this.type = type;
        }

        @Override
        public EventType getType() {
            return type;
        }
    }
```

## Listening for an event
```java
public class Main {

    public static void main(String[] args) {

        Test test = new Test();

        // registering
        EventManager.INSTANCE.register(test);

        // un-registering
        EventManager.INSTANCE.unregister(test);
    }

    // Every class you register must implement Listener
    private static class Test implements Listener {

        @EventTarget
        public void onEvent(TestEvent event) {
            System.out.println("test");
        }

    }
}
```

## Calling an event
```java
public class Main {

    public static void main(String[] args) {
       new TestEvent().call();
    }

}
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
