The download link of GWT SDK in www.gwtproject.org can not work because of web restriction from goverment.
So this gwt folder is worked out. This fold contains all GWT source codes, the version may be 2.5 which is not up-to-date.

Building steps as following：
1. Install git client software and run git init command (don't forget this command).
2. Install gdk and set JAVA_HOME, CLASSPATH, PATH.
3. Install ant and set ANT_HOME.
4. run ant clean dist-dev command, building will fail and some failure about gwt-dev.jar will appeared.
5. SOME CONFIGURATION FILES HAS BEEN CHANGED to pass through building by ant:
    1) distro-source\build.xml, comments move command as below shows:
      <target name="merge_codeserver">
        <echo message="Merge gwt-dev.jar and gwt-codeserver.jar" />
        <gwt.jar destfile="${gwt.build.out}/gwt-dev-merged.jar">
          <zipfileset src="${gwt.build.lib}/gwt-dev.jar"/>
          <zipfileset src="${gwt.build.lib}/gwt-codeserver.jar"/>
        </gwt.jar>
        <echo message="Overwriting gwt-dev.jar with merged gwt-dev.jar" />
        <!--move file="${gwt.build.out}/gwt-dev-merged.jar" tofile="${gwt.build.lib}/gwt-dev.jar"/-->
      </target>
    
    2) common.ant.xml:
         <macrodef name="gwt.jar">
            <attribute name="destfile" default="${project.lib}"/>
            <attribute name="duplicate" default="fail"/>
            <attribute name="update" default="true"/>
            <element name="jarcontents" implicit="true"/>
            <sequential>
              <!--jar destfile="@{destfile}" duplicate="@{duplicate}" filesonly="false"
                  index="true" update="@{update}">
                <jarcontents/>
              </jar-->
              <jar destfile="@{destfile}" filesonly="false"
                  index="true" update="@{update}">
                <jarcontents/>
              </jar>

            </sequential>
          </macrodef>
6.run ant dist-dev again, no clean command this time.
