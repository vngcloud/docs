# Configure for an Application Load Balancer

On the \[Ingress for an Application Load Balancer] page, we have shown you how to install the LoadBalancer Controller and create ingress via the Ingress Yaml file. The following are detailed meanings of the information you can set for an Ingress

## Annotations <a href="#configureforanapplicationloadbalancer-annotation" id="configureforanapplicationloadbalancer-annotation"></a>

Use the annotations below when creating ingress to customize the Load Balancer to suit your needs:

<table data-full-width="true"><thead><tr><th width="224">Annotations</th><th width="257">Required/Not required</th><th>Meaning</th></tr></thead><tbody><tr><td>vks.vngcloud.vn/load-balancer-id</td><td>Optional</td><td><ul><li><strong>If you do not already have a</strong> previously initialized Application Load Balancer on the vLB system. Now, when creating an Ingress, leave this information blank. After you have implemented Ingress deployment following the instructions at <a href="https://docs.vngcloud.vn/display/VKSVI/Ingress+for+an+Application+Load+Balancer">Ingress for an Application Load Balancer</a> . We will automatically create an ALB on your cluster. This ALB will be displayed on vLB Portal, details can be accessed <a href="https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb">here</a></li><li><p><strong>If you already have a</strong> previously initialized Application Load Balancer on the vLB system and you want to reuse the ALB for your cluster. Now, when creating an Ingress, enter the Load Balancer ID information into this annotation. After you have created Ingress according to the instructions at <a href="https://docs.vngcloud.vn/display/VKSVI/Ingress+for+an+Application+Load+Balancer">Ingress for an Application Load Balancer</a> . If:</p><ul><li><p>Your ALB currently has 2 listeners in it:</p><ul><li>1 listener has HTTP protocol configuration and port 80</li><li>If a listener has HTTPS protocol configuration and port 443, we will use these 2 listeners.</li></ul></li><li>Your ALB does not have either or both listeners with the above configuration, we will automatically create them.</li></ul></li></ul><p>Attention:</p><p>If your ALB has:</p><ul><li>1 listener has HTTP protocol configuration and port 443</li><li>Or a listener configured with HTTPS protocol and portal 80</li></ul><p>then when creating Ingress an error will occur. At this point, you need to edit valid listener information on the vLB system and recreate ingress.</p></td></tr><tr><td>vks.vngcloud.vn/load-balancer-name</td><td>Optional</td><td><ul><li>Annotation <code>vks.vngcloud.vn/load-balancer-name</code>will be used if you <strong>do not</strong> use annotation <code>load-balancer-id</code>.</li><li>Annotation <code>vks.vngcloud.vn/load-balancer-name</code> <strong>only makes sense</strong> when you create a new Ingress resource. After the Ingress resource is successfully created, this annotation <strong>will be automatically deleted</strong> . Using this annotation after the Ingress resource is created will <strong>have no effect</strong> .</li><li><strong>When you use this annotation, if you do not already have a</strong> previously initialized Application Load Balancer on the vLB system. We will automatically create an ALB on your cluster. This ALB will be displayed on vLB Portal, details can be accessed <a href="https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb">here</a></li><li><strong>If you already have a</strong> previously initialized Application Load Balancer on the vLB system and you want to reuse the ALB for your cluster. Now, please enter the Load Balancer Name information into this annotation.</li></ul></td></tr><tr><td>vks.vngcloud.vn/package-id</td><td>Optional</td><td><ul><li>If you do not enter this information, we will use the <strong>ALB Small configuration by default.</strong></li><li>If you already have an ACTIVE vLB host and you want to integrate this host into your K8S cluster, please skip this information field.</li></ul></td></tr><tr><td>vks.vngcloud.vn/tags</td><td>Optional</td><td><ul><li>The tag is added to your ALB.</li></ul></td></tr><tr><td>vks.vngcloud.vn/scheme</td><td>Optional</td><td><ul><li>Default is <strong>internet-facing</strong> , you can change it to <strong>internal</strong> depending on your needs.</li></ul></td></tr><tr><td>vks.vngcloud.vn/security-groups</td><td>Optional</td><td><ul><li>By default, a <strong>default security group</strong> will be created according to your Cluster.</li></ul></td></tr><tr><td>vks.vngcloud.vn/inbound-cidrs</td><td>Optional</td><td><ul><li>Default All CIRD: <strong>0.0.0.0/0</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/healthy-threshold-count</td><td>Optional</td><td><ul><li>Default <strong>3</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/unhealthy-threshold-count</td><td>Optional</td><td><ul><li>Default <strong>3</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-interval-seconds</td><td>Optional</td><td><ul><li>Default <strong>30</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-timeout-seconds</td><td>Optional</td><td><ul><li>Default <strong>5</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-protocol</td><td>Optional</td><td><ul><li>Default <strong>TCP</strong> . The user can select one of the TCP/HTTP values</li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-http-method</td><td>Optional</td><td><ul><li>Default <strong>GET</strong> . User can choose one of GET / POST / PUT values</li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-path</td><td>Optional</td><td><ul><li>Default <strong>/</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-http-version</td><td>Optional</td><td><ul><li>Default <strong>1.0</strong> . Users can choose one of the values ​​1.0, 1.1</li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-http-domain-name</td><td>Optional</td><td><ul><li>Default is empty</li></ul></td></tr><tr><td>vks.vngcloud.vn/healthcheck-port</td><td>Optional</td><td><ul><li>Default <strong>traffic port</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/success-codes</td><td>Optional</td><td><ul><li>Default <strong>200</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/idle-timeout-client</td><td>Optional</td><td><ul><li>Default <strong>50</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/idle-timeout-member</td><td>Optional</td><td><ul><li>Default <strong>50</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/idle-timeout-connection</td><td>Optional</td><td><ul><li>Default <strong>5</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/pool-algorithm</td><td>Optional</td><td><ul><li>Default <strong>ROUND_ROBIN</strong> . The user can select one of the values ​​ROUND_ROBIN / LEAST_CONNECTIONS / SOURCE_IP</li></ul></td></tr><tr><td>vks.vngcloud.vn/enable-sticky-session</td><td>Optional</td><td><ul><li>Default <strong>false</strong> .</li></ul></td></tr><tr><td>vks.vngcloud.vn/enable-tls-encryption</td><td>Optional</td><td><ul><li>Default <strong>false</strong></li></ul></td></tr><tr><td>vks.vngcloud.vn/target-node-labels</td><td>Optional</td><td><ul><li>Default is empty</li></ul></td></tr><tr><td>vks.vngcloud.vn/certificate-ids</td><td>Optional</td><td><ul><li>Default is empty</li></ul></td></tr><tr><td>vks.vngcloud.vn/is-poc</td><td>Optional</td><td><ul><li>Default false.</li></ul><ul><li>If the user specifies this field as true, the system will create a Load Balancer and make payments using the POC wallet balance.</li></ul></td></tr><tr><td>vks.vngcloud.vn/enable-autoscale</td><td>Optional</td><td><ul><li>Default false.</li></ul><ul><li>If the user specifies this field to true, the system will create a Load Balancer with autoscale mode enabled.</li></ul></td></tr><tr><td>vks.vngcloud.vn/ignore</td><td>Optional</td><td><ul><li>Deault false.</li></ul><ul><li>If the user specifies this field as false, our operator will not manage Services and Ingress. Any changes to the resource will be ignored and the LoadBalancer will not be update</li></ul></td></tr><tr><td>vks.vngcloud.vn/implementation-specific-params</td><td>Optional</td><td><ul><li>Default blank</li><li>By default, <strong>ALB policy</strong> has only 1 rule for host and path, with limited operations such as <strong>EQUAL_TO (Exact)</strong> and <strong>START_WITH (Prefix)</strong> . If users want to create more policies or use other operations such as <strong>ENDS_WITH</strong> or <strong>REGEX</strong> , they need to change <strong>pathType</strong> to <strong>ImplementationSpecificParams</strong> and use <strong>annotation</strong> with JSON value to configure. For example:</li></ul><pre class="language-json"><code class="lang-json">[{
  "path": "/haha",
  "rules": [
    {
      "type": "PATH",
      "compare": "EQUAL_TO",
      "value": "/foo#"
    },
    {
      "type": "PATH",
      "compare": "REGEX",
      "value": "/foo#anchor"
    }
  ],
  "action": {
    "action": "REJECT",
    "redirectUrl": "http://golang.cafe/a",
    "redirectHttpCode": 301
  }
}]
</code></pre></td></tr><tr><td>vks.vngcloud.vn/insert-headers</td><td>Optional</td><td><ul><li><p>Default:</p><ul><li>http":["X-Forwarded-For", "X-Forwarded-Proto", "X-Forwarded-Port"]</li><li>https":["X-Forwarded-For", "X-Forwarded-Proto", "X-Forwarded-Port"]</li></ul></li></ul><ul><li>You can override the default configuration by specifying JSON for the annotation <code>vks.vngcloud.vn/insert-headers</code>, for example:</li></ul><pre class="language-json"><code class="lang-json">vks.vngcloud.vn/insert-headers: '{"http":{"X-Forwarded-For":"true", "Access-Control-Allow-Origin": "*"}}'


