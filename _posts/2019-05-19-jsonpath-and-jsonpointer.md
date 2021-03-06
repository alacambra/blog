---
ID: 338
post_title: >
  The JsonPointer. Simplifying the way to
  work with JSON
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=338
published: true
post_date: 2019-05-19 15:25:15
---
Since Java API for JSON Processing  (JSR 374) version 1.1, it is possible to use JosnPointer.

JsonPointer is a specification of <a href="https://tools.ietf.org/html/rfc6901">rfc6901</a> and as we can read on it, <em>JSON Pointer defines a string syntax for identifying a specific value
within a JavaScript Object Notation (JSON) document.</em>
In other words, it is possible now to evaluate and change values from our JsonObjects using a pointer string instead to go through the whole chain of calls and recreating an object builder at the end.

So instead of that:

[java]
    String nameWithObject = jsonObject.getJsonArray(&quot;user_mentions&quot;).getJsonObject(0).getString(&quot;name&quot;);
[/java]

we can do that:

[java]
    String nameWithPointer = ((JsonString)Json.createPointer(&quot;/user_mentions/0/name&quot;).getValue(jsonObject)).getString();
[/java]

We can easily see, that the use of pointers make easier to know which element we are fetching and more intuitive to write.
However, since the pointer is returning a JsonValue, we need to use a cast to be able to fetch the final value.

Why JsonPointer is not providing methods to directly get java types like JsonObject is doing, is something I do not really know.

<strong>So, what can we do with the JSON pointer?</strong>
We can not only get values from a JsonStructure using pointer notation but also modify the object without the need to reconvert it into its builder equivalent. So specifically we can:
<ul>
 	<li>add a value to a JsonStructure</li>
 	<li>check if a value is contained into a JsonStructure</li>
 	<li>remove a value from a jsonStructure</li>
 	<li>replace a value into a JsonStructre</li>
</ul>
Let's see some examples. For the examples, I will use the json object shown at the end of thas a basis:
<ul>
 	<li><strong>Get a simple value from an object.</strong>

[java]
JsonNumber id = ((JsonNumber) Json.createPointer(&quot;/id&quot;).getValue(example));
[/java]

</li>
 	<li><strong>get an object from an object.</strong>

[java]
    JsonObject user = Json.createPointer(&quot;/user&quot;).getValue(example).asJsonObject();
[/java]

</li>
 	<li><strong>get an array from an object</strong>

[java]
    JsonArray userMentions = Json.createPointer(&quot;/user_mentions&quot;).getValue(example).asJsonArray();
[/java]

</li>
 	<li><strong>get an element from an array</strong>

[java]
    JsonObject mention = Json.createPointer(&quot;/user_mentions/0&quot;).getValue(example).asJsonObject();
    String mentionName = ((JsonString) Json.createPointer(&quot;/user_mentions/0/name&quot;).getValue(example)).getString();
    int mentionIndex0 = ((JsonNumber) Json.createPointer(&quot;/user_mentions/0/indices/1&quot;).getValue(example)).intValue();
[/java]

</li>
 	<li><strong>check if an object contains an element</strong>

[java]
    Assertions.assertTrue(Json.createPointer(&quot;/id&quot;).containsValue(example));
    Assertions.assertTrue(Json.createPointer(&quot;/user_mentions/0/indices/0&quot;).containsValue(example));
    Assertions.assertTrue(Json.createPointer(&quot;/user_mentions/0/indices/1&quot;).containsValue(example));
    Assertions.assertFalse(Json.createPointer(&quot;/user_mentions/0/indices/2&quot;).containsValue(example));
[/java]

</li>
 	<li><strong>Add a simple value</strong>

[java]
       JsonObject extendedExample = Json.createPointer(&quot;/timestamp&quot;).add(example, Json.createValue(System.currentTimeMillis()));
       Assertions.assertTrue(Json.createPointer(&quot;/timestamp&quot;).containsValue(extendedExample));
[/java]

</li>
 	<li><strong>Add an element to a JsonArray. The pointer must point to the last_element + 1 index. Empty elements would produce an error.</strong>

[java]
    extendedExample = Json.createPointer(&quot;/user_mentions/0/indices/2&quot;).add(extendedExample, Json.createValue(30));
    Assertions.assertEquals(30, ((JsonNumber) Json.createPointer(&quot;/user_mentions/0/indices/2&quot;).getValue(extendedExample)).intValue());
[/java]

</li>
 	<li><strong>Replace elements</strong>

[java]
    example = Json.createPointer(&quot;/id&quot;).replace(example, Json.createValue(2));
    Assertions.assertEquals(2, example.getInt(&quot;id&quot;));

    example = Json.createPointer(&quot;/user_mentions/0/indices/1&quot;).replace(example, Json.createValue(9999));
    Assertions.assertEquals(9999, ((JsonNumber) Json.createPointer(&quot;/user_mentions/0/indices/1&quot;).getValue(example)).intValue());
[/java]

</li>
 	<li><strong>Remove elements</strong>

[java]
    example = Json.createPointer(&quot;/id&quot;).remove(example);
    Assertions.assertFalse(example.containsKey(&quot;id&quot;));
[/java]

Json used for the examples:</li>
</ul>

[javascript]

{
&quot;id&quot;: 1,
&quot;user&quot;:
{
&quot;name&quot;: &quot;some-name&quot;,
&quot;lastname&quot;: &quot;some-lastname&quot;
},
&quot;user_mentions&quot;: [
{
&quot;name&quot;: &quot;Twitter API&quot;,
&quot;indices&quot;: [
4,
15
],
&quot;screen_name&quot;: &quot;twitterapi&quot;,
&quot;id&quot;: 6253282,
&quot;id_str&quot;: &quot;6253282&quot;
}
]
}

[/javascript]

In another article I will speak about the JsonPatch, <a href="https://tools.ietf.org/html/rfc6902">rfc</a> defined as
<pre>JSON Patch defines a JSON document structure for expressing a sequence of operations to apply to a JavaScript Object Notation (JSON) document; it is suitable for use with the HTTP PATCH method. The "application/json-patch+json" media type is used to identify such patch documents.</pre>
Sourcecode on <a href="https://github.com/alacambra/blogs-posts-code/blob/master/json-patch-and-pointer/src/test/java/json_patch_and_pointer/PatchAndPointer.java">github</a>