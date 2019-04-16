---
ID: 300
post_title: >
  State-machines and Java Validation API.
  Good fit for business objects flows.
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=300
published: true
post_date: 2019-04-16 22:12:44
---
<strong>Java Validation API.  What is it?</strong>

The Java Validation API is a specification of Java EE (Jakarta EE) that makes it easy to validate objects and their fields.

It uses annotations to specify what must be validated and how. Once the validation happens, we will have available a list of errors that will give as all needed information about what has failed.

For example, given the class Item:

[java]

public class Item {

  @NotNull
  private Integer id;

  @NotEmpty
  private String name;

  @Min(1)
  private BigDecimal price;

  public Item(Integer id, String name, BigDecimal price) {
    this.id = id;
    this.name = name;
    this.price = price;
  }
}
[/java]

we are are validating that the id is not null, the attribute name can not be an empty String and that price must be bigger than one. Then, to test that it works, we just needs to run the following test:

[java]

class ValidationTest {

  private ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
  private Validator validator;

  @BeforeEach
  void setUp() {
    validator = factory.getValidator();
  }

  @Test
  void validateSingleItem() {

    Item item = new Item(1, &quot;MacbookPro&quot;, BigDecimal.ONE);
    Set&lt;ConstraintViolation&lt;Item&gt;&gt; violations = validator.validate(item);
    Assertions.assertTrue(violations.isEmpty());


    item = new Item(1, &quot;&quot;, BigDecimal.ZERO);
    violations = validator.validate(item);
    Assertions.assertTrue(violations.isEmpty());

  }
}

[/java]

<strong>State machine. What is it and why should you use it? </strong>

In our context, I will define a state machine as the representation of the sates where an object or flow can be and the transitions that allow to go from one state to another state. The referred object or flow can be in only and only one state at a time.

This modeling in our software context is useful to give structure and design to the different rules and conditions that normally any business logic have.

Usually, objects have states, and to have states often means to apply different validation rules per each different state.

<strong>Match with Validation API:</strong>

Is in this context where the validation API comes to place. Using a state machine, it is trivial to integrate this business validation into the state machine. The only thing you need to do, is to associate each state with one or more validation groups. Then, when the object enters an state, the state machine can apply the validation for the defined groups of the entering state.

Using this design, we achieve two goals:
<ul>
 	<li>We define and make it transparent which validation rules are applied each time in a semantic way, without any need to understand the validation logic itself.</li>
 	<li>Describing the states and transitions it makes really transparent how the object flow looks like</li>
</ul>
Let's see the most simple example, where we have some business object or pojos with a state. The state of the object can be represented using a StateMachine. In this example. the current state of the state machine is the object itself but in more complex scenarios, a state can represent the state and relations of several objects. To model the states of a given object, we are gone a code a TransitionBuilder class where we will describe transitions as a source node, an event triggering the transition and a traget node. The source and target nodes represents the start and end state of the transition.

[java]
 public class TransitionBuilder {
    private State source;
    private State target;
    private Object event;

    private TransitionBuilder() {
    }

    public TransitionBuilder fromState(State source) {
      this.source = source;
      return this;
    }

    public TransitionBuilder goToState(State target) {
      this.target = target;
      return this;
    }

    public TransitionBuilder onEvent(Object event) {
      this.event = event;
      return this;
    }

    public TransitionBuilder addAndBeginTransition() {
      Transition transition = new Transition(source, target, event);
      StateMachineBuilder.this.addTransition(transition);
      return new TransitionBuilder();
    }

    public StateMachine done() {
      Transition transition = new Transition(source, target, event);
      StateMachineBuilder.this.addTransition(transition);
      return StateMachineBuilder.this.done();
    }
  }
[/java]

Now we can model a simple object state machine. As an example, we are modeling a really simple order object. An order have a state INIT, (item)BOOKED, (item)DISPATCHED, ON_TRACK, DELIVERED.
Now, using the builder above, we just need to create our state model:

[java]
public StateMachine create() {

    InitState initState = new InitState();
    BookedState bookedState = new BookedState();
    DispatchedState dispatchedState = new DispatchedState();
    OnTrackState onTrackState = new OnTrackState();
    DeliveredState deliveredState = new DeliveredState();

    return new StateMachineBuilder()

        .beginTransition()

        .onEvent(Event.START_ORDER)
        .fromState(initState)
        .goToState(bookedState)

        .addAndBeginTransition()

        .onEvent(Event.DISPATCH)
        .fromState(bookedState)
        .goToState(dispatchedState)

        .addAndBeginTransition()

        .onEvent(Event.SEND)
        .fromState(dispatchedState)
        .goToState(onTrackState)

        .addAndBeginTransition()

        .onEvent(Event.DELIVER)
        .fromState(onTrackState)
        .goToState(deliveredState)

        .done();
[/java]

&nbsp;

It is possible now, using the Java Validation API to assign one or more validation groups to each state, and with a little bit of simple logic, we will trigger per each transition the validation with the groups of the target state.

The next code ilustrates the workflow:
[java]
@Test
void testStateMachine() {

StateMachine stateMachine = new OrderStateMachineFactory().create();
Order order = new Order();

Optional&lt;ConstraintViolationException&gt; r = stateMachine.trigger(Event.START_ORDER, order);

assertFalse(r.isEmpty());
System.out.println(&quot;1:&quot; + r.get().getMessage());

order.setId(&quot;OrderId&quot;);
order.setItemId(&quot;ItemId&quot;);
r = stateMachine.trigger(Event.START_ORDER, order);

assertTrue(r.isEmpty());
assertEquals(new BookedState().getName(), order.getState());

r = stateMachine.trigger(Event.DISPATCH, order);
assertFalse(r.isEmpty());
System.out.println(&quot;2:&quot; + r.get().getMessage());

order.setInvoiceRef(&quot;InvoiceRef&quot;);
order.setAddress(&quot;Major Str. PLZ 122 Berlin&quot;);

r = stateMachine.trigger(Event.DISPATCH, order);
assertTrue(r.isEmpty());
assertEquals(new DispatchedState().getName(), order.getState());

r = stateMachine.trigger(Event.SEND, order);
assertTrue(r.isEmpty());
assertEquals(new OnTrackState().getName(), order.getState());

r = stateMachine.trigger(Event.DELIVER, order);
assertTrue(r.isEmpty());
assertEquals(new DeliveredState().getName(), order.getState());
}
[/java]

The state machine itself is a simple class implementing a method <em>trigger</em> that given an event and object with a state (current state of the StateMachine) just look for the target event and triggers it.
The state object is just triggering the validation and updating the state of the object:

[java]
public class StateMachine {

  public List&lt;Transition&gt; transitions;

  public StateMachine(List&lt;Transition&gt; transitions) {
    this.transitions = new ArrayList&lt;&gt;(transitions);
  }

  public Optional&lt;ConstraintViolationException&gt; trigger(Object event, StateObject stateObject) {

    Object state = stateObject.getState();

    Optional&lt;ConstraintViolationException&gt; r = transitions
        .stream()
        .filter(t -&gt; t.getEvent().equals(event))
        .filter(t -&gt; t.getSource().getName().equals(stateObject.getState()))
        .findAny()
        .orElseThrow(() -&gt; new InvalidTransitionException(event, stateObject.getState()))
        .getTarget().onState(stateObject);

    //Simulates a roll-back in case of error
    r.ifPresent(ex -&gt; stateObject.setState(state));

    return r;
  }
}
[/java]
[java]
public Optional&lt;ConstraintViolationException&gt; onState(StateObject stateObject) {
    enterState((Order) stateObject);
    Set&lt;ConstraintViolation&lt;StateObject&gt;&gt; violations = validator.validate(stateObject, getValidationGroups());
    if (!violations.isEmpty()) {
      return Optional.of(new ConstraintViolationException(&quot;Violations on state &quot; + getName() + &quot;. &quot; + toString(violations), violations));
    }

    return Optional.empty();
}
[/java]
With the two commented advantages, it is also easy and almost error free to add new states and transitions.
You can find the code of this article on <a href="https://github.com/alacambra/blogs-posts-code/tree/master/simple-statemachine" rel="noopener" target="_blank">github</a>