{
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "GET,POST,OPTIONS",
  "Access-Control-Allow-Headers": "Authorization, Content-Type",
  "Access-Control-Max-Age": "86400",
  "Access-Control-Allow-Credentials": "true",
  "Access-Control-Expose-Headers": "X-Custom-Header, Authorization, Link"
}
</code></pre></td></tr><tr><td>vks.vngcloud.vn/client-certificate-id</td><td>Optional</td><td><ul><li>Default blank</li></ul><ul><li><strong>Client CA is a Load Balancer</strong> security feature that authenticates clients using <strong>client certificates</strong> to allow authorized clients to access an application or service. Passing a portal <strong>certificate id to</strong> this <strong>annotation</strong> will enable <strong>the Client CA</strong> for <strong>the https listener</strong> .</li></ul></td></tr></tbody></table>

***

## IngressClassName <a href="#configureforanapplicationloadbalancer-ingressclassname" id="configureforanapplicationloadbalancer-ingressclassname"></a>

The Ingress installed by the VNGCloud LoadBalancer Controller will have the information IngressClassName = "vngcloud". You may not change this information.

***

## DefaultBackend <a href="#defaultbackend" id="defaultbackend"></a>

* An Ingress without any rules will send all traffic to a single default service default backend, or if no _host_ and _path_ match the HTTP request in the Ingress Yaml file, traffic will be routed to the service default backend. For example below, we are configuring the default if the request does not satisfy any rule in the Ingress yaml file, it will go to service name: example-svc-1 with port number 8080

