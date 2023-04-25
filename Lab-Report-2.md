# Part 1


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
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}

  @Test 
  public void testReverseInPlaceMod2() {
    int[] input1 = { 3 , 2 , 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1 , 2 , 3 }, input1);
  }
```
[Image](Screen Shot 2023-04-24 at 8.37.38 PM.png)
Solution: 
The initial bug of this code was that when iterating through the list, the last element of the new array would be the first element of the new list instead newly modified array. For example when reversing { 1 , 2 , 3 } the program would return { 3 , 2 , 3 }. My fix was to add an if statment checking if the index is at 0, if so, instead of looking through the array for the first varriable it would add the varriable that was assgined the first element of the old array.   

# Part 3 
Something that I've learned from the past few weeks in CSE 15l is how to create local server. Also implemeting code to modify the servers such as changing the count by any number. I've also learned how to write @Test in Junit even though I'm in CSE 12, I was really behind on the PAs.

