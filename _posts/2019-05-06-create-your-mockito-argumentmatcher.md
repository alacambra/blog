---
ID: 332
post_title: create your mockito.ArgumentMatcher
author: Albert Lacambra
post_excerpt: ""
layout: post
permalink: https://blog.lacambra.tech/?p=332
published: true
post_date: 2019-05-06 21:54:56
---
When testing you usually need to mock. I mock mostly using Mockito and usually, I stub using <em>when</em> and verify calls using <em>verify</em>.

Normally you will want to verify that a given method has called with specific parameters or that a mocked method returns the desired value only when called also with specific parameters.

In the following class, an article is the same if its <em>id</em> is the same. We can, however, be interested in match the article using its contents (tile and text) instead of its database id.

[java]
public class Article {

  private int id;
  private String title;
  private String text;

  public Article(int id, String title, String text) {
    this.id = id;
    this.title = title;
    this.text = text;
  }

  public int getId() {
    return id;
  }

  public String getTitle() {
    return title;
  }

  public String getText() {
    return text;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Article article = (Article) o;
    return id == article.id;
  }

  @Override
  public int hashCode() {
    return Objects.hash(id);
  }
}

[/java]

Usually, it is enough to use the <em>Mocikto.eq()</em> ArgumentMatcher that will use the Object.equals() method.

[java]
 Mockito.verify(publication).addArticle(Mockito.eq(article));
[/java]

However, if we want to match against its contents, we need a new matcher <em>"ArticleMatcher"</em> that compares title and text. Therefore, I will just create a <em>class ArticleMatcher implements ArgumentMatcher<Article></em>

<article>

[java]
class ArticleMatcher implements ArgumentMatcher
&lt;Article&gt; {

  public final Article article;

  /**
   * register our matcher.
   */
  public static Article eq(Article article) {
    mockingProgress().getArgumentMatcherStorage().reportMatcher(new ArticleMatcher(article));
    return null;
  }

  public ArticleMatcher(Article article) {
    this.article = article;
  }

  /**
   * Implements matches method with our matching logic.
   * @param article
   * @return
   */
  @Override
  public boolean matches(Article article) {
    return this.article.getText().equalsIgnoreCase(article.getText());
  }

  public String toString() {
    return &quot;&lt;ArticleMatcher&gt;&quot;;
  }
}
[/java]

Now we can use our ArgumentMutcher to create stubs and verify calls:

[java]
class ArticleTest {

  @Test
  void checkVerify() {

    Article article1 = new Article(1, &quot;someText&quot;, &quot;title&quot;);
    Article article2 = new Article(2, &quot;someText&quot;, &quot;title&quot;);
    Article article3 = new Article(3, &quot;someText&quot;, &quot;title&quot;);

    Publication publication = Mockito.spy(Publication.class);
    publication.addArticle(article1);

    Mockito.verify(publication).addArticle(ArticleMatcher.eq(article2));
    Mockito.verify(publication, Mockito.times(0)).addArticle(Mockito.eq(article3));

  }

  @Test
  void checkStub() {

    Article article1 = new Article(1, &quot;someText&quot;, &quot;title&quot;);
    Article article2 = new Article(2, &quot;someText&quot;, &quot;title&quot;);
    Article article3 = new Article(3, &quot;someText&quot;, &quot;title&quot;);

    Publication publication = Mockito.spy(Publication.class);
    Mockito.when(publication.getArticlesLike(ArticleMatcher.eq(article2))).thenReturn(Arrays.asList(article1, article2));

    List&lt;Article&gt; articles = publication.getArticlesLike(article3);
    Assertions.assertEquals(2, articles.size());
    Assertions.assertTrue(articles.contains(article1));
    Assertions.assertTrue(articles.contains(article2));
    Assertions.assertFalse(articles.contains(article3));
  }
}
[/java]

So easy :)

code in <a href="https://github.com/alacambra/blogs-posts-code/blob/master/matchers/src/test/java/tech/lacambla/blog/examples/matchers/ArticleTest.java">github</a>