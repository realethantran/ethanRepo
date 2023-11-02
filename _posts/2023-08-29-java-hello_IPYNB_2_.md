---
toc: True
comments: True
layout: post
title: Java Hello (Classes)
description: None
type: hacks
courses: {'csa': {'week': 1}}
---

The beginning of the code defines the SuperHero class with private instance variables. The SuperHero class has a default constructor that initializes the instance variables to empty values.

<html>
<img src="https://github.com/realethantran/ethan_student/assets/109186517/936e9858-7a69-495b-ac6d-9b1a04ee6e36" height="550px">
</html>


```java
// class definition for SuperHero
public class SuperHero {
    // private instance variables
    private String Name;
    private String Affiliation;
    private String SecretIdentity;
    private String Powers;

    // constructor w/o parameters
    public SuperHero() {
        Name = "";
        Affiliation = "";
        SecretIdentity = "";
        Powers = "";
    }

    // parameterized constructor
    public SuperHero(String name, String affiliation, String secretIdentity, String powers) {
        this.Name = name;
        this.Affiliation = affiliation;
        this.SecretIdentity = secretIdentity;
        this.Powers = powers;
    }

    // setters to set the values of instance variables
    public void setName(String name) {
        Name = name;
    }

    public void setAffiliation(String affiliation) {
        Affiliation = affiliation;
    }

    public void setSecretIdentity(String secretIdentity) {
        SecretIdentity = secretIdentity;
    }

    public void setPowers(String powers) {
        Powers = powers;
    }

    // getters to get the values of instance variables
    public String getName() {
        return Name;
    }

    public String getAffiliation() {
        return Affiliation;
    }

    public String getSecretIdentity() {
        return SecretIdentity;
    }

    public String getPowers() {
        return Powers;
    }

    public static void main(String[] args) {
        // create an instance using the default constructor
        SuperHero batman = new SuperHero();

        // set the attributes of the superhero object
        batman.setName("Batman");
        batman.setAffiliation("Justice League");
        batman.setSecretIdentity("Bruce Wayne");
        batman.setPowers("None");

        // create an instance using the parameterized constructor
        SuperHero ultimate_spiderman = new SuperHero(
            "Spiderman",
            "Champions",
            "Miles Morales",
            "Super strength, super speed, agility, cling to solid surfaces, invisibility, and venom strike."
        );
        System.out.println("Details of Batman:");
        System.out.println("Name: " + batman.getName());
        System.out.println("Affiliation: " + batman.getAffiliation());
        System.out.println("Secret Identity: " + batman.getSecretIdentity());
        System.out.println("Powers: " + batman.getPowers());
    }
}
SuperHero.main(null);

// using getters I can retrieve the values of instance variables. For example, here I am retrieving the values of the attributes for the Batman instance.
```

    Details of Batman:
    Name: Batman
    Affiliation: Justice League
    Secret Identity: Bruce Wayne
    Powers: None



```java
public class City {
    String name;
    String state;
    String motto;

    public City(String name, String state, String motto) {
        this.name = name;
        this.state = state;
        this.motto = motto;
    }

    public static void main(String[] args) {
        City sanDiego = new City("San Diego", "California", "Semper Vigilans");
        System.out.println("City Name: " + sanDiego.name);
        System.out.println("State: " + sanDiego.state);
        System.out.println("Motto: " + sanDiego.motto);

        City tallahassee = new City("Tallahassee", "Florida", "Where There Are Hills");
        System.out.println("City Name: " + tallahassee.name);
        System.out.println("State: " + tallahassee.state);
        System.out.println("Motto: " + tallahassee.motto);
    }
}
City.main(null);

```

    City Name: San Diego
    State: California
    Motto: Semper Vigilans
    City Name: Tallahassee
    State: Florida
    Motto: Where There Are Hills

