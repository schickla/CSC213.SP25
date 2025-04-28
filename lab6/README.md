# **Lab: Maven and `pom.xml` Implementation**  

## **Objectives**  

1. Use Maven to manage a Java project.  
2. Create and implement a `pom.xml` file.  

---

## **Step 1: Creating a Proper Project Structure**  

Look at `Book.java`. You will see that it resides at the root level of the project.  

When using Maven in a properly packaged Java project, you **must** follow the correct directory structure. This is true for Python projects as well, in case you were wondering!  

So, your first step is to **reorganize** your project so that it looks like this:  

```
lab6/
├── src/
│   └── main/
│       └── java/
│           └── Book.java
└── pom.xml
```

This is **key** for Maven projects—having the correct directory structure is crucial!  

---

## **Step 2: Running the Code**  

You will notice an immediate problem.  

If you open `Book.java`, you will see that the **imports are not found**, like this:  

```
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
```

### **How do we fix this?**  

Check the `pom.xml` file! You will see a comment indicating where dependencies can be added, but **there are none**.  

### **Task 1: Add a Dependency**  

You need to **add the dependency** for **Apache Commons Logging, version 1.2**. It’s up to you to find out how to do it! 💡  

_Hint: Google "Maven dependency Apache Commons Logging 1.2" and add it to your `pom.xml`._  

---

## **Step 3: Running Maven**  

Now that you have added the dependency in `pom.xml`, it’s time to **use Maven!**  

On the left-hand side, locate your **Maven project** in the file tree. You will see a section with **Lifecycle options**:  

### **Maven Lifecycle Commands**  

| Command    | Description |
|------------|------------|
| `validate` | Checks the project's configuration (`pom.xml`) to ensure it's valid. |
| `compile`  | Compiles all Java source files in `src/main/java/`, generating `.class` files in `target/classes/`. |
| `clean`    | Deletes the `target/` directory, removing compiled files and built artifacts. |
| `install`  | Installs the project's artifacts (JARs, WARs, etc.) into the local Maven repository (`~/.m2/repository`). |

### **What does `install` do?**  
It runs multiple steps in one:  

1. **Validate** - Ensures the project is correctly set up.  
2. **Compile** - Compiles the main source code.  
3. **Test** - Executes the tests in the project.  
4. **Package** - Packages the compiled code into a JAR or WAR file.  
5. **Integration-test** - Runs integration tests.  
6. **Verify** - Checks the package against quality standards.  
7. **Install** - Places the package in the local Maven repository for reuse.  

### **Run the Commands!**  

A typical Maven sequence is:  

```
mvn validate
mvn clean
mvn install
```

### **What happens after `install`?**  

Check your project directory. You will see a new folder called `target/`. Open it and examine its contents—you should see a JAR file named **`Lab6-1.jar`**.  

This JAR file is the **output** of the build process. Its name is determined by attributes in the `pom.xml` file, which define the **artifact name**.  

### **Try Running the JAR File**  

From the terminal, navigate (`cd`) into the `target/` directory, then run:  

```sh
java -jar Lab6-1.jar
```

Not much happens, right? That’s because this JAR file is **not yet executable**. Let’s fix that!  

---

## **Task 2: Making a Runnable JAR File**  

You need to modify your `pom.xml` to **add a custom build**. This will generate an **executable JAR file**—one that runs the `main` method of `Book.java`.  

But remember:  
- It needs to **include third-party dependencies** (like Apache Commons Logging).
- Here, you are making what is called an uber jar.  It has everything a person needs to run it!  
- The output JAR file **must** be named:  

  ```
  Lab6-1-jar-with-dependencies.jar
  ```

How do you do this? **Google it!** Or ask ChatGPT. 😉  

### **After Making the Changes**  

1. Rebuild the project.  
2. Run the new JAR file:  

   ```sh
   java -jar Lab6-1-jar-with-dependencies.jar
   ```

If it works, it will print **information about "The Great Gatsby"!** 📖✨  

---

## **Step 4: Add Your Jar to D2L**  

If you have completed everything and you see that message about the Great Gatsby, simply upload the Lab6-1-jar-with-dependencies.jar to D2L.
