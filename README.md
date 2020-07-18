# Spring-Inner-Bean-Injection-Example
Spring-Inner-Bean-Injection-Example


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://maven.apache.org/POM/4.0.0"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.docsconsole.tutorials.spring5</groupId>
    <artifactId>Spring-Inner-Bean-Injection-Example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <springframework.version>5.2.7.RELEASE</springframework.version>
        <maven.war.plugin.version>3.2.2</maven.war.plugin.version>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>


    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${springframework.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context-support</artifactId>
            <version>${springframework.version}</version>
        </dependency>

    </dependencies>

    <build>
        <pluginManagement>
            <plugins>

                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-war-plugin</artifactId>
                    <version>${maven.war.plugin.version}</version>
                    <configuration>
                        <warSourceDirectory>src/main/webapp</warSourceDirectory>
                        <warName>${project.artifactId}</warName>
                        <failOnMissingWebXml>false</failOnMissingWebXml>
                    </configuration>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
</project>




package com.docsconsole.spring5.innerbean.xml.constructorinjectior;

public class AInnerSpringBean {

    private String beanName;

    public String getBeanName() {
        return beanName;
    }

    public void setBeanName(String beanName) {
        this.beanName = beanName;
    }
}



package com.docsconsole.spring5.innerbean.xml.constructorinjectior;

public class ASpringBean {

    private AInnerSpringBean aInnerSpringBean;

    public AInnerSpringBean getaInnerSpringBean() {
        return aInnerSpringBean;
    }

    public void setaInnerSpringBean(AInnerSpringBean aInnerSpringBean) {
        this.aInnerSpringBean = aInnerSpringBean;
    }

    public ASpringBean(AInnerSpringBean aInnerSpringBean){
        this.aInnerSpringBean = aInnerSpringBean;
    }
}




package com.docsconsole.spring5.innerbean.xml.constructorinjectior;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans1.xml");
        ASpringBean aSpringBean = (ASpringBean) context.getBean("aSpringBean");
        AInnerSpringBean AInnerSpringBean = aSpringBean.getaInnerSpringBean();
        AInnerSpringBean.setBeanName("Testing InnerSpringBean with constructor injection");
        System.out.println(aSpringBean.getaInnerSpringBean().getBeanName());
        context.close();

    }
}






package com.docsconsole.spring5.innerbean.xml.setterinjection;

public class AInnerSpringBean  {

    private String beanName;

    public String getBeanName() {
        return beanName;
    }

    public void setBeanName(String beanName) {
        this.beanName = beanName;
    }
}








package com.docsconsole.spring5.innerbean.xml.setterinjection;

public class ASpringBean {

    private AInnerSpringBean aInnerSpringBean;

    public AInnerSpringBean getaInnerSpringBean() {
        return aInnerSpringBean;
    }

    public void setaInnerSpringBean(AInnerSpringBean aInnerSpringBean) {
        this.aInnerSpringBean = aInnerSpringBean;
    }
}






package com.docsconsole.spring5.innerbean.xml.setterinjection;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans.xml");
        ASpringBean aSpringBean = (ASpringBean) context.getBean("aSpringBean");
        AInnerSpringBean AInnerSpringBean = aSpringBean.getaInnerSpringBean();
        AInnerSpringBean.setBeanName("Testing InnerSpringBean with setter injection");
        System.out.println(aSpringBean.getaInnerSpringBean().getBeanName());
        context.close();

    }
}






<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean" class="com.docsconsole.spring5.innerbean.xml.setterinjection.ASpringBean">
        <property name="aInnerSpringBean">
            <bean id="aInnerSpringBean" class="com.docsconsole.spring5.innerbean.xml.setterinjection.AInnerSpringBean"></bean>
        </property>
    </bean>

</beans>





<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean" class="com.docsconsole.spring5.innerbean.xml.constructorinjectior.ASpringBean">
        <constructor-arg>
            <bean id="aInnerSpringBean" class="com.docsconsole.spring5.innerbean.xml.constructorinjectior.AInnerSpringBean"></bean>
        </constructor-arg>
    </bean>
</beans>





C:\USERS\D951857\WORKSPACE\SPRINGCOREWS\SPRING-INNER-BEAN-INJECTION-EXAMPLE
|   pom.xml
|   Spring-Inner-Bean-Injection-Example.iml
|
+---.idea
|       .gitignore
|       compiler.xml
|       jarRepositories.xml
|       misc.xml
|       uiDesigner.xml
|       workspace.xml
|
+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---docsconsole
|   |   |           \---spring5
|   |   |               \---innerbean
|   |   |                   \---xml
|   |   |                       +---constructorinjectior
|   |   |                       |       AInnerSpringBean.java
|   |   |                       |       ASpringBean.java
|   |   |                       |       MainAppClient.java
|   |   |                       |
|   |   |                       \---setterinjection
|   |   |                               AInnerSpringBean.java
|   |   |                               ASpringBean.java
|   |   |                               MainAppClient.java
|   |   |
|   |   \---resources
|   |           spring-beans.xml
|   |           spring-beans1.xml
|   |
|   \---test
|       \---java
\---target
    |   Spring-Inner-Bean-Injection-Example-1.0-SNAPSHOT.jar
    |
    +---classes
    |   |   spring-beans.xml
    |   |   spring-beans1.xml
    |   |
    |   \---com
    |       \---docsconsole
    |           \---spring5
    |               \---innerbean
    |                   +---annotations
    |                   |       AppConfig.class
    |                   |       ASpringBean.class
    |                   |       MainAppClient.class
    |                   |
    |                   \---xml
    |                       +---constructorinjectior
    |                       |       AInnerSpringBean.class
    |                       |       ASpringBean.class
    |                       |       MainAppClient.class
    |                       |
    |                       \---setterinjection
    |                               AInnerSpringBean.class
    |                               ASpringBean.class
    |                               MainAppClient.class
    |
    +---generated-sources
    |   \---annotations
    +---maven-archiver
    |       pom.properties
    |
    \---maven-status
        \---maven-compiler-plugin
            +---compile
            |   \---default-compile
            |           createdFiles.lst
            |           inputFiles.lst
            |
            \---testCompile
                \---default-testCompile
                        inputFiles.lst
