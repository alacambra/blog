---
ID: 45
post_title: >
  Create a correct 201 Created response
  with JAX-RS
author: alacambra
post_date: 2016-09-18 16:57:41
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/create-a-correct-201-created-response/
published: true
---

[java]
@POST
@Path(&quot;project&quot;)
public Response createProject(@Context UriInfo uriInfo, JsonObject json) {
        Project project = projectConverter.fromJson(json);
        project.setWorkspace(getCurrentWorkspace());
        project = em.merge(project);

        URI uri = uriInfo.getBaseUriBuilder()
                .path(ProjectResource.class)
                .resolveTemplate(PathExpressions.workspaceId, getCurrentWorkspace().getId())
                .resolveTemplate(PathExpressions.projectId, project.getId())
                .build();

        return Response.created(uri).build();
[/java]

<pre>The <em><strong>@Context UriInfo uriInfo </strong></em>provides information about the current URI. 
The <em><strong>.path(ProjectResource.class) </strong></em> call will return the path used for the ProjectResource.class. 
The <em><strong>.resolveTemplate("<span class="pl-s">{workspace</span>Id:<span class="pl-cce">\\</span>d+<span class="pl-s">}"</span>, getCurrentWorkspace().getId()) </strong></em> will replace the <em>workspaceId</em> template variable for the actual<em> wokspace id</em>.

Once the whole path has been created, it is only needed to put it into a <em>created</em> response.
</pre>