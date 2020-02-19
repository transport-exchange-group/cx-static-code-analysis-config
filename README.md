# TEG Static Code Analysis Tools Configuration
Provides default configuration for Checkstyle and PMD at TEG.
Also contains TEG standart `.eiditorconfig` and `.gitignore` files, that you have to copy and use in your project

## Getting Started
To use it, configure your maven plugins like so:

### Checkstyle configuration
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.1.0</version>
    <dependencies>
        <dependency>
            <groupId>com.puppycrawl.tools</groupId>
            <artifactId>checkstyle</artifactId>
            <version>8.28</version>
        </dependency>
    </dependencies>
    <executions>
        <execution>
            <phase>validate</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <configLocation>https://raw.githubusercontent.com/transport-exchange-group/cx-static-code-analysis-config/master/cx-checkstyle.xml</configLocation>
        <consoleOutput>true</consoleOutput>
        <enableRulesSummary>false</enableRulesSummary>
        <violationSeverity>warning</violationSeverity>
    </configuration>
</plugin>
```

See the [maven-checkstyle-plugin docs](https://maven.apache.org/plugins/maven-checkstyle-plugin/check-mojo.html) 
for more information about what the configuration parameters mean.

The configuration of the checkstyle plugin you get from `cx-checkstyle.xml` tells it to 
optionally look for a file named `suppressions.xml` as per the
[SuppressionFilter docs](http://checkstyle.sourceforge.net/config_filters.html#SuppressionFilter). 
This means you can configure suppressions by providing such a file on your
project's classpath or in the current directory where you build it - note 
that for multi-module projects, it's probably a good idea to use something
like [this solution](http://stackoverflow.com/a/19690484/1659929) to share
the configuration among each sub-module.

### PMD configuration
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-pmd-plugin</artifactId>
    <version>3.12.0</version>
    <executions>
        <execution>
            <phase>validate</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <analysisCache>true</analysisCache>
        <linkXRef>false</linkXRef>
        <rulesets>
            <ruleset>https://raw.githubusercontent.com/transport-exchange-group/cx-static-code-analysis-config/master/cx-pmd-ruleset.xml</ruleset>
        </rulesets>
        <failOnViolation>true</failOnViolation>
        <printFailingErrors>true</printFailingErrors>
    </configuration>
</plugin>
```

See the [maven-pmd-plugin docs](https://maven.apache.org/plugins/maven-pmd-plugin/check-mojo.html) 
for more information about what the configuration parameters mean.

## Authors

* Vitaliy Evtushenko