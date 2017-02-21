# .xml
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
