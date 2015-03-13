# Introduction #

This Sample WSDL file can be used to test the automation of the SOAP Web Service client generation.


# Details #

```
<?xml version="1.0" encoding="utf-8"?>
<wsdl:definitions xmlns:s="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/" xmlns:mime="http://schemas.xmlsoap.org/wsdl/mime/" xmlns:i0="http://www.witsml.org/wsdl/120" xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" xmlns:tm="http://microsoft.com/wsdl/mime/textMatching/" xmlns:http="http://schemas.xmlsoap.org/wsdl/http/" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" targetNamespace="http://www.witsml.org/wsdl/120" xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">
  <wsdl:documentation xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">&lt;b&gt;WITSML 1.3.1&lt;/b&gt; (default) and &lt;b&gt;WITSML 1.2.0&lt;/b&gt; are supported.&lt;br&gt;&lt;br&gt;STORE WSDL file is available at &lt;a href="wmls.aspx"&gt;Store interface WSDL&lt;/a&gt;&lt;br&gt;&lt;br&gt;The following functions are defined:&lt;br&gt;&lt;ul&gt;&lt;li&gt;&lt;b&gt;WMLS_AddToStore&lt;/b&gt; - add one new object to the server&lt;br&gt;&lt;li&gt;&lt;b&gt;WMLS_DeleteFromStore&lt;/b&gt; - delete one existing object from the server&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetBaseMsg&lt;/b&gt; - get the fixed "base" description of a return value&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetCap&lt;/b&gt; - get the server’s Capabilities object&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetFromStore&lt;/b&gt; – gets one or more objects from the server&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetVersion&lt;/b&gt; - retrieves the data version(s) that are supported&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_UpdateInStore&lt;/b&gt; - update one existing object on the server&lt;/li&gt;&lt;/ul&gt;</wsdl:documentation>
  <wsdl:import namespace="http://www.witsml.org/wsdl/120" location="wmls_import.wsdl" />
  <wsdl:types />
  <wsdl:service name="WMLS">
    <wsdl:documentation xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">&lt;b&gt;WITSML 1.3.1&lt;/b&gt; (default) and &lt;b&gt;WITSML 1.2.0&lt;/b&gt; are supported.&lt;br&gt;&lt;br&gt;STORE WSDL file is available at &lt;a href="wmls.aspx"&gt;Store interface WSDL&lt;/a&gt;&lt;br&gt;&lt;br&gt;The following functions are defined:&lt;br&gt;&lt;ul&gt;&lt;li&gt;&lt;b&gt;WMLS_AddToStore&lt;/b&gt; - add one new object to the server&lt;br&gt;&lt;li&gt;&lt;b&gt;WMLS_DeleteFromStore&lt;/b&gt; - delete one existing object from the server&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetBaseMsg&lt;/b&gt; - get the fixed "base" description of a return value&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetCap&lt;/b&gt; - get the server’s Capabilities object&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetFromStore&lt;/b&gt; – gets one or more objects from the server&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_GetVersion&lt;/b&gt; - retrieves the data version(s) that are supported&lt;/li&gt;&lt;li&gt;&lt;b&gt;WMLS_UpdateInStore&lt;/b&gt; - update one existing object on the server&lt;/li&gt;&lt;/ul&gt;</wsdl:documentation>
    <wsdl:port name="StoreSoapBinding" binding="i0:StoreSoapBinding">
      <soap:address location="https://path/to/wmls.asmx" />
    </wsdl:port>
  </wsdl:service>
</wsdl:definitions>
```