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
I see, 
**Part 2:**

Something that I've learned in this second half of CSE 15l is using VIM. Personally, I think that vim is a really cool program, but i still prefer using VS code or eclipse to edit my code. Also something cool that I've learned outside of class is that you can use markdown on Discord. You can use most of the markdown commands from the cheatsheet. 

