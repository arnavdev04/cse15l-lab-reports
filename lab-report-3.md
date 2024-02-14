# Lab Report 3 - Bugs and Commands (Week 5)

## Part 1 - Bugs
For this part of the lab report I will be focussing on the following code excerpt from `ArrayExamples.java` file:
```java
public class ArrayExamples {
...
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
...
}
```

* A failure-inducing input for the buggy program, as a JUnit test and any associated code
    ```java
       import static org.junit.Assert.*;
       import org.junit.*;

       public class ArrayTests {

       @Test
       public void testReversed() {
         int[] input1 = {1,2,3};
         assertArrayEquals(new int[]{3,2,1}, ArrayExamples.reversed(input1));
         assertArrayEquals(new int[]{1,2,3}, input1);
         }
      }
    ```
* An input that doesn't induce a failure, as a JUnit test and any associated code
    ```java
       import static org.junit.Assert.*;
       import org.junit.*;

       public class ArrayTests {

       @Test
       public void testReversed() {
         int[] input1 = { };
         assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
         assertArrayEquals(new int[]{ }, input1);
         }
      }
    ```
* The symptom, as the output of running the tests:
    * For the 1st test-block:
       ![Image](report-3-images/image2.png)
    * For the 2nd test-block:
       ![Image](report-3-images/image1.png)
* The bug, as the before-and-after code change required to fix it
    * Before
    ```java
       public class ArrayExamples {
       ...
         // Returns a *new* array with all the elements of the input array in reversed
         // order
         static int[] reversed(int[] arr) {
           int[] newArray = new int[arr.length];
           for(int i = 0; i < arr.length; i += 1) {
           arr[i] = newArray[arr.length - i - 1]; //This line is the bug, arr and newArray should be swaped
           }
         return arr; //This line is all the bug, newArray should be returned
         }
       ...
      }
    ```
    * After
    ```java
       public class ArrayExamples {
       ...
         // Returns a *new* array with all the elements of the input array in reversed
         // order
         static int[] reversed(int[] arr) {
           int[] newArray = new int[arr.length];
           for(int i = 0; i < arr.length; i += 1) {
           newArray[i] = arr[arr.length - i - 1];
           }
         return newArray;
         }
       ...
      }
    ```
* Briefly describe why the fix addresses the issue.

  Firstly, we read from the description that we have to create a new array and return the new array we also have to make sure that the original array is left unchanged. From the first bug, the issue I realized was that the original array was being changed. The newly created `newArray` has null characters in it and since the original array `arr` was on the left side of the `=` sign, arr's data was also changed to null. The second problem was that `arr` was being returned instead of the new array `newArray`. 

   The issues addresses all these problems. Inside the `for loop`, `newArray` is constinuosly being updated with the reverse-ordeered data from `arr`. This fix also addresses the issue that the original array doesn't change and the reverses array is returned.
  
<br/><br/>
## Part 2 - Researching Commands
For this part of the lab report I will be writing about the `grep` command[^note].

1. `-r` option:
   


   `-r` option recursively searches for the given word or pattern (phrase) in a directory and or a group of files and systematically lists them out. The `-r` option is very useful as it enables the user to search through a directory instead of searching through each file individually.

2. `-r` option:
   

3. `-r` option:


4. `-r` option:
   




<br/><br/>
<br/><br/>

[^note]: ACADEMIC INTEGRITY NOTE: I have not used ChatGPT for this section and only referred to information provided by `man grep`. For general syntax of the options, I referred to web searches with a general search along the following line- "How does '-...' option of grep command work? ".




