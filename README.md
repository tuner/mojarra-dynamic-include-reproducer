# Reproducer for JSF dynamic composite component inclusion problem

N.B. This problem has finally been fixed! See:

* [Mojarra 2.2](https://github.com/javaserverfaces/mojarra/commit/14e87ea57319012f02f0e3b09522d67c6d960378) - Included in 2.2.8-22
* [Mojarra 2.3](https://github.com/javaserverfaces/mojarra/commit/5cddde673f2257f3700b1ede6d44afaaa42e8fab) - Included in 2.3.1

Dynamic inclusion of composite components by using either c:if or ui:include cause the following exception in
certain circumstances:
`javax.servlet.ServletException: Component ID *xxxxxx* has already been found in the view.`

See the following issues in Mojarra GitHub issue tracking:

1. [Duplicate ID exception when using composite component with c:if](https://github.com/javaserverfaces/mojarra/issues/4244)
1. [Error Component already found when using c:if in composite components](https://github.com/javaserverfaces/mojarra/issues/4076)
1. [Using c:if: Component ID * has already been found in the view](https://github.com/javaserverfaces/mojarra/issues/3982)
1. [Dynamic `<ui:include>` duplicates a composite component](https://github.com/javaserverfaces/mojarra/issues/3944)
1. [Dynamic Composite Component in ui:include lead to duplicate id Exception](https://github.com/javaserverfaces/mojarra/issues/4208)

The problem has also been discussed at Stack Overflow:
* [Duplicate component ID in JSF using composite component twice in view](http://stackoverflow.com/questions/33258296/duplicate-component-id-in-jsf-using-composite-component-twice-in-vie)
* [Duplicate ID exception when using <c:if> with composite component](http://stackoverflow.com/questions/42863043/duplicate-id-exception-when-using-cif-with-composite-component)

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

Some of my findings are reported in a mail that I sent to mojarra dev list: https://java.net/projects/javaserverfaces/lists/dev/archive/2016-04/message/0
