---
ID: 45
post_title: Create a correct 201 Created response
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
    @AllowedTo({Role.MEMBER, Role.OWNER})
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