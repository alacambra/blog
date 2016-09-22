---
ID: 58
post_title: Create own collectors
author: alacambra
post_date: 2016-09-22 19:09:49
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/22/create-own-collectors/
published: true
---
Sometimes it is useful to be able perform several actions extracting several actions with a stream pass. It can be achieved building our own collector. For example, suppose we need to get the maximal and minimal values of a series. So can we achieve it using collectors.

[java]
package de.lacambra.utils.collectors;

import java.util.Optional;

public class MaxMinCollector{

    Integer max;
    Integer min;

    public void accumulate(Integer val){

        if(max == null){
            max = val;
        }else if(max &lt; val){ max = val; } if(min == null){ min = val; }else if(min &gt; val){
            min = val;
        }

    }

    public void combine(MaxMinCollector other){
        if(max == null){
            other.getMax().ifPresent(v -&gt; max = v);
        }else {
            other.getMax().ifPresent(v -&gt; max = max &lt; v ? v : max); } if(min == null){ other.getMin().ifPresent(v -&gt; min = v);
        }else {
            other.getMax().ifPresent(v -&gt; min = min &gt; v ? v : min);
        }
    }

    public Optional&lt;Integer&gt; getMax() {
        return Optional.ofNullable(max);
    }

    public Optional&lt;Integer&gt; getMin() {
        return Optional.ofNullable(min);
    }
}
[/java]

and its corresponding test:

[java]
package de.lacambra.utils.collectors;

import org.junit.Before;
import org.junit.Test;

import java.util.stream.IntStream;

import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertThat;

public class MaxMinCollectorTest {

    MaxMinCollector cut;

    @Before
    public void setUp() throws Exception {
        cut = new MaxMinCollector();
    }

    @Test
    public void testMaxMinSerie() {

        MaxMinCollector result = IntStream.of(1, 2, 3, 4, 5, 6)
                .collect(MaxMinCollector::new, MaxMinCollector::accumulate, MaxMinCollector::combine);

        assertThat(result.getMax().get(), is(6));
        assertThat(result.getMin().get(), is(1));

        result = IntStream.of(1000, 2, 3342, 421, 523, 6)
                .collect(MaxMinCollector::new, MaxMinCollector::accumulate, MaxMinCollector::combine);

        assertThat(result.getMax().get(), is(3342));
        assertThat(result.getMin().get(), is(2));
    }

    @Test
    public void emptySerie(){
        MaxMinCollector result = IntStream.of()
                .collect(MaxMinCollector::new, MaxMinCollector::accumulate, MaxMinCollector::combine);

        assertThat(result.getMax().isPresent(), is(false));
        assertThat(result.getMin().isPresent(), is(false));
    }

    @Test
    public void oneValueSerie(){
        MaxMinCollector result = IntStream.of(34)
                .collect(MaxMinCollector::new, MaxMinCollector::accumulate, MaxMinCollector::combine);

        assertThat(result.getMax().get(), is(34));
        assertThat(result.getMin().get(), is(34));
    }
}
[/java]