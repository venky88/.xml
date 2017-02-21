ivy.xml:
________________

<?xml version="1.0"?>
<ivy-module version="2.0">

 
    <info organisation="banking" module="sbl_opportunity" revision="${spark.release}" />
    <configurations>
        <conf name="runtime" visibility="public" description="Core runtime dependencies" />
        <conf name="build-main" visibility="public"         description="Default (base) build configuration" extends="runtime"/>
        <conf name="build-tests" visibility="public"            description="Base test case (junit) build configuration" extends="build-main" />
        <conf name="build-tests-unit" visibility="public"           description="Unit test case (junit) build configuration" extends="build-tests" />
        <conf name="build-tests-integration" visibility="public"            description="Integration test case (junit) build configuration" extends="build-tests" />
        <conf name="build-jar" visibility="public" extends="build-main"         description="Runtime dependencies for Jetty server" />
    </configurations>

    <publications>
        <artifact name="sbl_opportunity" type="jar" ext="jar"  conf="runtime" />
        <artifact name="sbl_opportunity" type="src" ext="src.jar" conf="runtime" />
    </publications>

    <dependencies>
       
      <dependency org="ossjava" name="junit" rev="default"    conf="runtime" /> 

      
 	
 	 <dependency org="hadoop" name="cdh" rev="5.5.0-ms1" 
        	conf="build-main->hive,hadoop-hdfs,hadoop-0.20-mapreduce,hadoop-mapreduce,hadoop-yarn,hadoop,parquet,spark" >
        </dependency>    
     
    </dependencies>
</ivy-module>



ivy.settings.xml

<?xml version="1.0"?>
<ivysettings>
	<properties file="${ivy.settings.dir}/build.properties"/>
    <include file="${msde.build-template.dir}/ivy-settings.xml" />

    <resolvers>
        <filesystem name="jai.dist" checkconsistency="false" checkmodified="true">
            <artifact pattern="//ms/dist/msjava/PROJ/eval/jai-[revision]/lib/[artifact].[ext]" />
        </filesystem>
        <filesystem name="hadoop.jars.dist" checkconsistency="false" checkmodified="true">
            <ivy pattern="//ms/dist/[organisation]/PROJ/[module]/[revision]/common/etc/ivys/ivy.xml" />
            <artifact pattern="//ms/dist/[organisation]/PROJ/[module]/[revision]/jars/[artifact].[ext]" />
        </filesystem>
    </resolvers>
    <modules>
        <module organisation="msjava" name="jai" resolver="jai.dist" />
        <module organisation="hadoop" name="cdh" resolver="hadoop.jars.dist" />
        <module organisation="banking" resolver="msde.resolvers.dist" />
    </modules>

    <settings defaultResolver="msde.resolvers.dist" />

</ivysettings>
