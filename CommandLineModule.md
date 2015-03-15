# Introduction #

PropertiesModule is great for automatically binding a large number of constants to annotations in Guice, but sometimes you also want to take properties from the command line. CommandLineModule is an _extension_ to PropertiesModule that allows you to use the command line to supply properties (and even override properties from the environment).

# How to Use #

Just create a CommandLineModule instance, passing the `args` array directly from your `main` method into its constructor, and wire it to GuiceBox, like this:
```
public static void main(String[] args)
{
    final GuiceBox guicebox = GuiceBox.init(new CommandLineModule(args));
}
```
Note that you don't need to wire PropertiesModule if you use CommandLineModule. The latter is an extension of the former, so PropertiesModule functionality is _included_ in CommandLineModule.

# Command Line Arguments #

Properties can then be supplied at the command line using the following syntax:
```
java MyMainClass -org.guicebox.Param1 base1 -my.boolean.prop -my.integer.prop 5
```
The properties generated from the command line above would be:
```
   @org.guicebox.Param1                               = base1
    my.boolean.prop                                   = true
    my.integer.prop                                   = 5
```

Note that **boolean** properties are assumed to be `true` if you don't supply a value after the `-propname` argument.