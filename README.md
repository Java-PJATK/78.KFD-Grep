# KFD-Grep

Here, we don’t use classes from the java.nio package, but from an older (but still used
and still necessary) java.io package.  

There are some differences to be noted: class File which, to some extend, plays the rôle of the class Path from the java.nio.file package. Notice also, that Buffere-dReader must be created in two steps: first we create ‘raw’ byte stream of type, e.g., FileInputStream, then we pass it to the constructor of InputStreamReader with, as
the second argument, the required encoding, and then this to the constructor of the
BufferedReader. In the example above there are only two steps: to the constructor
of BufferedReader we pass directly an object of type FileReader, but then there is
no way to specify the encoding — default system encoding will be assumed. Note how
try-with-resources simplifies operations on IO streams; in the program above, we don’t
use it and therefore the somewhat complicated finally clause is needed (as close may
itself also throw an exception).


## KFD-Grep: Understanding java.io Package
Unlike the java.nio package, KFD-Grep utilizes the older but still essential java.io package.
  
**Key Differences:  
**Class File: Serves a similar purpose to the Path class from java.nio.file, representing files within the file system.  
BufferedReader Creation: It requires a two-step process:  
Create a ‘raw’ byte stream, such as FileInputStream.  
Pass it to InputStreamReader with the required encoding, and then to BufferedReader.  
  
**Example Breakdown:  
**In the given example, BufferedReader is created by directly passing a FileReader object, which does not allow specifying the encoding; thus, the system’s default encoding is used.  

**Try-With-Resources:  
**This Java feature simplifies IO stream operations by automatically closing resources, eliminating the need for a complex finally clause that handles resource closure and potential exceptions.
