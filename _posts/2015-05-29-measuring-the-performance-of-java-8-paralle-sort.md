---
layout: posts
---

I was curious as to the performance improvement of Arrays.parallelSort over Arrays.sort.

    package com.jpark;

    import java.text.NumberFormat;
    import java.util.Arrays;
    import java.util.Random;

    public class Main {

      private final static NumberFormat NUMBER_FORMAT = NumberFormat.getInstance();

      public static void main(String[] args) {
        sortIntegers(5);
        sortIntegers(50);
        sortIntegers(500);
        sortIntegers(5000);
        sortIntegers(50000);
        sortIntegers(500000);
        sortIntegers(5000000);
        sortIntegers(50000000);
      }

      private static void sortIntegers(int numberOfIntegers) {
        int[] numbers1 = getArrayOfRandomIntegers(numberOfIntegers);

        long currentTimeInNanos1 = System.nanoTime();
        Arrays.sort(numbers1);
        System.out.println(
            "It took " +
            NUMBER_FORMAT.format(System.nanoTime() - currentTimeInNanos1) +
            " nanoseconds to sort " +
            NUMBER_FORMAT.format(numberOfIntegers) +
            " integers.");

        int[] numbers2 = getArrayOfRandomIntegers(numberOfIntegers);
        long currentTimeInNanos2 = System.nanoTime();
        Arrays.parallelSort(numbers2);
        System.out.println(
            "It took " +
            NUMBER_FORMAT.format(System.nanoTime() - currentTimeInNanos2) +
            " nanoseconds to parallel sort " +
            NUMBER_FORMAT.format(numberOfIntegers) +
            " integers.\n");
      }

      private static int[] getArrayOfRandomIntegers(int sizeOfArray) {
        int[] numbers = new int[sizeOfArray];

        Random random = new Random();
        for (int i = 0; i < sizeOfArray; i++) {
          numbers[i] = random.nextInt(sizeOfArray);
        }

        return numbers;
      }
    }

And here are the results:

    It took 249,227 nanoseconds to sort 5 integers.
    It took 8,453 nanoseconds to parallel sort 5 integers.

    It took 22,733 nanoseconds to sort 50 integers.
    It took 16,206 nanoseconds to parallel sort 50 integers.

    It took 311,243 nanoseconds to sort 500 integers.
    It took 295,214 nanoseconds to parallel sort 500 integers.

    It took 4,493,890 nanoseconds to sort 5,000 integers.
    It took 676,900 nanoseconds to parallel sort 5,000 integers.

    It took 8,691,251 nanoseconds to sort 50,000 integers.
    It took 20,807,485 nanoseconds to parallel sort 50,000 integers.

    It took 169,959,867 nanoseconds to sort 500,000 integers.
    It took 31,648,894 nanoseconds to parallel sort 500,000 integers.

    It took 619,525,317 nanoseconds to sort 5,000,000 integers.
    It took 278,889,064 nanoseconds to parallel sort 5,000,000 integers.

    It took 7,050,170,435 nanoseconds to sort 50,000,000 integers.
    It took 3,121,830,435 nanoseconds to parallel sort 50,000,000 integers.

So it appears that Arrays.parallelSort is faster indeed.
