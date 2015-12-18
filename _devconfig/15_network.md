---
layout: page
title: How do I PIV enable my network logon?
permalink: /15_network/
---
<script>
$(function() {
  $( "#accordion" ).accordion({
    heightStyle: "content",
    collapsible: "true"
  });
});
</script>
#### Overview

PIV Authentication to for the purposes of network logon requires the configuration of a number of components in an agency's architecture. At a high level, the following components will be required and configured:
<ul>
<li>A user directory</li>
<li>CA certificates that signed the card certificates that will be accepted</li>
<li>User data linking the cards to the accounts in the user directory</li>
<li>User card readers</li>
</ul>

As with any PKI implementation, all parties must trust the Root CA to which the issuing CA chains. Both the domain controllers and the smartcard workstations trust this root.

#### Before you get started:
<ul>
<li>Required: Identify and the credential issuing / signing CA chain.</li>
<li>Required: Identify network entry points that you will enable.</li>
<li>Required: Determine the protocols you'll be using for validation and revocation (SCVP, TAMP, OCSP, CRL).</li>
</ul>

#### Complete the following steps:
<div id="accordion">
  <h3>1. Setup your user directory</h3>
  <div>
    <p>For users internal to an agency, users and their access rights are typically stored in a directory. Your agency may already have a directory capable of filling this role. If you do, it is recommended that you utilize the existing system as appropriate to the enterprise. Typically, client applications can communicate with these servers using the Lightweight Directory Access Protocol (LDAP). Some examples of vendor server products that can accomplish this task are:</p>
    <ul>
    <li>Microsoft Active Directory</li>
    <li>Oracle Unified Directory</li>
    <li>IBM Security Directory Server</li>
    </ul>
    <p>Please refer to your product's documentation for details on configuring a new system.</p>
  </div>
  <h3>2. Import the trusted CA Certificates.</h3>
  <div>
    <p>PKI Authentication Certificates that are stored on a PIV card have been signed by trusted Certification Authorities (CA). These certificates must be imported into the authentication mechanism's trust store to validate that the presented certificate is trusted and original.</p>
    <p>Reference the following guides to import the trusted CA certificates into your trust store:</p>
    <ul>
    <li>Guide for product x</li>
    <li>Guide for product x</li>
    <li>Guide for product x</li>
    <li>Guide for product x</li>
    </ul>
  </div>
  <h3>3. Configure your access management tool.</h3>
  <div>
    <p>Your access management tool must be able to authenticate the credential provided by the user. --other details here--</p>
    <ul>
      <li><a href="{{ site.baseurl }}/3_ad/">Microsoft Active Directory</a></li>
      <li>Follow this step.</li>
      <li>Follow this step.</li>
      <li>Follow this step.</li>
    </ul>
  </div>
  <h3>4. Configure your client hardware.</h3>
  <div>
    <p>Users typically access network resources through devices such as laptops, desktops, or mobile devices. The configuration of those client systems are typically operating system specific. --other details here--</p>
    <p>Refer to the following guides to configure the following client systems to accept PIV credentials:</p>
    <ul>
    <li><a href="{{ site.baseurl }}/3_ad/">Microsoft Windows</a></li>
    <li><a href="{{ site.baseurl }}/2_mac/">Apple OSX</a></li>
    <li><a href="{{ site.baseurl }}/1_unix/">Red Hat Linux</a></li>
    </ul>
  </div>
  <h3>5. Configure your client software.</h3>
  <div>
    <p>Depending on the use case, there may be various software components that require configuration. These may include native operating system configuration or VPN software configuration.</p>
    <p>Refer to the following guides to configure the following software components:</p>
    <ul>
    <li><a href="{{ site.baseurl }}/3_ad/">Microsoft Windows</a></li>
    <li><a href="{{ site.baseurl }}/2_mac/">Apple OSX</a></li>
    <li><a href="{{ site.baseurl }}/2_mac/">XYZ VPN Software</a></li>
    </ul>
  </div>
</div>

#### Test your solution!

  Insert your PIV card. Enter your pin. Viola.
  <ul>
    <li>Follow this step.</li>
    <li>Follow this step.<br/>
      <div class="code">Here's a block of interesting code.</div>
    </li>
    <li>Follow this step.</li>
  </ul>

#### References

TBD

#### Related Playbooks

<ul>
<li><a href="{{ site.baseurl }}/4_adadmin/" title="How do I enable Microsoft AD for Admin access?">How do I enable Microsoft AD for Admin access?</a></li>
<li><a href="{{ site.baseurl }}/5_domainassert/" title="How do I enable a domain to assert assurance in AD?">How do I enable a domain to assert assurance in AD?</a></li>
<li><a href="{{ site.baseurl }}/9_trustwindows/" title="How do I validate trust stores on a Windows platform?">How do I validate trust stores on a Windows platform?</a></li>
</ul>
