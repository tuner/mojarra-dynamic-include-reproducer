# Reproducer for JSF dynamic composite component inclusion problem

Dynamic inclusion of composite components by using either c:if or ui:include cause the following exception in
certain circumstances:
`javax.servlet.ServletException: Component ID *xxxxxx* has already been found in the view.`

See the following issues in Mojarra JIRA:

1. [JAVASERVERFACES-4072](https://java.net/jira/browse/JAVASERVERFACES-4072)
2. [JAVASERVERFACES-3978](https://java.net/jira/browse/JAVASERVERFACES-3978)
3. [JAVASERVERFACES-3940](https://java.net/jira/browse/JAVASERVERFACES-3940)

This reproducer triggers an exception with the following Mojarra releases:

* 2.1.22
* 2.2.1
* 2.3.0-m05

However, earlier releases are not affected:

* 2.1.21
* 2.2.0

MyFaces (2.2.9) works without problems.

I believe that the problem is related to the fix of issue
[JAVASERVERFACES-2494](https://java.net/jira/browse/JAVASERVERFACES-2494).
It was applied to both 2.1.22 and 2.2.1, and it introduced optimizations to handling of dynamic components.
