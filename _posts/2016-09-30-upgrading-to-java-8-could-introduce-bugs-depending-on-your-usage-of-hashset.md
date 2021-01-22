---
title: Upgrading to Java 8 could introduce bugs depending on your usage of HashSet
layout: posts
---

If you're looking to upgrade from Java 7 to Java 8 you may not be aware that there are some rather significant differences to how ordering is maintained for HashSet and HashMap in Java 8.  This may not matter to you if you're confident that your code base is free of code that assumes HashSet and HashMap is relied on to maintain order.  Even though the Java documentation clearly states that both [HashSet](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) and [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) make no guarantees as to the order of the elements AND that the order will remain constant over time, it's not inconceivable that some developers may not be aware of this.  As I was writing this blog post and playing around with HashSet in Java 7, I could see how naive developers could be fooled (very much dependent on the elements that are contained in the HashSet) into believing that HashSet maintains order that's consistent with something like an ArrayList.

Anyhow, I'd like to keep this simple and demonstrate how ordering is different in Java 7 Vs 8.  I have the following Java class:

    import java.util.HashMap;
    import java.util.HashSet;
    import java.util.Map;
    import java.util.Set;

    public class Main {
       public static void main(String[] args) {
          Set<String> names = new HashSet<>();
          names.add("Amy");
          names.add("Bob");
          names.add("Chris");

          for (String name : names) {
             System.out.print(name + " > ");
          }
          System.out.println("");

          Set<Integer> numbers = new HashSet<>();
          numbers.add(1);
          numbers.add(2);
          numbers.add(3);

          for (Integer number : numbers) {
             System.out.print(number + " > ");
          }
          System.out.println("");

          Map<String, String> cars = new HashMap();
          cars.put("Ford", "Taurus");
          cars.put("Honda", "Fit");
          cars.put("Toyota", "Camry");

          for (String car : cars.keySet()) {
             System.out.print(car + " > ");
          }
       }
    }

When I compiled and executed the above code in Java 7, I got the following result:

    Amy > Bob > Chris >
    1 > 2 > 3 >
    Ford > Toyota > Honda >

However, when I compiled and executed it in Java 8, I got the following result:

    Bob > Chris > Amy >
    1 > 2 > 3 >
    Toyota > Ford > Honda >

FWIW - even though the Java documentation states that *"...it does not guarantee that the order will remain constant over time..."* - I don't believe this means that given a HashSet with a particular set of elements, the order will vary frequently.  My experience with HashSet has been that if I were to execute the above code 1,000 times, the order will be consistent across all 1,000 executions.
