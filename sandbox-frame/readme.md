To run mvn clean test in sandbox-frame-master, since mvn.twttr.com cannot be accessed, you have to modify c:\windows\system\drivers\etc\hosts file:
by adding below line:<br>
<br>
199.16.156.89 maven.twttr.com<br>
<br>
You can also add aliyun's maven repository into settings.xml in maven's conf folder:<br>
&lt;mirror&gt;<br>
    &lt;id&gt;nexus-aliyun&lt;/id&gt;<br>
    &lt;mirrorOf&gt;*&lt;/mirrorOf&gt;<br>
    &lt;name&gt;Nexus aliyun&lt;/name&gt;<br>
    &lt;url&gt;http://maven.aliyun.com/nexus/content/groups/public&lt;/url&gt;<br>
&lt;/mirror&gt;<br>
　　
