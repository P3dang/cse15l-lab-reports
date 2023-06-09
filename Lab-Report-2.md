# Part 1
Code for StringServer:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String num = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("%s", num);
        } else if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            num += parameters[1]+"\n";
            return String.format("%s, Message has been added!", parameters[1]);
        
            }
            return "404 Not Found!";
        }
    }


class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

Examples of using `/add-message`:

![Image](Screen Shot 2023-05-10 at 9.00.30 PM.png)

In order for me to run this code, I would first have to compile both StringServer.java and Server.java. The revelent arguments are `/add-message?s=<string>` which is added to the end of the URL to add a string of your choice. Within my code a relevent field is the num, whichs holds the String that are being printed on the local URL. Also I added hello by adding `/add-message?s=Hello` to the end of my URL.

![Image](Screen Shot 2023-05-10 at 9.02.35 PM.png)

The methods that are being called in this code is StringServer.java and Server.java. The relevent arguments in this screenshot are `/add-message?s=elloH`, and a relevent field is the nums field holding the String of words in the URL. 
# Part 2 

Code before changes:
```
public class ArrayExamples {

  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
Failure-inducting input:
```
  @Test 
  public void testReverseInPlace1() {
    int[] input1 = { 3 , 2 , 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1 , 2 , 3 }, input1);
  }
```
[Image](Screen Shot 2023-04-24 at 8.41.12 PM.png)
Non-failure input: 
```
	@Test 
	public void testReverseInPlace() {
    	  int[] input1 = { 3 };
   	  ArrayExamples.reverseInPlace(input1);
    	  assertArrayEquals(new int[]{ 3 }, input1);
	}
```
Result after running the test on ORIGINAL code:
``` 
phuoc@Phuocs-MacBook-Air lab3-main % java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
.E
Time: 0.004
There was 1 failure:
1) testReverseInPlaceMod2(ArrayTests)
arrays first differed at element [2]; expected:<3> but was:<1>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlaceMod2(ArrayTests.java:30)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<3> but was:<1>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more

FAILURES!!!
Tests run: 1,  Failures: 1
```
[Image](Screen Shot 2023-04-24 at 8.39.48 PM.png)
Working modified code: 
```
 public class ArrayExamples {
  static int[] reverseInPlaceMod(int[] arr) {
    int temp = arr[0];


    for(int i = 0; i < arr.length; i += 1) {
      if (arr.length - i - 1 == 0){ 
        arr[i] = temp;
      }
      else { 
      arr[i] = arr[arr.length - i - 1];
    }
    
    
  }
    return arr;
}
}

```
Test for moddified code:
```
  @Test 
	public void testReverseInPlaceMod1() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlaceMod(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}

  @Test 
  public void testReverseInPlaceMod2() {
    int[] input1 = { 3 , 2 , 1 };
    ArrayExamples.reverseInPlaceMod(input1);
    assertArrayEquals(new int[]{1 , 2 , 3 }, input1);
  }
```
Result after running the MODDIfIED code: 
```
phuoc@Phuocs-MacBook-Air lab3-main % java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
..
Time: 0.003

OK (2 tests)
```
[Image](Screen Shot 2023-04-24 at 8.37.38 PM.png)
Solution: 
The initial bug of this code was that when iterating through the list, the last element of the new array would be the first element of the new list instead newly modified array. For example when reversing { 1 , 2 , 3 } the program would return { 3 , 2 , 3 }. My fix was to add an if statment checking if the index is at 0, if so, instead of looking through the array for the first varriable it would add the varriable that was assgined the first element of the old array.   

# Part 3 
Something that I've learned from the past few weeks in CSE 15l is how to create local server. Also implemeting code to modify the servers such as changing the count by any number. I've also learned how to write @Test in Junit even though I'm in CSE 12, I was really behind on the PAs.

