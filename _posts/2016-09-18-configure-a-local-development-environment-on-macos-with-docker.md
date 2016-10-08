---
ID: 32
post_title: >
  Configure a local development
  environment on MacOS with Docker
author: alacambra
post_date: 2016-09-18 14:56:29
post_excerpt: ""
layout: post
permalink: >
  http://chronicles.lacambra.de/wordpress/2016/09/18/configure-a-local-development-environment-on-macos-with-docker/
published: true
---
<h2>Using dnsmasq for development domains</h2>
With dnsmasq I am redirecting my developer domains to its corresponding target:
<ul>
 	<li>*.dev: localhost</li>
 	<li>*.dock: docker container</li>
</ul>
So no more ip stuff on the browser url.
<h4><a id="Install_dmasq_on_mac_OS_X_7"></a>Install dmasq on mac OS X:</h4>
<em>(from <a href="http://passingcuriosity.com/2013/dnsmasq-dev-osx/">http://passingcuriosity.com/2013/dnsmasq-dev-osx/</a>)</em>
<pre><code class="language-bash">brew install dnsmasq
<span class="hljs-comment"># Copy the default configuration file.</span>
cp $(brew list dnsmasq | grep /dnsmasq.conf.example$) /usr/<span class="hljs-built_in">local</span>/etc/dnsmasq.conf
<span class="hljs-comment"># Copy the daemon configuration file into place.</span>
sudo cp $(brew list dnsmasq | grep /homebrew.mxcl.dnsmasq.plist$) /Library/LaunchDaemons/
<span class="hljs-comment"># Start Dnsmasq automatically.</span>
sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
</code></pre>
<h4><a id="Configure_dmasq_19"></a>Configure dmasq:</h4>
<em>(/usr/local/etc/dnsmasq.conf)</em>
<pre><code class="language-bash"><span class="hljs-comment">#Redirect *.dev urls to 127.0.0.1</span>
address=/dev/<span class="hljs-number">127.0</span>.<span class="hljs-number">0.1</span>

<span class="hljs-comment">#Redirect *.dock urls to docker host url (192.168.99.100 in my case)</span>
address=/dock/<span class="hljs-number">192.168</span>.<span class="hljs-number">99.100</span>
</code></pre>
and restart dnsmasq:
<pre><code class="language-bash">sudo launchctl stop homebrew.mxcl.dnsmasq
sudo launchctl start homebrew.mxcl.dnsmasq
</code></pre>
Then you need to say the OS to use Dnsmasq for the desired domain. Most UNIX-like operating systems have a configuration file called <code>/etc/resolv.conf</code> which controls the way DNS queries are performed, including the default server to use for DNS queries (this is the setting that gets set automatically when you connect to a network or change your DNS server/s in System Preferences).

OS X also allows you to configure additional <em>resolvers</em> by creating configuration files in the<code>/etc/resolver/</code> directory. This directory probably won’t exist on your system, so your first step should be to create it:
<div class="sourceCode">
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">sudo</span> mkdir -p /etc/resolver</code></pre>
</div>
Now you should create a new file in this directory for each resolver you want to configure.  There a number of details you can configure for each resolver but I generally only bother with two:
<ul>
 	<li>the <em>name</em> of the resolver (which corresponds to the <em>domain name</em> to be resolved); and</li>
 	<li>the DNS server to be used.</li>
</ul>
Create a new file with <em>the same name</em> as your new top-level domain (I’m using dec and dock) in the <code>/etc/resolver/</code> directory and add a <code>nameserver</code> to it by running the following commands:
<pre class="sourceCode bash"><code class="sourceCode bash"><span class="kw">sudo</span> tee /etc/resolver/dev <span class="kw">&gt;</span>/dev/null &lt;&lt;EOF
nameserver 127.0.0.1
EOF</code></pre>
<h4><a id="Binding_all_services_34"></a>Binding all services</h4>
I am developing an application that needs several resources:
<ul>
 	<li>Wildfly AS</li>
 	<li>Mysqls DB</li>
 	<li>keycloak</li>
 	<li>An nginx server as proxy.</li>
</ul>
To avoid to write each time the ports, I am using nginx to redirect the requests to the correct container. All the containers must be able to locate the proxy server and the proxy will do the rest. To achieve that, when we run a container we need to link it to the proxy server with the domain of the required service. E.g. to get my widlfly App signing in using the keycloak server, we will run the containers as follows:
<pre><code class="language-bash">docker run --link proxy:keycloak.dock some/wildlfy
docker run --link proxy:app.dock some/keycloak
</code></pre>
<h3><a id="Configuring_the_proxy_52"></a>Configuring the proxy:</h3>
In order to allow the proxy to bind all services we need to add some server configs: For the widlfy app, a file named <em>app.dock</em> will be added in the conf.d directory:
<pre><code>server {
    listen      80;
    server_name app.dock;

        location / {
            proxy_pass http://${docker-host-ip}:${widlfly-app-port};
            proxy_set_header Host $http_host;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

      # needed to map the ip address to the correct domain
      proxy_redirect http://${docker-host-ip}:${widlfly-app-port} http://app.dock;
            proxy_redirect ${docker-host-ip}:${keycloak-port} http://keycloak.dock;
        }

    access_log /var/log/nginx/app.dock_access.log;
        error_log /var/log/nginx/app.dock_error.log;
}
</code></pre>
and for the keycloak:
<pre><code>server {
    listen      80;
    server_name app.dock;

        location / {
            proxy_pass http://${docker-host-ip}:${keycloak-port};
            proxy_set_header Host $http_host;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

      # needed to map the ip address to the correct domain
            proxy_redirect ${docker-host-ip}:${keycloak-port} http://keycloak.dock;
        }

    access_log /var/log/nginx/app.dock_access.log;
        error_log /var/log/nginx/app.dock_error.log;
}</code></pre>