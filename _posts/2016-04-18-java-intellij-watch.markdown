---
layout: page
description: Transfer resources on the fly with this one simple trick.
title:  "IntelliJ + File Watcher"
date:   2016-04-18 20:10:04 -0400
categories: java intelli mustache
---

## The Problem
You're developing a [Spark](http://sparkjava.com) application, and you're finding it annoying that you have to re-run your entire application each time you make a change to a resource file (template or js or css or other)

## A Solution
We will be combining a native OSX `cp` command with a configured IntelliJ plugin called "File Watcher".

### The File watcher Plugin
Find it in the plugins window. Restart IntelliJ.

Save this as `watchers.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<TaskOptions>
  <TaskOptions>
    <option name="arguments" value="&quot;$FilePath$&quot; &quot;$OutputPath$/$FileDirName$/$FileName$&quot;" />
    <option name="checkSyntaxErrors" value="true" />
    <option name="description" value="Copy Things" />
    <option name="exitCodeBehavior" value="ERROR" />
    <option name="fileExtension" value="*" />
    <option name="immediateSync" value="true" />
    <option name="name" value="Copy Watcher" />
    <option name="output" value="" />
    <option name="outputFilters">
      <array />
    </option>
    <option name="outputFromStdout" value="false" />
    <option name="program" value="/bin/cp" />
    <option name="scopeName" value="Changed Files" />
    <option name="trackOnlyRoot" value="false" />
    <option name="workingDir" value="$ProjectFileDir$" />
    <envs />
  </TaskOptions>
</TaskOptions>
```


Open your preferences pane. Under tools, there is now a tab called 'File Watchers'. Click the door with the green arrow to import. Import this file.

Congratulations, you're almost done.


### Mustache Template Engine Generation
Sadly, if you're working with Spark's Mustache template generation, template compilation happens once and not more than once. This means if you change a HTML file, you won't see the change until you restart your web server, which defeats the purpose. 

To get around this, where you're invoking `new MustacheTemplateEngine()`, either make a new class that overrides the render method, or turn this into an anonymous class:

```java
new MustacheTemplateEngine() {
    @Override
    public String render(ModelAndView modelAndView) {
        String viewName = modelAndView.getViewName();
        Mustache mustache = new DefaultMustacheFactory("templates").compile(viewName);
        StringWriter stringWriter = new StringWriter();
        try {
            mustache.execute(stringWriter, modelAndView.getModel()).close();
        } catch (IOException e) {
            throw new RuntimeIOException(e);
        }
        return stringWriter.toString();
    }
}
```

Using a new MustacheFactory object will effectively disable this template compilation caching mechanism. Clearly this should not be used for traffic-heavy websites.

Voila. You should now see your changes reflected immediately without the need for restarting your web server.