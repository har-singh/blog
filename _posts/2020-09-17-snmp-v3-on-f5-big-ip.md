---
layout: post
title: SNMP v3 on F5 BIG-IP
date: 2020-09-17 16:01
author: har-singh
comments: true
categories: [bigip, snmp, technical]
---
<!-- wp:paragraph -->
<p>A post to document and share the cli commands required to configure SNMP agent on F5 device.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Via the GUI the configuration is pretty much straight forward:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Allow NMS IP to the list at <strong>System &gt; SNMP &gt; Agent &gt; Configuration</strong><ul><li>I had to struggle here as the snmpwalk test was working from the bigip box when pointing to localhost (127.0.0.1) however the snmpwalk against the management IP didn't work. By default (and F5 is default deny device) the SNMP requests are blocked.</li></ul></li><li>Add user by navigating to <strong>System &gt; SNMP &gt; Agent &gt; Access (v3)</strong><ul><li>more information about Authentication type, Privacy protocol, Security level can be retrived from the F5 knowledge base article <a rel="noreferrer noopener" href="https://support.f5.com/csp/article/K13625" target="_blank">K13625</a></li></ul></li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><em>Note: what to put for the <strong>OID </strong>was a bit tricky as it is a mendatory field and I had no clue on what to put in there. Looking at kb article I found that <strong>.1</strong> can be specifed to get all the MIBs.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>What I've done is to create a user via GUI and issues the <code>show running-config sys snmp users</code> command at the CLI to get syntax; which is the following:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>root@(bigip1)(cfg-sync Standalone)(Active)(/Common)(tmos)# show running-config sys snmp users
sys snmp {
    users {
        idemo_1 {
            auth-password-encrypted "XICfN\?MFr6CM=jHBg^p]VM;IUPkcY7jY@q\?=BRd/^HjSX8I"
            auth-protocol sha
            oid-subset .1
            privacy-password-encrypted 9b&lt;L`=8:qgB_3\\CIJo8OjR)iLPPwH30_TbSAWLfoeQi\?i6W
            privacy-protocol aes
            security-level auth-privacy
            username demo
        }
    }
}

</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>From this I've created the command which can be issues directly to the CLI create create the user:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>modify sys snmp allowed-addresses add { 10.0.0.0/255.0.0.0 }

modify sys snmp users add { snmpuser-entry {  auth-password "MakeUpSomePassword" auth-protocol sha oid-subset .1 privacy-password "MakeUpSomePassword" privacy-protocol aes security-level auth-privacy username snmpuser } }</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>The test section:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>snmpget -v3 -u snmpuser -a SHA -A "MakeUpSomePassword" -x AES -X "MakeUpSomePassword" -l authPriv 192.168.1.245 iso.3.6.1.2.1.1.5.0

Answer:
iso.3.6.1.2.1.1.5.0 = STRING: "bigip1.f5lab.com"
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The knowledge base article <a rel="noreferrer noopener" href="https://support.f5.com/csp/article/K12601" target="_blank">K12601</a> is being reported as archived but was very useful to understand the commands.</p>
<!-- /wp:paragraph -->
