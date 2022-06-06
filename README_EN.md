[release-img]: https://img.shields.io/github/release/docer-savior/getter-setter-postfix-idea-plugin.svg
[latest-release]: https://github.com/docer-savior/getter-setter-postfix-idea-plugin/releases/latest
[plugin-img]: https://img.shields.io/badge/plugin-19320-orange.svg
[plugin]: https://plugins.jetbrains.com/plugin/19320
[jet-img]: https://img.shields.io/badge/plugin-Install%20Plugin-4597ff.svg
[jet]: http://localhost:63342/api/installPlugin?action=install&pluginId=gudqs7.github.io.getter-setter-postfix

[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)
[![license](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![GitHub release][release-img]][latest-release] [![Jetbrains Plugins][plugin-img]][plugin]
[![Version](http://phpstorm.espend.de/badge/19320/version)][plugin]  
[![Downloads](http://phpstorm.espend.de/badge/19320/downloads)][plugin]
[![Install Plugins][jet-img]][jet]

---
[Chinese 🇨🇳](./README.md)

# What does GenerateAllSetter Postfix Completion do?

- is an IDEA plugin that supports Java only.
- Referring to the GenerateAllSetter plugin, as a supplement, several Postfix syntaxes have been added, and the functions are basically the same as GenerateAllSetter.
- Generate all setters via `.allset` after pojo variables
- generate all setters via `.allsetn` after pojo variables (but no defaults)
- Generate all getters via `.allget` after pojo variables
- Generate all setter call chains via `.allbuilder` after using @lombok.Builder's pojo variable

# Why is this project useful?

- One more choice, and I think Postfix is more convenient and helps to further improve efficiency.
- Provide you with a Postfix plug-in development template, I hope you will develop more plug-ins to improve efficiency.

# How do I get started?

## 1. Install the plugin
### zip package installation
Download the zip package from the latest [Release][latest-release] page, then open IDEA, go to Settings --> Plugins --> Pinion --> Install Plugin from Disk
![zip](parts/imgs/install-plugin-from-disk.png)

### Marketplace Installation
Open IDEA, go to Settings --> Plugins, select Marketplace, enter GenerateAllSetter Postfix Completion and click Install
![Marketplace](parts/imgs/install-from-marketplace.png)


## 2. Open the sample project provided by me
Example project address: [docer-savior-plugin-usage-examples](https://github.com/docer-savior/docer-savior-plugin-usage-examples)

or
```shell
git clone https://github.com/docer-savior/docer-savior-plugin-usage-examples
````
After downloading, find the `cn.gudqs.example.genset.GenerateSetterAndGetterUsage` file

## 3. Plugin usage

The base class used by the demo
````java

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
class Foo {

    private Integer testInt;

    private Long testLong;

    private Float testFloat;

    private Double testDouble;

    private Boolean testBoolean;

}
````

### generate set
````java
public void usage01() {
    // Usage 1, generate all set methods, with default values, via postfix
    Foo foo = new Foo();
    // uncomment below, cursor is behind allset, press Tab
// foo.allset
    // The following result can be obtained, and foo.allset will disappear automatically
    foo.setTestInt(0);
    foo.setTestLong(0L);
    foo.setTestFloat(0f);
    foo.setTestDouble(0D);
    foo.setTestBoolean(false);
}
````

### generate get
````java
public void usage03() {
    // Usage 3, generate all get methods, via postfix
    Foo foo = new Foo();
    // Uncomment below, cursor is behind allget, press Tab
// foo.allget
    // The following result can be obtained, and foo.allget will disappear automatically
    Integer testInt = foo.getTestInt();
    Long testLong = foo.getTestLong();
    Float testFloat = foo.getTestFloat();
    Double testDouble = foo.getTestDouble();
    Boolean testBoolean = foo.getTestBoolean();
}
````


## Lombok's @Builder quickly generates the call chain of all assignment methods

````java
public void usage04() {
    // Usage 4, generate all set methods, via builder, via postfix
    // uncomment below, cursor is behind allbuilder, press Tab
// Foo.builder().allbuilder
    // You can get the following result
    Foo foo = Foo.builder()
            .testInt(0)
            .testLong(0L)
            .testFloat(0f)
            .testDouble(0D)
            .testBoolean(false)
            .build();
}
````

## Generate all set methods according to a b.setXxx(a.getXxx()) method code with source object (a)/target object (b) to quickly implement object conversion

````java
public void usage05() {
    // Usage 5, assign the data of src to dest, which is often used to convert two different classes directly (the field names need to be the same), through postfix
    Foo src = new Foo();
    Foo dest = new Foo();
    // Uncomment below, cursor is after convert, press Tab
// dest.setTestInt(src.getTestInt());.convert
    // You can get the following result
    dest.setTestInt(src.getTestInt());
    dest.setTestLong(src.getTestLong());
    dest.setTestFloat(src.getTestFloat());
    dest.setTestDouble(src.getTestDouble());
    dest.setTestBoolean(src.getTestBoolean());
}
````


# Where can I get more help if needed?

## Get help by submitting an issue
[Click to visit Github Issue](https://github.com/docer-savior/getter-setter-postfix-idea-plugin/issues)
> Everyone is welcome to ask questions, and everyone is welcome to improve it together!

**In addition, I have connected to the error handling component of IDEA, so when I find an error message from the plugin, follow the IDEA prompt to view the error information and report it to me with one click (that is, an issue is automatically generated)**

## See the wiki for more instructions

- [Getting Started Tutorial](https://github.com/docer-savior/getter-setter-postfix-idea-plugin/wiki/Getting-Started)

## Contribution Guidelines
[Contribution Guidelines](CONTRIBUTING_EN.md)

# Acknowledgments

- [Github intellij-generateAllSetMethod](https://github.com/gejun123456/intellij-generateAllSetMethod)
- [Github genSets](https://github.com/yoke233/genSets)