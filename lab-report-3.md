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

```
arnav@Arnavs-MacBook-Pro docsearch % grep -r "Darwin" ./technical
./technical/plos/journal.pbio.0020347.txt:        described by Charles Darwin (1859).
./technical/plos/journal.pbio.0020347.txt:        Not all genetic variation is created equal. When Darwin first introduced the concept of
./technical/plos/journal.pbio.0020347.txt:        evolution (Darwin 1859), he challenged the prevailing view that species were fixed entities
./technical/plos/journal.pbio.0020346.txt:        on the traditional comparative approach, which was always the strength of Darwinian
./technical/plos/journal.pbio.0020046.txt:        answers to possible questions and criticisms to avoid stuttering. Charles Darwin also
./technical/plos/journal.pbio.0020046.txt:        stuttered; interestingly, his grandfather Erasmus Darwin suffered from the same condition,
./technical/plos/journal.pbio.0020302.txt:        turn to be consumed by predators. Darwinian evolution would result in many of the same
./technical/plos/journal.pbio.0020311.txt:        out by Charles Darwin and his son Francis in 1880. The Darwins were able to demonstrate
./technical/plos/journal.pbio.0020071.txt:        are many ideologically motivated books opposing natural selection and Darwinism. To
./technical/plos/journal.pbio.0020439.txt:        location within the head (Hsieh 2003). Charles Darwin was right when he wrote that people
./technical/plos/journal.pbio.0020439.txt:        extra sense” (F. Darwin 1905). Today's biologists increasingly recognize that appropriate
./technical/biomed/1471-2105-3-2.txt:        In the 1830's, Charles Darwin's investigation of the
./technical/biomed/1471-2105-3-2.txt:        In the 1970's, Woese and Fox revisited Darwinian
```

```
arnav@Arnavs-MacBook-Pro docsearch % grep -r "and therefore was" ./technical                
./technical/government/Gen_Account_Office/June30-2000_gg00135r.txt:customers, and therefore was in the process of improving the
./technical/biomed/1471-2407-1-19.txt:          NRP-154 (Figure 5, panels C and D), and therefore was
./technical/biomed/1471-2180-2-29.txt:          from a HCV genome in that region, and therefore was used
```

   `-r` option recursively searches for the given word or pattern (phrase) in a directory and or a group of files and systematically lists them out. The `-r` option is very useful as it enables the user to search through a directory instead of searching through each file individually.

2. `-e` option:

```
arnav@Arnavs-MacBook-Pro docsearch % grep -r  -e "Darwin" -e  "and therefore was" ./technical
./technical/government/Gen_Account_Office/June30-2000_gg00135r.txt:customers, and therefore was in the process of improving the
./technical/plos/journal.pbio.0020347.txt:        described by Charles Darwin (1859).
./technical/plos/journal.pbio.0020347.txt:        Not all genetic variation is created equal. When Darwin first introduced the concept of
./technical/plos/journal.pbio.0020347.txt:        evolution (Darwin 1859), he challenged the prevailing view that species were fixed entities
./technical/plos/journal.pbio.0020346.txt:        on the traditional comparative approach, which was always the strength of Darwinian
./technical/plos/journal.pbio.0020046.txt:        answers to possible questions and criticisms to avoid stuttering. Charles Darwin also
./technical/plos/journal.pbio.0020046.txt:        stuttered; interestingly, his grandfather Erasmus Darwin suffered from the same condition,
./technical/plos/journal.pbio.0020302.txt:        turn to be consumed by predators. Darwinian evolution would result in many of the same
./technical/plos/journal.pbio.0020311.txt:        out by Charles Darwin and his son Francis in 1880. The Darwins were able to demonstrate
./technical/plos/journal.pbio.0020071.txt:        are many ideologically motivated books opposing natural selection and Darwinism. To
./technical/plos/journal.pbio.0020439.txt:        location within the head (Hsieh 2003). Charles Darwin was right when he wrote that people
./technical/plos/journal.pbio.0020439.txt:        extra sense” (F. Darwin 1905). Today's biologists increasingly recognize that appropriate
./technical/biomed/1471-2407-1-19.txt:          NRP-154 (Figure 5, panels C and D), and therefore was
./technical/biomed/1471-2180-2-29.txt:          from a HCV genome in that region, and therefore was used
./technical/biomed/1471-2105-3-2.txt:        In the 1830's, Charles Darwin's investigation of the
./technical/biomed/1471-2105-3-2.txt:        In the 1970's, Woese and Fox revisited Darwinian
```

```
arnav@Arnavs-MacBook-Pro docsearch % grep -e "Charles Darwin" -e  "genetic variation" ./technical/plos/journal.pbio.0020347.txt
        described by Charles Darwin (1859).
        varieties, these ancient sources of genetic variation continue to provide the basic
        amount of time is to have access to a large and diverse pool of genetic variation.
        Not all genetic variation is created equal. When Darwin first introduced the concept of
        a good predictor of the extent of their genetic variation.
        closely related to the wild ancestors and embody a great deal more genetic variation than
        pool of genetic variation that will drive the future of plant improvement (Bessey 1906;
        At some level, the idea of using natural genetic variation found in wild species and
        exploration and utilization of natural genetic variation, expanding the genetic base of our
```

`-e` option allows the user to give multiple phrases to be searched simultaneously and displays the lines where at least one of the phrases given matches. `-e` option helps broaden the scope of our command when we might have to find all of the lines which contains at least one of the phrases

3. `-r` option:


4. `-r` option:
   




<br/><br/>
<br/><br/>
---
---
[^note]: ACADEMIC INTEGRITY NOTE: I have not used ChatGPT for this section and only referred to information provided by `man grep`. For general syntax of the options, I referred to web searches with a general search along the following line- "How does '-...' option of grep command work? ".




