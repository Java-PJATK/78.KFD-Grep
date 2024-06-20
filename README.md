## Listing 78 KFD-Grep/Grep.java

For completeness, another version of essentially the same program is shown below.

Here, we don’t use classes from the java.nio package, but from an older (but still used and still necessary) java.io package.

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class Grep {
    public static void main(String[] args) {
        File filein = new File("alice.txt");
        String wordSearchedFor = "Cheshire";

        if ( !filein.exists()     ||
             !filein.canRead()    ||
              filein.isDirectory()  ) {
            System.out.println("Invalid input file !!!");
            System.exit(1);
        }
        File fileou = new File("grep_" + filein.getName());
        BufferedReader br = null;
        BufferedWriter bw = null;
        String LF=System.getProperty("line.separator");

        try {
            br = new BufferedReader(
                     new FileReader(filein));
            bw = new BufferedWriter(
                     new FileWriter(fileou));
            String line;
            int lineNo = 0;
            while ( (line = br.readLine()) != null) {
                ++lineNo;
                if (line.indexOf(wordSearchedFor) >=0)
                    bw.write(String.format("Line %2d: %s%s",
                                           lineNo,line,LF));
            }

        } catch (IOException e) {
            System.out.println("Problems with reading");
        } finally {
            try { if (br != null) br.close(); }
            catch(IOException ignore) { }
            try { if (bw != null) bw.close(); }
            catch(IOException ignore) { }
            System.out.println("Results written to " +
                            fileou.getAbsolutePath());
        }
    }
}
```

https://github.com/Java-PJATK/78.KFD-Grep/blob/main/alice.txt

https://github.com/Java-PJATK/78.KFD-Grep/blob/main/grep_alice.txt

There are some differences to be noted: `class File` which, to some extent, plays the rôle of the `class Path` from the `java.nio.file` package. Notice also, that `BufferedReader` must be created in two steps: first, we create a ‘raw’ byte stream of type, e.g., `FileInputStream`, then we pass it to the constructor of `InputStreamReader` with, as the second argument, the required encoding, and then this to the constructor of the `BufferedReader`. 

In the example above there are only two steps: to the constructor of `BufferedReader` we pass directly an object of type `FileReader`, but then there is no way to specify the encoding — default system encoding will be assumed. Note how try-with-resources simplifies operations on IO streams; in the program above, we don’t use it and therefore the somewhat complicated `finally` clause is needed (as `close` may itself also throw an exception).


## KFD-Grep: Understanding java.io Package
Unlike the java.nio package, KFD-Grep utilizes the older but still essential java.io package.
  
Key Differences:  
  
Class File:  
Serves a similar purpose to the Path class from java.nio.file, representing files within the file system.  
BufferedReader  
  
Creation: It requires a two-step process:  
Create a ‘raw’ byte stream, such as FileInputStream.  
Pass it to InputStreamReader with the required encoding, and then to BufferedReader.  
  
Example Breakdown:  
In the given example, BufferedReader is created by directly passing a FileReader object, which does not allow specifying the encoding; thus, the system’s default encoding is used.  
  
Try-With-Resources:  
This Java feature simplifies IO stream operations by automatically closing resources, eliminating the need for a complex finally clause that handles resource closure and potential exceptions.