```
defaultBackend:
    service:
      name: example-svc-1
      port:
        number: 8080
```

***

## TLS <a href="#configureforanapplicationloadbalancer-tls" id="configureforanapplicationloadbalancer-tls"></a>

You can secure Ingress by specifying a Secret that contains the TLS key and certificate. Currently Ingress only supports TLS port 443 and is the termination point for TLS (TLS termination). TLS Secret must contain fields with key names tls.crt and tls.key, which are the certificate and private key to use for TLS. Specifically, you need to specify:

* Host: the specified hosts will use the cert.
* SecretName: secret name containing cert.

***

## Path types <a href="#configureforanapplicationloadbalancer-pathtypes" id="configureforanapplicationloadbalancer-pathtypes"></a>

Each path in Ingress has a corresponding pathType. There are three supported pathTypes:

* Exact: Matches the URL path with absolute precision and is case sensitive.
* Prefix: Matches based on the URL path prefix separated by /. Matching is case-sensitive and is performed on each element of the URL path. A component of the main URL path is a label separated by a / in the URL path (This means that the URL path can consist of multiple levels separated by /, each string is between two main / marks). is a label, each label is a component of the URL path). A URL request is considered to match a path field (configured in the Ingress specification) when the entire value of the path (which can include multiple components separated by /) matches the first labels (adjectives). left of the URL). For example /example1/path1 matches /example1/path1/path2, but not /example1/path1path2

