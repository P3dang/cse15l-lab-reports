**Part 1:**
Step #1
What environment are you using(computer, operating system, web browser, terminal/editor, and so on)?
- I am working on a macbook with VS code. Chrome > Safari.

Detail the symptom you’re seeing. Be specific; include both what you’re seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn’t work”.
```
phuoc@Phuocs-MacBook-Air hehe3 % bash grade.sh                                                        
fatal: repository 'student-submission' does not exist
Finished cloning
Files moved successfully to grading-area.
cp: student-submission/ListExamples.java: No such file or directory
TestListExamples.java:17: error: cannot find symbol
    List<String> merged = ListExamples.merge(left, right);
                          ^
  symbol:   variable ListExamples
  location: class TestListExamples
TestListExamples.java:26: error: cannot find symbol
    List<String> merged = ListExamples.merge(left, right);
                          ^
  symbol:   variable ListExamples
  location: class TestListExamples
TestListExamples.java:35: error: cannot find symbol
    List<String> filtered = ListExamples.filter(input, new IsMoon());
                            ^
  symbol:   variable ListExamples
  location: class TestListExamples
TestListExamples.java:43: error: cannot find symbol
    List<String> filtered = ListExamples.filter(input, new IsMoon());
                            ^
  symbol:   variable ListExamples
  location: class TestListExamples
4 errors
JUnit version 4.13.2
.E.E.E.E
Time: 0.006
There were 4 failures:
1) testFilterMulti(TestListExamples)
java.lang.NoClassDefFoundError: ListExamples
        at TestListExamples.testFilterMulti(TestListExamples.java:43)
        ... 9 trimmed
Caused by: java.lang.ClassNotFoundException: ListExamples
        at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:641)
        at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:188)
        at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
        ... 11 more
2) testFilterSingle(TestListExamples)
java.lang.NoClassDefFoundError: ListExamples
        at TestListExamples.testFilterSingle(TestListExamples.java:35)
        ... 9 trimmed
Caused by: java.lang.ClassNotFoundException: ListExamples
        ... 11 more
3) testMergeRightEnd(TestListExamples)
java.lang.NoClassDefFoundError: ListExamples
        at TestListExamples.testMergeRightEnd(TestListExamples.java:17)
        ... 9 trimmed
Caused by: java.lang.ClassNotFoundException: ListExamples
        ... 11 more
4) testMergeLeftEnd(TestListExamples)
java.lang.NoClassDefFoundError: ListExamples
        at TestListExamples.testMergeLeftEnd(TestListExamples.java:26)
        ... 9 trimmed
Caused by: java.lang.ClassNotFoundException: ListExamples
        ... 11 more

FAILURES!!!
Tests run: 4,  Failures: 4
```
The error seems like my terminal can't find ListExamples. I am expecting to see `ok ( 4 tests )`. 

Detail the failure-inducing input and context. That might mean any or all of the command you’re running, a test case, command-line arguments, working directory, even the last few commands you ran. DO your best to provide as much context as you can. 

Here is my current grade.sh:
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'


# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
if [[ -e student-submission/ListExamples.java ]] 
    then echo "Submit correctly"

fi

# cp student-submission/* grading-area
if [ $? -eq 0 ]
    then echo "Files moved successfully to grading-area."

fi

cp student-submission/ListExamples.java ./

javac -cp $CPATH *.java

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 
```
<img width="170" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/c6a5a24b-ccfe-400f-adab-9cfefd698833">

This was the code, me and my partner used during our lab. This code was supposed to work, but when I ran it on my computer the error above occurred. Im not sure why, but from the code I `git clone $1 student-submission` and then `cp student-submission/ListExamples.java ./`, so Im not sure why ListExamples.java isn't showing up in my directory. 

Step #2
I see, this could possibly be because the ListExample.java was never in your directory, so `cp student-submission/ListExamples.java ./` does nothing and returns an error. Maybe trying importing ListExamples. Since ListExamples.java isn't present in your directory, all the test failed since its missing the file. 

Step #3
```
phuoc@Phuocs-MacBook-Air hehe3 % bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
Cloning into 'student-submission'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
Submit correctly
Files moved successfully to grading-area.
JUnit version 4.13.2
....
Time: 0.005

OK (4 tests)
```
I imported the file, and now all my test passed successfully. The bug was that since ListExample.java wasn't in the files, the program couldn't copy ListExamples.java into student submission and run the test. 

Step #4
<img width="169" alt="image" src="https://github.com/P3dang/cse15l-lab-reports/assets/130012963/e2e63c08-aff5-4f3f-a51f-6fde170d204e">

GradeServer.java:
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {

  /**
    Takes an input stream, reads the full stream, and returns the result as a
    string.

    In Java 9 and later, new String(out.readAllBytes()) would be a better
    option, but using Java 8 for compatibility with ieng6.
  */
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
      System.out.println(System.currentTimeMillis() + "; just read: " + (char)c);
    }
    return result;
  }

  /**
    Takes a command, represented as an array of strings as it would by typed at
    the command line, runs it, and returns its combined stdout and stderr as a
    string.
  */
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream out = p.getInputStream();
    return String.format("%s\n", streamToString(out));
  }

}

class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               return ExecHelpers.exec(new String[]{"bash", "grade.sh", parameters[1]});
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
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
Grade.sh
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'


# Draw a picture/take notes on the directory structure that's set up after
# getting to this point

# Then, add here code to compile and run, and do any post-processing of the
# tests
if [[ -e student-submission/ListExamples.java ]] 
    then echo "Submit correctly"

fi

# cp student-submission/* grading-area
if [ $? -eq 0 ]
    then echo "Files moved successfully to grading-area."

fi

cp student-submission/ListExamples.java ./

javac -cp $CPATH *.java

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 
```
ListExamples.java 
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```
TestListExamples.java
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "z");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "d", "z");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testFilterSingle() {
    List<String> input = Arrays.asList("Moon", "MOO", "moo");
    List<String> expect = Arrays.asList("Moon");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);
  }

  @Test(timeout = 500)
  public void testFilterMulti() {
    List<String> input = Arrays.asList("Moon", "MOO", "moon", "MOON");
    List<String> expect = Arrays.asList("Moon", "moon", "MOON");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);
  }
}
```
I ran `bash grade.sh` into the terminal of VS code. What fixed the bug was importing in ListExamples.java so that the TestListExamples.java would work. 

**Part 2:**

Something that I've learned in this second half of CSE 15l is using VIM. Personally, I think that vim is a really cool program, but i still prefer using VS code or eclipse to edit my code. Also something cool that I've learned outside of class is that you can use markdown on Discord. You can use most of the markdown commands from the cheatsheet. 

