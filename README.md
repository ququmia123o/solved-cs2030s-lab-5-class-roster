Download Link: https://assignmentchef.com/product/solved-cs2030s-lab-5-class-roster
<br>
<table width="683">

 <tbody>

  <tr>

   <td colspan="3" width="683">Your task is to read in a roster of students, the modules they take, the assessments they have completed, and the grade for each assessment. Then, given a query consisting of a triplet: a student, a module, and an assessment, retrieve the corresponding grade.For instance, if the input is:

    <table width="609">

     <tbody>

      <tr>

       <td width="609">Steve CS1010 Lab3 ASteve CS1231 Test A+Bruce CS2030 Lab1 C</td>

      </tr>

     </tbody>

    </table>and the query is Steve CS1231 Test, the program should print A+.In our scenario, a roster has zero or more students; a student takes zero or more modules, a module has zero or more assessments, and each assessment has exactly one grade. Each of these entities can be uniquely identified by a string.This lab also involves using the HashMap class from Java Collections.<strong>Preamble</strong><strong>Map</strong>Map&lt;K,V&gt; is a generic interface from the Java Collection Framework, the implementation of which is useful for storing a collection of items and retrieving an item. It maintains a map (aka dictionary) between keys (of type K) and values (of type V). The two core methods are (i) put, which stores a (key, value) pair into the map, and (ii) get, which returns the value associated with a given key if the key is found or returns null otherwise.The following examples show how the Map&lt;K,V&gt; interface and its implementation HashMap&lt;K,V&gt; can be used.</td>

  </tr>

  <tr>

   <td width="37"> </td>

   <td width="609"><strong>jshell&gt; Map&lt;String,Integer&gt; map = new HashMap&lt;String,Integer&gt;();</strong> <strong>jshell&gt; map.put(“one”, 1);</strong> $.. ==&gt; null</td>

   <td width="37"> </td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; map.put(“two”, 2);</strong>$.. ==&gt; null<strong>jshell&gt; map.put(“three”, 3);</strong>$.. ==&gt; null<strong>jshell&gt; map.get(“one”)</strong>$.. ==&gt; 1<strong>jshell&gt; map.get(“four”)</strong>$.. ==&gt; null<strong>jshell&gt; map.entrySet()</strong>$.. ==&gt; [one=1, two=2, three=3]<strong>jshell&gt; for (Map.Entry&lt;String,Integer&gt; e: map.entrySet()) {</strong> <strong>   …&gt;  System.out.println(e.getKey() + “:” + e.getValue());</strong><strong>   …&gt; }</strong> one:1 two:2 three:3</td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; new Assessment(“Lab1”, “B”)</strong>$.. ==&gt; {Lab1: B}<strong>jshell&gt; new Assessment(“Lab1”, “B”).getGrade()</strong>$.. ==&gt; “B”<strong>jshell&gt; new Assessment(“Lab1”, “B”).getKey()</strong>$.. ==&gt; “Lab1” <strong>jshell&gt; /exit</strong></td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; new Module(“CS2040”)</strong>$.. ==&gt; CS2040: {}<strong>jshell&gt; new Module(“CS2040”).getKey();</strong>$.. ==&gt; “CS2040”<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))</strong>$.. ==&gt; CS2040: {{Lab1: B}}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).put(new Assessment(“Lab2”,”A</strong>$.. ==&gt; CS2040: {{Lab1: B}, {Lab2: A+}}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).put(new Assessment(“Lab2”,”A</strong>$.. ==&gt; {Lab1: B}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).put(new Assessment(“Lab2”,”A</strong>$.. ==&gt; {Lab2: A+}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).put(new Assessment(“Lab2”,”A</strong>$.. ==&gt; null <strong>jshell&gt; /exit</strong></td>

  </tr>

 </tbody>

</table>

<h2>Level 1</h2>

<h2>Assessment class and Keyable interface</h2>

We shall start by writing the Assessment class that implements the following Keyable interface.

interface Keyable {     String getKey();

}

Include a getGrade method that returns the grade of an assessment.

Check the format correctness of the output by running the following on the command line:

$ javac -Xlint:rawtypes *.java

$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test1.jsh

Check your styling by issuing the following

$ checkstyle *.java

<strong>Level 2</strong>

<h2>Module class</h2>

Write the Module class to store (via the put method) the assessments of a module in a map for easy retrieval as part of answering queries. A module can have zero or more assessments, with each assessment having a title as a key — a unique identifier.

Check the format correctness of the output by running the following on the command line:

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”)</strong>$.. ==&gt; {Lab1: B}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()</strong>$.. ==&gt; “B”<strong>jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))</strong>$.. ==&gt; Tony: {CS2040: {{Lab1: B}}}<strong>jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get</strong>$.. ==&gt; CS2040: {{Lab1: B}}<strong>jshell&gt; Student natasha = new Student(“Natasha”);</strong><strong>jshell&gt; natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))</strong>$.. ==&gt; Natasha: {CS2040: {{Lab1: B}}}<strong>jshell&gt; natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessmen</strong>$.. ==&gt; Natasha: {CS2030: {{Lab2: C}, {PE: A+}}, CS2040: {{Lab1: B}}}<strong>jshell&gt; Student tony = new Student(“Tony”);</strong><strong>jshell&gt; tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}}<strong>jshell&gt; tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Lab1: F}, {Test: B}}} <strong>jshell&gt; /exit</strong></td>

  </tr>

 </tbody>

