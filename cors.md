- Add the following to the head portion of the Fiddler script:
```js
public static RulesOption("Force CORS")
var m_ForceCORS: boolean = true;
```

- Add the following at the end of the `OnBeforeResponse` method:
```js
if (m_ForceCORS && oSession.oRequest.headers.Exists("Origin")) { 
	oSession.oResponse.headers.Remove("Access-Control-Allow-Origin");
	oSession.oResponse.headers.Add("Access-Control-Allow-Origin", oSession.oRequest.headers["Origin"]) ;
	
	oSession.oResponse.headers.Remove("Access-Control-Allow-Methods");
	oSession.oResponse.headers.Add("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
	
	oSession.oResponse.headers.Remove("Access-Control-Allow-Headers"); 
	oSession.oResponse.headers.Add("Access-Control-Allow-Headers", "Content-Type, Authorization, Accept, Csrf-Token, X-Requested-With, cloudSession, WbeSession, Cookie");
	
	oSession.oResponse.headers.Remove("Access-Control-Max-Age");
	oSession.oResponse.headers.Add("Access-Control-Max-Age", "1728000");
	
	oSession.oResponse.headers.Remove("Access-Control-Allow-Credentials");
	oSession.oResponse.headers.Add("Access-Control-Allow-Credentials", "true");
	 
	// if (oSession.oRequest.headers.Exists("Cookie")) {
		// oSession.oResponse.headers.Remove("Set-Cookie");
		// oSession.oResponse.headers.Add("Set-Cookie", oSession.oRequest.headers["Cookie"]);
	// }
}
```
