# jObjectFormatter - A toString Builder for Java

![Build Status](https://travis-ci.org/dtanzer/jobjectformatter.svg?branch=master)

jObjectFormatter is a library for implementing toString at runtime. It is easy to use, yet fully configurable and very
flexible. You can decide which fields to include in toString using Java annotations - And you can configure a different
behavior for transitive objects.

Stay in touch and get news about jObjectFormatter: Follow [David Tanzer (@dtanzer)](https://twitter.com/dtanzer) on Twitter.  
If you tweet about jObjectFormatter, please use the hash tag [#jObjectFormatter](https://twitter.com/search?f=tweets&q=%23jObjectFormatter).

* [Getting Started](#GettingStarted)
* [Why jObjectFormatter](#WhyJObjectFormatter)
* [Configuring jObjectFormatter](#ConfiguringJObjectFormatter)
* [Formatting Options (Annotations)](#FormattingOptions)
* [Transitive Objects](#TransitiveObjects)
* [Contributing](#Contributing)
* [License](#License)

## <a name="GettingStarted"> Getting Started

You really only need to do two things to get started: Add jObjectFormatter to your project, and then implement your 
```toString()``` methods like this:

    @Override
    public void toString() {
        return ObjectFormatter.format(this);
    }

### Add jObjectFormatter to Your Project

jObjectFormatter is available on Maven Central. So if you are using a build tool that supports maven dependencies and
if you have already configured the central repository correctly, you only have to add the dependency to your project:

**Gradle**

    compile 'net.davidtanzer:jobjectformatter:0.1.0'

**Maven**

    <dependency>
      <groupId>net.davidtanzer</groupId>
      <artifactId>jobjectformatter</artifactId>
      <version>0.1.0</version>
    </dependency>

### Implement toString to Use jObjectFormatter

Say you have a class ```Person``` and a class ```Address```, where a person has an address. You just have to implement
toString to use jObjectFormatter, which will take care of the rest.

    private static class Person {
        private String firstName;
        private String lastName;
        private Address address;

        public Person(final String firstName, final String lastName, final Address address) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.address = address;
        }

        @Override
        public String toString() {
            return ObjectFormatter.format(this);
        }
    }

    private static class Address {
        private String street;
        private String streetNo;

        public Address(final String street, final String streetNo) {
            this.street = street;
            this.streetNo = streetNo;
        }

        @Override
        public String toString() {
            return ObjectFormatter.format(this);
        }
    }

In it's default configuration, jObjectFormatter will use a very simple toString style. Let's try to print a person and
an address:

    Address address = new Address("Evergreen Terrace", "12b");
    Person person = new Person("Jane", "Doe", address);

The output of your toString from above will look like this:

    person.toString() -> { firstName=Jane, lastName=Doe, address=[not null] }
    address.toString() -> { street=Evergreen Terrace, streetNo=12b }

As you can see, jObjectFormatter does not transitively print objects in it's default configuration. Also, the string
formatter from the default configuration does not print the class name or group values.

## <a name="WhyJObjectFormatter"> Why jObjectFormatter

TBD

## <a name="ConfiguringJObjectFormatter"> Configuring jObjectFormatter

TBD

## <a name="FormattingOptions"> Formatting Options (Annotations)

TBD

## <a name="TransitiveObjects"> Transitive Objects

TBD

## <a name="Contributing"> Contributing

TBD

## <a name="License"> License

    Copyright 2015 David Tanzer (business@davidtanzer.net / @dtanzer)

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
