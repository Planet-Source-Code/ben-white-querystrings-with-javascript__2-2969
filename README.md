<div align="center">

## Querystrings with JavaScript


</div>

### Description

This code allows you to pass information from one page to the next using querystrings and javascript only. no server side processing required.
 
### More Info
 
Example:

querystring.html?x=1&y=2&y=two&z=3&z=three&z=III

qs.x = 1

qs.x[0] = 1

qs.y = 2,two

qs.y[0] = 2

qs.y[1] = two

qs.z = 3,three,III

qs.z[0] = 3

qs.z[1] = three

qs.z[2] = III


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ben White](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ben-white.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |
**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__2-64.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ben-white-querystrings-with-javascript__2-2969/archive/master.zip)





### Source Code

```
<script>
/*
Author: BenWhite@columbus.rr.com
This class allows you to set variabled directly from a querystring
Access variables like this:
	qs.VarName
	qs.Varname[n]
Display Varibles:
	qs.debug()	- Writes debug info to document
	qs.debug(true)	- Returns debug info
Variables that won't work:
	debug
	variables
*/
function clsQueryString() {
	variables = new Array();
	strQuery = document.location.search
	if (strQuery.length >1) {
		strQuery = strQuery.slice(1).split('\&');
		for (i=0; i<strQuery.length; i++) {
			strVar = strQuery[i].split('=')
			if (strVar.length > 1) {
				obj = eval('this.'+strVar[0])
				strVar[1] = unescape(strVar[1].replace(/\'/g,'\\\''));
				if (typeof obj == 'undefined') {
					eval('this.'+strVar[0]+'= new Array()');
					eval('this.'+strVar[0]+'[0]=\''+strVar[1]+'\'')
					variables[variables.length] = strVar[0];
				} else {
					eval('this.'+strVar[0]+'['+obj.length+']=\''+strVar[1]+'\'')
	}	}	}	}
	function debug(bol) {
		strDebug = '';
		strCR = (bol)?'\n':'<br>'
		for (i=0; i<qs.variables.length; i++) {
			strDebug += 'qs.'+qs.variables[i]+' = '+eval('qs.'+qs.variables[i])+strCR;
			for (n=0; n<eval('qs.'+qs.variables[i]+'.length'); n++) {
				strDebug += 'qs.'+qs.variables[i]+'['+n+'] = '+eval('qs.'+qs.variables[i]+'['+n+']')+strCR;
			}
			strDebug += strCR;
		}
		if (bol) {return(strDebug)} else {document.write(strDebug)}
	}
	this.debug = debug;
	this.variables = variables;
}
qs = new clsQueryString();
</script>
```

