---
layout: page
title: How do I enable Microsoft AD for PIV Logon?
permalink: /3_ad/
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

Smart Card Authentication to Active Directory requires that Smartcard workstations, Active Directory, and Active Directory domain controllers be configured properly. Active Directory must trust a certification authority to authenticate users based on certificates from that CA. Both Smartcard workstations and domain controllers must be configured with correctly configured certificates.

As with any PKI implementation, all parties must trust the Root CA to which the issuing CA chains. Both the domain controllers and the smartcard workstations trust this root.

#### Before you get started:
<ul>
<li>Required: Active Directory must have the third-party issuing CA in the NTAuth store to authenticate users to active directory.</li>
<li>Required: Domain controllers must be configured with a domain controller certificate to authenticate smartcard users.</li>
<li>Optional: Active Directory can be configured to distribute the third-party root CA to the trusted root CA store of all domain members using the Group Policy.</li>
</ul>

#### Complete the following steps:
<div id="accordion">
  <h3>1. Add the root CA to the trusted roots in an Active Directory Group Policy object.</h3>
  <div>
    To configure Group Policy in the Windows 2000 domain to distribute the third-party CA to the trusted root store of all domain computers:
    <ol>
    <li>Click Start, point to Programs, point to Administrative Tools, and then click <b>Active Directory Users and Computers</b>.</li>
    <li>In the left pane, locate the domain in which the policy you want to edit is applied.</li>
    <li>Right-click the domain, and then click <b>Properties</b>.</li>
    <li>Click the <b>Group Policy</b> tab.</li>
    <li>Click the <b>Default Domain Policy Group Policy</b> object, and then click <b>Edit</b>. A new window opens.</li>
    <li>In the left pane, expand the following items:<br/>
      <ul>
        <li>Computer Configuration</li>
        <li>Windows Settings</li>
        <li>Security Settings</li>
        <li>Public Key Policy</li>
      </ul>
    </li>
    <li>Right-click Trusted Root Certification Authorities.</li>
    <li>Select All Tasks, and then click Import.</li>
    <li>Follow the instructions in the wizard to import the certificate.</li>
    <li>Click OK.</li>
    <li>Close the Group Policy window.</li>
    </ol>
  </div>
  <h3>2. Add the third-party issuing the CA to the NTAuth store in Active Directory.</h3>
  <div>
    The smart card logon certificate must be issued from a CA that is in the NTAuth store. By default, Microsoft Enterprise CAs are added to the NTAuth store.
    <ul>
      <li>If the CA that issued the smart card logon certificate or the domain controller certificates is not properly posted in the NTAuth store, the smart card logon process does not work. The corresponding answer is "Unable to verify the credentials".</li>
      <li>The NTAuth store is located in the Configuration container for the forest. For example, a sample location is as follows:<br/><br/>
      <div class="code">LDAP://server1.name.com/CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=name,DC=com</div></li>
      <li>By default, this store is created when you install a Microsoft Enterprise CA. The object can also be created manually by using ADSIedit.msc in the Windows 2000 Support tools or by using LDIFDE. For more information, click the following article number to view the article in the Microsoft Knowledge Base:<br/><br/>
      <p>295663 How to import third-party certification authority (CA) certificates into the Enterprise NTAuth store</p></li>
      <li>The relevant attribute is cACertificate, which is an octet String, multiple-valued list of ASN-encoded certificates.
      <br/>After you put the third-party CA in the NTAuth store, Domain-based Group Policy places a registry key (a thumbprint of the certificate) in the following location on all computers in the domain:
      <br/><br/><div class="code">HKEY_LOCAL_MACHINE\Software\Microsoft\EnterpriseCertificates\NTAuth\Certificates</div>
      This is refreshed every eight hours on workstations (the typical Group Policy pulse interval).</li>
    </ul>
  </div>
  <h3>3. Request and install a domain controller certificate.</h3>
  <div>
    <p> Request and install a domain controller certificate on the domain controller(s). Each domain controller that is going to authenticate smartcard users must have a domain controller certificate.</p>
    <p>If you install a Microsoft Enterprise CA in an Active Directory forest, all domain controllers automatically enroll for a domain controller certificate. For more information about requirements for domain controller certificates from a third-party CA, click the following article number to view the article in the Microsoft Knowledge Base:</p>
    <p class="code"><a href="https://support.microsoft.com/en-us/kb/291010">291010</a> Requirements for domain controller certificates from a third-party CA</p>
    <p>NOTE: The domain controller certificate is used for Secure Sockets Layer (SSL) authentication, Simple Mail Transfer Protocol (SMTP) encryption, Remote Procedure Call (RPC) signing, and the smart card logon process. Using a non-Microsoft CA to issue a certificate to a domain controller may cause unexpected behavior or unsupported results. An improperly formatted certificate or a certificate with the subject name absent may cause these or other capabilities to stop responding.</p>
  </div>
  <h3>4. Correlate PIV card Certificates with active directory accounts.</h3>
  <div>
    <p>Placeholder.</p>
  </div>
  <h3>5. Install smart card reader hardware and drivers.</h3>
  <div>
    <p>Install the smart card reader hardware as specified by the hardware vendor's documentation.</p>
  </div>
</div>

#### Test your solution!

  Insert your PIV card.
  <ol>
    <li>Insert your PIV card into your card reader.</li>
    <li>Enter the PIN to unlock the card.</li>
    <li>Verify that authentication occurred successfully.</li>
  </ol>

#### Troubleshooting

  Placeholder.

#### References

  This guide was derived from a <a href="https://support.microsoft.com/en-us/kb/281245">Microsoft Knowledgebase Article</a>.

#### Related Playbooks

<ul>
<li><a href="{{ site.baseurl }}/4_adadmin/" title="How do I enable Microsoft AD for Admin access?">How do I enable Microsoft AD for Admin access?</a></li>
<li><a href="{{ site.baseurl }}/5_domainassert/" title="How do I enable a domain to assert assurance in AD?">How do I enable a domain to assert assurance in AD?</a></li>
<li><a href="{{ site.baseurl }}/9_trustwindows/" title="How do I validate trust stores on a Windows platform?">How do I validate trust stores on a Windows platform?</a></li>
</ul>
