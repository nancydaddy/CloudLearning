The download link of GWT SDK in www.gwtproject.org can not work because of web restriction from goverment.<br>
So this gwt folder is worked out. This fold contains all GWT source codes, the version may be 2.5 which is not up-to-date.<br>
<br>
Building steps as following：<br>
1. Install git client software and run git init command (don&#x27;t forget this command).<br>
2. Install gdk and set JAVA_HOME, CLASSPATH, PATH.<br>
3. Install ant and set ANT_HOME.<br>
4. run ant clean dist-dev command, building will fail and some failure about gwt-dev.jar will appeared.<br>
5. SOME CONFIGURATION FILES HAS BEEN CHANGED to pass through building by ant:<br>
    1) distro-source\build.xml, comments move command as below shows:<br>
      &lt;target name=&quot;merge_codeserver&quot;&gt;<br>
        &lt;echo message=&quot;Merge gwt-dev.jar and gwt-codeserver.jar&quot; /&gt;<br>
        &lt;gwt.jar destfile=&quot;${gwt.build.out}/gwt-dev-merged.jar&quot;&gt;<br>
          &lt;zipfileset src=&quot;${gwt.build.lib}/gwt-dev.jar&quot;/&gt;<br>
          &lt;zipfileset src=&quot;${gwt.build.lib}/gwt-codeserver.jar&quot;/&gt;<br>
        &lt;/gwt.jar&gt;<br>
        &lt;echo message=&quot;Overwriting gwt-dev.jar with merged gwt-dev.jar&quot; /&gt;<br>
        &lt;!--move file=&quot;${gwt.build.out}/gwt-dev-merged.jar&quot; tofile=&quot;${gwt.build.lib}/gwt-dev.jar&quot;/--&gt;<br>
      &lt;/target&gt;<br>
    2) common.ant.xml:<br>
         &lt;macrodef name=&quot;gwt.jar&quot;&gt;<br>
            &lt;attribute name=&quot;destfile&quot; default=&quot;${project.lib}&quot;/&gt;<br>
            &lt;attribute name=&quot;duplicate&quot; default=&quot;fail&quot;/&gt;<br>
            &lt;attribute name=&quot;update&quot; default=&quot;true&quot;/&gt;<br>
            &lt;element name=&quot;jarcontents&quot; implicit=&quot;true&quot;/&gt;<br>
            &lt;sequential&gt;<br>
              &lt;!--jar destfile=&quot;@{destfile}&quot; duplicate=&quot;@{duplicate}&quot; filesonly=&quot;false&quot;<br>
                  index=&quot;true&quot; update=&quot;@{update}&quot;&gt;<br>
                &lt;jarcontents/&gt;<br>
              &lt;/jar--&gt;<br>
              &lt;jar destfile=&quot;@{destfile}&quot; filesonly=&quot;false&quot;<br>
                  index=&quot;true&quot; update=&quot;@{update}&quot;&gt;<br>
                &lt;jarcontents/&gt;<br>
              &lt;/jar&gt;<br>
            &lt;/sequential&gt;<br>
          &lt;/macrodef&gt;<br>
6. run ant dist-dev again, no clean command this time.<br>
