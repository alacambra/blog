---
ID: 35
post_title: >
  Collect into JsonArray using without
  using foreach
author: alacambra
post_date: 2016-09-18 15:27:04
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/collect-into-jsonarray-using-without-using-foreach/
published: true
---

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