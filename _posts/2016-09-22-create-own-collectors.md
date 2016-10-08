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

[java]&lt;/pre&gt;
&lt;pre&gt;public class MaxMinCollector2 implements Collector&lt;Integer, MaxMinContainer, MaxMinContainer&gt;{

    public void accumulate(MaxMinContainer container, Integer val){

        if(container.max == null){
            container.max = val;
        }else if(container.max &lt; val){
            container.max = val;
        }

        if(container.min == null){
            container.min = val;
        }else if(container.min &gt; val){
            container.min = val;
        }

    }

    public MaxMinContainer combine(MaxMinContainer a, MaxMinContainer b){
        if(a.max == null){
            b.getMax().ifPresent(v -&gt; a.max = v);
        }else {
            b.getMax().ifPresent(v -&gt; a.max = a.max &lt; v ? v : a.max);
        }

        if(a.min == null){
            b.getMin().ifPresent(v -&gt; a.min = v);
        }else {
            b.getMax().ifPresent(v -&gt; a.min = a.min &gt; v ? v : a.min);
        }

        return a;
    }

    @Override
    public Supplier&lt;MaxMinContainer&gt; supplier() {
        return MaxMinContainer::new;
    }

    @Override
    public BiConsumer&lt;MaxMinContainer, Integer&gt; accumulator() {
        return this::accumulate;
    }

    @Override
    public BinaryOperator&lt;MaxMinContainer&gt; combiner() {
        return this::combine;
    }

    @Override
    public Function&lt;MaxMinContainer, MaxMinContainer&gt; finisher() {
        return (a) -&gt; a;
    }

    @Override
    public Set&lt;Characteristics&gt; characteristics() {
        return new HashSet&lt;&gt;(Arrays.asList(Characteristics.IDENTITY_FINISH, Characteristics.UNORDERED));
    }
}&lt;/pre&gt;
&lt;pre&gt;[/java]

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