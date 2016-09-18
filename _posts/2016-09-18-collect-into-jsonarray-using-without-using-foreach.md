---
ID: 35
post_title: >
  Collect into Jsonp JsonArray using
  without using foreach
author: alacambra
post_date: 2016-09-18 15:27:04
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/collect-into-jsonarray-using-without-using-foreach/
published: true
---
Each collector has three parts:
<ul>
 	<li><strong>A supplier</strong>: provides with instances of the accumulator.</li>
 	<li><strong>An accumulator</strong>: accumulates the objects being collected. Several instances of accumulator can be used.</li>
 	<li><strong>A combiner</strong>: combines all the accumulator putting all collected objects together.</li>
</ul>
For the JsonArray the combiner, accumulator  and combiener are respectively:
<pre>public static JsonArrayBuilder createArrayBuilder()
JsonArrayBuilder add(JsonValue value)
JsonArrayBuilder add(JsonArrayBuilder builder)</pre>

[java]

    public JsonArray getArray(Jsonable[] objects) {
        return Stream.of(objects).map(Jsonable::toJson)
                .collect(
                        Json::createArrayBuilder,
                        JsonArrayBuilder::add,
                        JsonArrayBuilder::add
                ).build();

    }

    public static class Jsonable {

        public JsonObject toJson() {
            return Json.createObjectBuilder().add(&quot;someId&quot;, LocalTime.now().toString()).build();
        }
    }

[/java]