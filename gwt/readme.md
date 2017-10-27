The download link of GWT SDK in www.gwtproject.org can not work because of web restriction from goverment.
So this gwt folder is worked out. This fold contains all GWT source codes, the version may be 2.5 which is not up-to-date.

Building steps as following：
1. Install git client software and run git init command (don&#x27;t forget this command).
2. Install gdk and set JAVA_HOME, CLASSPATH, PATH.
3. Install ant and set ANT_HOME.
4. run ant clean dist-dev command, building will fail and some failure about gwt-dev.jar will appeared.
5. SOME CONFIGURATION FILES HAS BEEN CHANGED to pass through building by ant:
    1) distro-source\build.xml, comments move command as below shows:
      &lt;target name=&quot;merge_codeserver&quot;&gt;
        &lt;echo message=&quot;Merge gwt-dev.jar and gwt-codeserver.jar&quot; /&gt;
        &lt;gwt.jar destfile=&quot;${gwt.build.out}/gwt-dev-merged.jar&quot;&gt;
          &lt;zipfileset src=&quot;${gwt.build.lib}/gwt-dev.jar&quot;/&gt;
          &lt;zipfileset src=&quot;${gwt.build.lib}/gwt-codeserver.jar&quot;/&gt;
        &lt;/gwt.jar&gt;
        &lt;echo message=&quot;Overwriting gwt-dev.jar with merged gwt-dev.jar&quot; /&gt;
        &lt;!--move file=&quot;${gwt.build.out}/gwt-dev-merged.jar&quot; tofile=&quot;${gwt.build.lib}/gwt-dev.jar&quot;/--&gt;
      &lt;/target&gt;
    2) common.ant.xml:
         &lt;macrodef name=&quot;gwt.jar&quot;&gt;
            &lt;attribute name=&quot;destfile&quot; default=&quot;${project.lib}&quot;/&gt;
            &lt;attribute name=&quot;duplicate&quot; default=&quot;fail&quot;/&gt;
            &lt;attribute name=&quot;update&quot; default=&quot;true&quot;/&gt;
            &lt;element name=&quot;jarcontents&quot; implicit=&quot;true&quot;/&gt;
            &lt;sequential&gt;
              &lt;!--jar destfile=&quot;@{destfile}&quot; duplicate=&quot;@{duplicate}&quot; filesonly=&quot;false&quot;
                  index=&quot;true&quot; update=&quot;@{update}&quot;&gt;
                &lt;jarcontents/&gt;
              &lt;/jar--&gt;
              &lt;jar destfile=&quot;@{destfile}&quot; filesonly=&quot;false&quot;
                  index=&quot;true&quot; update=&quot;@{update}&quot;&gt;
                &lt;jarcontents/&gt;
              &lt;/jar&gt;

            &lt;/sequential&gt;
          &lt;/macrodef&gt;
6. run ant dist-dev again, no clean command this time.
