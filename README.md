
# UrlRewriteFilter
### Republish: Support jakarta.servlet 6.0
Forked from [paultuckey/urlrewritefilter](https://github.com/paultuckey/urlrewritefilter)
SpringBoot
Add the JitPack repository to your build file
```xml
<repositories>
    <repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
    </repository>
</repositories>
```
Add the dependency
```xml
<dependency>
    <groupId>com.github.moieo</groupId>
    <artifactId>urlrewritefilter</artifactId>
    <version>4.0.4-jakarta-servlet</version>
</dependency>
```
The following files need to be added to use in spring boot 3
```java
/**
 * @author : Moieo
 * @created : 2023-01-01
 **/

import jakarta.servlet.FilterConfig;
import jakarta.servlet.ServletException;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;
import org.tuckey.web.filters.urlrewrite.Conf;

/**
 * UrlRewriteFilter
 */
@Configuration
public class UrlRewriteFilter
    extends org.tuckey.web.filters.urlrewrite.UrlRewriteFilter {

  protected void loadUrlRewriter(FilterConfig filterConfig)
      throws ServletException {
    try {
      Resource res = new ClassPathResource("urlrewirte.xml");
      Conf conf = new Conf(filterConfig.getServletContext(),
                           res.getInputStream(), res.getFilename(), null);
      checkConf(conf);
    } catch (Exception ex) {}
  }
}

```
<hr />
### [UrlRewriteFilter Web Site](http://www.tuckey.org/urlrewrite/) | [Documentation](https://tuckey.org/urlrewrite/manual/4.0/index.html)


*Based on the popular and very useful [mod_rewrite](http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html) for apache, UrlRewriteFilter is a Java Web Filter for any J2EE compliant web application server (such as [Resin](http://caucho.com), [Orion](http://www.orionserver.com/) or [Tomcat](http://tomcat.apache.org/)), which allows you to rewrite URLs before they get to your code. It is a very powerful tool just like Apache's mod_rewrite.*

URL rewriting is very common with Apache Web Server (see [mod_rewrite's rewriting guide](http://httpd.apache.org/docs-2.0/misc/rewriteguide.html)) but has not been possible in most java web application servers. The main things it is used for are:

  * URL Tidyness / [URL Abstraction](https://tuckey.org/urlrewrite/manual/4.0/guide.html#urlabs) - keep URLs tidy irrespective of the underlying technology or framework (JSP, Servlet, Struts etc).
  * Browser Detection - Allows you to rewrite URLs based on request HTTP headers (such as user-agent or charset).
  * Date based rewriting - Allows you to forward or redirect to other URL's based on the date/time (good for planned outages).
  * Moved content - enable a graceful move of content or even a change in CMS.
  * Tiny/Friendly URL's (i.e. blah.com/latest can be redirected to blah.com/download/ver1.2.46.2/setup.exe)
  * A Servlet mapping engine (see [Method Invocation](https://tuckey.org/urlrewrite/manual/4.0/guide.html#method))


!UrlRewriteFilter uses an xml file, called urlrewrite.xml (it goes into the WEB-INF directory), for configuration.  Most parameters can be Perl5 style Regular Expressions or Wildcard Expressions. This makes it very powerful indeed.

See the [manual](https://tuckey.org/urlrewrite/manual/4.0/index.html) for more information.


## Quick Start

  * Add Maven dependency below or add <a href="http://central.maven.org/maven2/org/tuckey/urlrewritefilter/4.0.3/urlrewritefilter-4.0.3.jar">urlrewritefilter-4.0.3.jar</a> directly into your <b>WEB-INF/lib</b> directory.
```xml
    <dependency>
        <groupId>org.tuckey</groupId>
        <artifactId>urlrewritefilter</artifactId>
        <version>4.0.3</version>
    </dependency>
```
  * Add the following to your WEB-INF/web.xml (add it near the top above your servlet mappings (if you have any)): (see <a href="https://tuckey.org/urlrewrite/manual/4.0/index.html#filterparams">filter parameters</a> for more options)
```xml
    <filter>
        <filter-name>UrlRewriteFilter</filter-name>
        <filter-class>org.tuckey.web.filters.urlrewrite.UrlRewriteFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>UrlRewriteFilter</filter-name>
        <url-pattern>/*</url-pattern>
        <dispatcher>REQUEST</dispatcher>
        <dispatcher>FORWARD</dispatcher>
    </filter-mapping>
```
  * Add <b><a href="https://tuckey.org/urlrewrite/manual/4.0/urlrewrite.xml">urlrewrite.xml</a></b> into your WEB-INF directory. (src/main/webapp/WEB-INF/ for Maven users)
  * Restart the context.

You can visit http://127.0.0.1:8080/rewrite-status (or whatever the address of your local webapp and context) to see output (note: this page is only viewable from localhost).

<a href="http://www.jetbrains.com/idea/"><img src="http://www.jetbrains.com/img/logo_bw.gif" alt="The best Java IDE" border="0"/></a> IDE Sponsored by [JetBrains](http://www.jetbrains.com/)

Previously on Google Code: http://code.google.com/p/urlrewritefilter.
