**Builder Pattern**

Suppose you have a class Cake. You might get away with creating a cake with multiple constructors if you want to create a cake in different ways. However, a better approach would be using the Builder Pattern that allows you to customize your Cake as you like and add default parameters if you want. Below is an example of such a cake with three parameters. Notice the private constructor for the actual cake, which means only the CakeBuilder can create instances of Cake.

```java
public class Cake {

  private final int sugar;
  private final int flour;
  private final int water;

  private Cake(int sugar, int flour, int water) {
    this.sugar = sugar;
    this.flour = flour;
    this.water = water;
  }

  static class CakeBuilder {
    private int sugar = 10;
    private int flour = 20;
    private int water = 30;

    public CakeBuilder setSugar(int sugar) {
      this.sugar = sugar;
      return this;
    }

    public CakeBuilder setFlour(int flour) {
      this.flour = flour;
      return this;
    }

    public CakeBuilder setWater(int water) {
      this.water = water;
      return this;
    }

    public Cake build() {
      return new Cake(this.sugar, this.flour, this.water);
    }
  }

}	
```

**Factory Pattern**

Suppose you have many different types of Cake. Instead of remembering how to create every type of Cake, you can have a CakeFactory class that will simplify the process. (IllegalArgumentException is the way of handling unknown String argument)

```java
public class CakeFactory {

  public static Cake makeCake(String type) throws IllegalArgumentException {
    switch (type) {
      case "cheesecake low cheese":
        return new CheeseCake(100, 100);
      case "cheesecake high cheese":
        return new CheeseCake(100, 250);
      case "chocolate cake no frosting":
        return new ChocolateCake(200, 200, false);
      case "chocolate cake with frosting":
        return new ChocolateCake(200, 200, true);
      default:
        throw new IllegalArgumentException("Unknown cake type");
    }
  }
}

class Cake {
  private final int sugar;

  public Cake(int sugar) {
    this.sugar = sugar;
  }
}

class CheeseCake extends Cake {

  private final int cheese;

  public CheeseCake(int sugar, int cheese) {
    super(sugar);
    this.cheese = cheese;
  }
}

class ChocolateCake extends Cake {

  private final int chocolate;
  private final boolean hasFrosting;

  public ChocolateCake(int sugar, int chocolate, boolean hasFrosting) {
    super(sugar);
    this.chocolate = chocolate;
    this.hasFrosting = hasFrosting;
  }
}
```