</table>

<table width="569">

 <tbody>

  <tr>

   <td width="569">class KeyableMap&lt;V extends Keyable&gt; implements Keyable {… }</td>

  </tr>

 </tbody>

</table>

$ javac -Xlint:rawtypes *.java

$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test2.jsh

Check your styling by issuing the following

$ checkstyle *.java

<strong>Level 3</strong>

<h2>Student class</h2>

Write a Student class that stores the modules he/she reads in a map via the put method. A student can read zero or more modules, with each module having a unique module code as its key.

Check the format correctness of the output by running the following on the command line:

$ javac -Xlint:rawtypes *.java

$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test3.jsh

Check your styling by issuing the following

$ checkstyle *.java

<strong>Level 4</strong>

<h3>Generic class KeyableMap</h3>

You will notice that the implementations of the Student and Module classes are very similar. Hence, by applying the <em>abstraction principle</em>, write a generic class KeyableMap to reduce the duplication.

<em>Hint:</em> KeyableMap&lt;V&gt; is a generic class that wraps around a String key (i.e. implements Keyable) and a

Map&lt;String,V&gt;. KeyableMap models an entity that contains a map, but is also itself contained in another container (e.g. a student contains a map of modules but could be contained in a roster). The parameter type V is the type of the value of items stored in the map; V must be a subtype of Keyable.

The class KeyableMap is a mutable class — we made this decision since the Map implementation in Java Collection Framework is mutable. KeyableMap provides two core methods:

get(String key) which returns the item with the given key; put(V item) which adds the key-value pair (item.getKey(),item) into the map. The put method returns a

KeyableMap. To avoid type mismatch when chaining put method calls together, each sub-class of KeyableMap should override the put method from KeyableMap and change the return type to the corresponding sub-classes. E.g., Student should override put to return a Student through a type-cast (which is guaranteed to be safe). Moreover, how do we restrict the classes bound to type V to be able to invoke the getKey method? The trick is to define the type parameter of Keyable as follows:

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”)</strong>$.. ==&gt; {Lab1: B}<strong>jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()</strong>$.. ==&gt; “B”<strong>jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))</strong>$.. ==&gt; Tony: {CS2040: {{Lab1: B}}}<strong>jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get</strong>$.. ==&gt; CS2040: {{Lab1: B}}<strong>jshell&gt; Student natasha = new Student(“Natasha”);</strong><strong>jshell&gt; natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))</strong>$.. ==&gt; Natasha: {CS2040: {{Lab1: B}}}<strong>jshell&gt; natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessmen</strong>$.. ==&gt; Natasha: {CS2030: {{Lab2: C}, {PE: A+}}, CS2040: {{Lab1: B}}}<strong>jshell&gt; Student tony = new Student(“Tony”);</strong><strong>jshell&gt; tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}}<strong>jshell&gt; tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Lab1: F}, {Test: B}}}<strong>jshell&gt; new Module(“CS1231”).put(new Assessment(“Test”, “A-“)) instanceof KeyableMap</strong>$.. ==&gt; true<strong>jshell&gt; new Student(“Tony”).put(new Module(“CS1231”)) instanceof KeyableMap</strong>$.. ==&gt; true <strong>jshell&gt; /exit</strong></td>

  </tr>

 </tbody>

