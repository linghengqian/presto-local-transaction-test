# presto-local-transaction-test

- For https://github.com/apache/shardingsphere/pull/35504 and https://github.com/prestodb/presto/issues/25204 .
- Execute the following PowerShell 7 command on the `Windows 11 Home 24H2` instance with `PowerShell/PowerShell`,
  `version-fox/vfox`, `git-for-windows/git` and `rancher-sandbox/rancher-desktop` installed.

```shell
vfox add java
vfox install java@21.0.7-ms
vfox use --global java@21.0.7-ms

git clone git@github.com:linghengqian/presto-local-transaction-test.git
cd ./presto-local-transaction-test/
./mvnw clean test -T 1C
```

- The log is as follows.

```shell
PS D:\TwinklingLiftWorks\git\public\presto-local-transaction-test> ./mvnw clean test -T 1C
[INFO] Scanning for projects...       
[INFO] 
[INFO] Using the MultiThreadedBuilder implementation with a thread count of 16
[INFO] 
[INFO] -------< com.github.linghengqian:presto-local-transaction-test >--------
[INFO] Building presto-local-transaction-test 1.0-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- clean:3.2.0:clean (default-clean) @ presto-local-transaction-test ---
[INFO] Deleting D:\TwinklingLiftWorks\git\public\presto-local-transaction-test\target
[INFO]
[INFO] --- resources:3.3.1:resources (default-resources) @ presto-local-transaction-test ---
[INFO] skip non existing resourceDirectory D:\TwinklingLiftWorks\git\public\presto-local-transaction-test\src\main\resources
[INFO]
[INFO] --- compiler:3.13.0:compile (default-compile) @ presto-local-transaction-test ---
[INFO] No sources to compile
[INFO]
[INFO] --- resources:3.3.1:testResources (default-testResources) @ presto-local-transaction-test ---
[INFO] Copying 2 resources from src\test\resources to target\test-classes
[INFO]
[INFO] --- compiler:3.13.0:testCompile (default-testCompile) @ presto-local-transaction-test ---
[INFO] Recompiling the module because of changed source code.
[INFO] Compiling 1 source file with javac [debug release 21] to target\test-classes
[INFO] 
[INFO] --- surefire:3.2.5:test (default-test) @ presto-local-transaction-test ---
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.github.linghengqian.PrestoTest
6月 15, 2025 4:16:22 下午 org.junit.jupiter.engine.descriptor.AbstractExtensionContext lambda$createCloseAction$1
警告: Type implements CloseableResource but not AutoCloseable: org.testcontainers.junit.jupiter.TestcontainersExtension$StoreAdapter
[ERROR] Tests run: 1, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 15.65 s <<< FAILURE! -- in com.github.linghengqian.PrestoTest
[ERROR] com.github.linghengqian.PrestoTest.assertLocalTransactions -- Time elapsed: 15.44 s <<< FAILURE!
java.lang.AssertionError:

Expected: is <true>
     but: was <false>
        at org.hamcrest.MatcherAssert.assertThat(MatcherAssert.java:18)
        at org.hamcrest.MatcherAssert.assertThat(MatcherAssert.java:6)
        at com.github.linghengqian.PrestoTest.assertRollbackWithTransactions(PrestoTest.java:97)
        at com.github.linghengqian.PrestoTest.assertLocalTransactions(PrestoTest.java:38)
        at java.base/java.lang.reflect.Method.invoke(Method.java:580)
        at java.base/java.util.ArrayList.forEach(ArrayList.java:1596)
        at java.base/java.util.ArrayList.forEach(ArrayList.java:1596)

[INFO] 
[INFO] Results:
[INFO]
[ERROR] Failures: 
[ERROR]   PrestoTest.assertLocalTransactions:38->assertRollbackWithTransactions:97 
Expected: is <true>
     but: was <false>
[INFO]
[ERROR] Tests run: 1, Failures: 1, Errors: 0, Skipped: 0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.088 s (Wall Clock)
[INFO] Finished at: 2025-06-15T16:16:23+08:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:3.2.5:test (default-test) on project presto-local-transaction-test: There are test failures.
[ERROR]
[ERROR] Please refer to D:\TwinklingLiftWorks\git\public\presto-local-transaction-test\target\surefire-reports for the individual test results.
[ERROR] Please refer to dump files (if any exist) [date].dump, [date]-jvmRun[N].dump and [date].dumpstream.
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoFailureException
```