Specific examples:

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Path type</td><td>Path(s)</td><td>Request path(s)</td><td>Is there a match or not?</td></tr><tr><td>Exact</td><td><code>/example1</code></td><td><code>/example1</code></td><td>Have</td></tr><tr><td>Exact</td><td><code>/example1</code></td><td><code>/host1</code></td><td>Are not</td></tr><tr><td>Exact</td><td><code>/example1</code></td><td><code>/example1/</code></td><td>Are not</td></tr><tr><td>Exact</td><td><code>/example1/</code></td><td><code>/example1</code></td><td>Are not</td></tr><tr><td>Prefix</td><td><code>/</code></td><td>(all paths)</td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1</code></td><td><code>/example1</code>,<code>/example1/</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/</code></td><td><code>/example1</code>,<code>/example1/</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/host11</code></td><td><code>/example1/host1</code></td><td>Are not</td></tr><tr><td>Prefix</td><td><code>/example1/host1</code></td><td><code>/example1/host1</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/host1/</code></td><td><code>/example1/host1</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/host1</code></td><td><code>/example1/host1/</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/host1</code></td><td><code>/example1/host1/ccc</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1/host1</code></td><td><code>/example1/host1xyz</code></td><td>Are not</td></tr><tr><td>Prefix</td><td><code>/</code>,<code>/example1</code></td><td><code>/example1/ccc</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/</code>, <code>/example1</code>,<code>/example1/host1</code></td><td><code>/example1/host1</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/</code>, <code>/example1</code>,<code>/example1/host1</code></td><td><code>/ccc</code></td><td>Have</td></tr><tr><td>Prefix</td><td><code>/example1</code></td><td><code>/ccc</code></td><td>Are not</td></tr></tbody></table>

* In some cases, multiple paths within Ingress will match the path of the request URL. In those cases, priority will be given to the longest matching path first. If the two paths still have the same length, the priority will be in the order of the rule created on the Ingress Yaml file.

***

## Ingress rule <a href="#configureforanapplicationloadbalancer-ingressrule" id="configureforanapplicationloadbalancer-ingressrule"></a>

Each HTTP rule contains the following information:

* **1 optional host** . If no host (we can understand it as a domain name) is specified, the rule will be applied to all HTTP traffic inbound to the specified IP address. If a host is specified (for example example1.com), the rule only applies to that host.
* **A list of paths (** for example `/example1/host1`), each path has a backend service associated with it defined by Service Name and Port Number. Both host and path must match the content of the incoming request before the load balancer directs traffic to the desired Services.
* **A backend** is a combination of the Service name and Port Number. HTTP and HTTPS requests going to Ingress and whose URL matches the host and path of the rule will be sent to the list of backends.

For example, does Host match the Host header according to the table:

| Host                                       | Host header                                                      | Is there a match or not? |
| ------------------------------------------ | ---------------------------------------------------------------- | ------------------------ |
| `*.`[`example1.com`](http://example1.com/) | [`example2.example1.com`](http://example2.example1.com/)         | Have                     |
| `*.`[`example1.com`](http://example1.com/) | [`baz.example2.example1.com`](http://baz.example2.example1.com/) | Are not                  |
| `*.`[`example1.com`](http://example1.com/) | [`example1.com`](http://example1.com/)                           | Are not                  |