</table>

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; Student natasha = new Student(“Natasha”);</strong><strong>jshell&gt; natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))</strong>$.. ==&gt; Natasha: {CS2040: {{Lab1: B}}}<strong>jshell&gt; natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessmen</strong>$.. ==&gt; Natasha: {CS2030: {{Lab2: C}, {PE: A+}}, CS2040: {{Lab1: B}}}<strong>jshell&gt; Student tony = new Student(“Tony”);</strong><strong>jshell&gt; tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}}<strong>jshell&gt; tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment</strong>$.. ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Lab1: F}, {Test: B}}} <strong>jshell&gt; Roster roster = new Roster(“AY1920”).put(natasha).put(tony)</strong><strong>jshell&gt; roster</strong> roster ==&gt; AY1920: {Natasha: {CS2030: {{Lab2: C}, {PE: A+}}, CS2040: {{Lab1: B}}}, Tony: <strong>jshell&gt; roster.get(“Tony”).get(“CS1231”).get(“Test”).getGrade()</strong>$.. ==&gt; “A-”<strong>jshell&gt; roster.get(“Natasha”).get(“CS2040”).get(“Lab1”).getGrade()</strong>$.. ==&gt; “B”<strong>jshell&gt; roster.get(“Tony”).get(“CS1231”).get(“Exam”)</strong>$.. ==&gt; null<strong>jshell&gt; roster.get(“Steve”)</strong>$.. ==&gt; null<strong>jshell&gt; roster.getGrade(“Tony”,”CS1231″,”Test”)</strong>$.. ==&gt; “A-”<strong>jshell&gt; roster.getGrade(“Natasha”,”CS2040″,”Lab1″)</strong> $.. ==&gt; “B”</td>

  </tr>

 </tbody>

</table>

Check the format correctness of the output by running the following on the command line:

$ javac -Xlint:rawtypes *.java

$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test4.jsh

Check your styling by issuing the following

$ checkstyle *.java

<strong>Level 5</strong>

<h2>Roster class</h2>

Now you are ready to create a roster. Define a Roster class that stores the students in a map via the put method. A roster can have zero or more students, with each student having a unique id as its key. Once again, notice the similarities between Roster, Student and Module.

Define a method called getGrade in Roster to answer the query from the user. The method takes in three String parameters, corresponds to the student id, the module code, and the assessment title, and returns the corresponding grade.

In cases where there are no such student, or the student does not read the given module, or the module does not have the corresponding assessment, then output No such record followed by details of the query.

<table width="609">

 <tbody>

  <tr>

   <td width="609"><strong>jshell&gt; roster.getGrade(“Tony”,”CS1231″,”Exam”);</strong> $.. ==&gt; “No such record: Tony CS1231 Exam” <strong>jshell&gt; roster.getGrade(“Steve”,”CS1010″,”Lab1″);</strong> $.. ==&gt; “No such record: Steve CS1010 Lab1” <strong>jshell&gt; new Roster(“AY1920”) instanceof Keyable</strong>$.. ==&gt; true<strong>jshell&gt; new Roster(“AY1920”).put(new Student(“Tony”)) instanceof Keyable</strong>$.. ==&gt; true <strong>jshell&gt; /exit</strong></td>

  </tr>

 </tbody>

</table>

Check the format correctness of the output by running the following on the command line:

$ javac -Xlint:rawtypes *.java

$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test5.jsh

Check your styling by issuing the following

$ checkstyle *.java

<strong>Level 6</strong>

<h3>The Main class</h3>

Now use the classes that you have built and write a Main class to solve the following:

Read the following from the standard input:

The first token read is an integer <em>N</em>, indicating the number of records to be read.

The subsequent inputs consist of <em>N</em> records, each record consists of four words, separated by one or more spaces. The four words correspond to the student id, the module code, the assessment title, and the grade, respectively.

The subsequent inputs consist of zero or more queries. Each query consists of three words, separated by one or more spaces. The three words correspond to the student id, the module code, and the assessment title.

For each query, if a match in the input is found, print the corresponding grade to the standard output. Otherwise, print “No Such Record:” followed by the three words given in the query, separated by exactly one space.

See sample input and output below. Inputs are underlined.

$ java Main

<u>12</u>

<u>Jack   CS2040 Lab4    B</u>

<u>Jack   CS2040 Lab6    C</u>

<u>Jane   CS1010 Lab1    A</u>

<u>Jane   CS2030 Lab1    A+</u>

<u>Janice CS2040 Lab1    A+</u>

<u>Janice CS2040 Lab4    A+</u>

<u>Jim    CS1010 Lab9    A+</u>

<u>Jim    CS2010 Lab1    C</u>

<u>Jim    CS2010 Lab2    B</u>

<u>Jim    CS2010 Lab8    A+</u>

<u>Joel   CS2030 Lab3    C</u>

<u>Joel   CS2030 Midterm A</u>

<u>Jack   CS2040 Lab4</u>

<u>Jack   CS2040 Lab6</u>

<u>Janice CS2040 Lab1</u>

<u>Janice CS2040 Lab4</u>

<u>Joel   CS2030 Midterm</u>

<u>Jason  CS1010 Lab1</u>

<u>Jack   CS2040 Lab5</u>

<u>Joel   CS2040 Lab3</u>

B

C

A


A


A

No such record: Jason CS1010 Lab1

No such record: Jack CS2040 Lab5

No such record: Joel CS2040 Lab3

Check the format correctness of the output by running the following on the command line:




<table width="683">

 <tbody>

  <tr>

   <td rowspan="2" width="37"> </td>

   <td width="609">$ javac -Xlint:rawtypes *.java$ java Main &lt; test6.in</td>

   <td rowspan="2" width="37"> </td>

  </tr>

  <tr>

   <td width="609">Check your styling by issuing the following

    <table width="609">

     <tbody>

      <tr>

       <td width="609">$ checkstyle *.java</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>